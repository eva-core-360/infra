# Eva Engine® — Orchestration Model v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** definir como o Eva Engine® transforma uma necessidade de processamento em um plano controlado de execução, selecionando capabilities por contrato, evidência, saúde, risco, custo, latência e policy sem transformar o Orchestrator em um cérebro monolítico ou gargalo central.

---

# 1. Definição

O **Orchestrator** é o maestro operacional do organismo.

Ele não deve ser a capability que “sabe tudo”.

Sua responsabilidade é coordenar capacidades distribuídas sob contratos explícitos:

```text
entender requisito operacional
        ↓
descobrir capabilities elegíveis
        ↓
filtrar por policy / scope / health
        ↓
montar plano de execução
        ↓
alocar orçamento
        ↓
despachar trabalho
        ↓
observar resultados
        ↓
decidir continuar / parar / degradar / escalar
```

Princípio:

> **O Orchestrator coordena inteligência; ele não deve absorver a inteligência que coordena.**

---

# 2. O problema que a orquestração resolve

Sem uma camada de orquestração explícita, um sistema com dezenas ou centenas de mecanismos tende a cair em um destes extremos:

```text
EXTREMO A
pipeline rígido
sempre chama tudo
custo alto
latência alta
pouca adaptação

EXTREMO B
agentes chamando agentes livremente
fan-out imprevisível
loops
custo sem controle
baixa auditabilidade
explosão combinatória
```

O Eva Engine® precisa de um terceiro caminho:

> **execução dinâmica, porém limitada, explicável e governada.**

---

# 3. Separação fundamental: Control Plane e Execution Plane

**DECISÃO APROVADA COMO PRINCÍPIO ARQUITETURAL**

A orquestração deve separar logicamente:

```text
CONTROL PLANE
- decide
- planeja
- seleciona
- autoriza
- aloca budget
- monitora
- replaneja
- interrompe
- escalona

EXECUTION PLANE
- executa capabilities
- produz artifacts
- produz evidence/signals
- reporta metrics
- reporta health/failure
```

Diagrama:

```text
┌───────────────────────────────────────────────────────────────┐
│                    ORCHESTRATION CONTROL PLANE                │
│                                                               │
│ Requirement → Registry Query → Planner → Admission → Dispatch │
│                              │                     │          │
│                              ▼                     ▼          │
│                         Budget Manager        Runtime Monitor  │
│                              │                     │          │
│                              └──────────┬──────────┘          │
│                                         ▼                     │
│                                Stop / Replan / Escalate       │
└───────────────────────────────────────┬───────────────────────┘
                                        │ invocation permits
                                        ▼
┌───────────────────────────────────────────────────────────────┐
│                         EXECUTION PLANE                       │
│                                                               │
│   Rules · SQL · Parsers · Graph · Statistics · Local Models  │
│             Agents · External AI · Human Authority           │
│                                                               │
└───────────────────────────────────────┬───────────────────────┘
                                        │ artifacts / metrics
                                        └──────────────► Control Plane
```

O Execution Plane não ganha autoridade para redefinir globalmente o plano sem passar pelo Control Plane.

---

# 4. O Orchestrator recebe requisitos, não nomes de agentes

Entrada conceitual:

```text
TaskRequirement
├── requirement_id
├── objective
├── input_refs[]
├── required_output_schema?
├── required_quality?
├── risk_class
├── privacy_scope
├── latency_budget
├── compute_budget
├── cost_budget
├── evidence_requirement
├── reversibility_class
├── deadline?
└── policy_context
```

Exemplo:

```text
objective = reconstruct_incident_sequence
required_quality = HIGH
risk_class = HIGH
cost_budget = 4.00 USD
deadline = 2s
```

O Orchestrator pergunta ao Capability Registry quais mecanismos podem satisfazer o requisito.

Ele não deve receber instruções como:

```text
"chame Agent42"
```

como arquitetura padrão.

---

# 5. Planejamento por Work Graph

O plano de execução deve ser representável como um **Work Graph**, preferencialmente um DAG quando o problema permitir.

```text
                        TASK ROOT
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
          ENTITY        TEMPORAL        RETRIEVAL
          RESOLVE        PARSE            │
              │             │             │
              └──────┬──────┴──────┬──────┘
                     ▼             ▼
                 SEQUENCE       CONTEXT
                     │             │
                     └──────┬──────┘
                            ▼
                        EVIDENCE
                            │
                            ▼
                       CHALLENGER
                            │
                            ▼
                         RESULT
```

Contrato conceitual:

```text
OrchestrationPlan
├── plan_id
├── trace_id
├── root_requirement_id
├── nodes[]
├── edges[]
├── execution_mode
├── budgets
├── stop_policy
├── escalation_policy
├── fallback_policy
├── created_by
├── created_at
└── version
```

Cada nó declara capability requerida, dependências e condições de execução.

---

# 6. Plan Node

```text
PlanNode
├── node_id
├── capability_requirement
├── candidate_capabilities[]
├── selected_capability?
├── input_refs[]
├── output_schema
├── dependencies[]
├── can_run_parallel
├── timeout
├── retry_policy
├── fallback_policy
├── budget_slice
├── risk_class
├── required_health
├── evidence_requirement
└── status
```

Estados iniciais:

```text
PENDING
READY
RUNNING
SUCCEEDED
DEGRADED
FAILED
SKIPPED
CANCELLED
ESCALATED
```

---

# 7. Hierarquia de orquestração

Um único processo central não deve gerenciar diretamente milhões de microdecisões.

O modelo deve permitir **orquestração hierárquica com execução descentralizada**.

```text
ROOT ORCHESTRATOR
        │
        ├──► SUB-PLAN A
        │       ├── capability
        │       └── capability
        │
        ├──► SUB-PLAN B
        │       ├── capability
        │       └── capability
        │
        └──► SUB-PLAN C
```

Cada subplano recebe:

```text
scope
budget_slice
risk_limit
max_depth
max_fanout
deadline
policy_context
```

O subplano não pode ultrapassar esses limites silenciosamente.

Princípio:

> **Delegar trabalho não significa delegar autoridade ilimitada.**

---

# 8. Budget Tokens / Budget Slices

O Processing Context já prevê budgets. A orquestração transforma isso em distribuição concreta.

Exemplo conceitual:

```text
TOTAL BUDGET
cost = 10.00
latency = 2000ms
compute = 100 units
waves = 4

        │
        ├── Context      15%
        ├── Retrieval    20%
        ├── Analysis     25%
        ├── Challenger   20%
        └── Reserve      20%
```

A reserva permite escalonamento somente se necessário.

Budgets possíveis:

```text
cost_budget
latency_budget
compute_budget
memory_budget
fanout_budget
wave_budget
external_ai_budget
human_budget
risk_budget
```

O orçamento deve ser consumido e registrado no trace.

---

# 9. Admission Control

Antes de executar um nó, o sistema deve executar **Admission Control**.

Perguntas:

```text
schema é compatível?
policy permite?
capability está saudável?
scope permite acesso aos dados?
budget ainda existe?
risco permite automação?
deadline ainda é viável?
dependências foram satisfeitas?
fallback existe se falhar?
```

Saídas:

```text
ADMIT
ADMIT_WITH_RESTRICTIONS
DEFER
REJECT
ESCALATE
```

Princípio:

> **Capability disponível não significa capability autorizada.**

---

# 10. Seleção de capability

Seleção não deve se basear em um único score global.

Critérios possíveis:

```text
quality evidence
health
risk fit
privacy fit
latency
cost
historical calibration
failure rate
context fit
provider constraints
reversibility
```

Forma conceitual:

```text
Eligibility = hard_constraints(...)

Ranking = f(
  expected_quality,
  health,
  cost,
  latency,
  risk,
  context_fit,
  historical_performance
)
```

Hard constraints filtram primeiro. Ranking ocorre apenas entre candidatos elegíveis.

---

# 11. Deterministic-first não significa deterministic-only

A direção econômica permanece:

```text
mecânica / deterministic
        ↓ se insuficiente
heuristic / statistical
        ↓ se insuficiente
specialist / local model
        ↓ se insuficiente
agent / external AI
        ↓ se insuficiente
human authority
```

Mas essa sequência **não é uma escada obrigatória para todo evento**.

Em casos de alto risco, baixa reversibilidade ou prazo curto, policy pode pular níveis.

Exemplo:

```text
risk = CRITICAL
reversibility = LOW

→ exige HUMAN_AUTHORITY diretamente
```

Princípio:

> **Preferência por mecânica é política econômica e de previsibilidade; não dogma que ignora risco.**

---

# 12. Parallelism

Capabilities independentes podem executar em paralelo.

```text
             EVENT
               │
      ┌────────┼────────┐
      ▼        ▼        ▼
   Temporal  Entity   Schema
      │        │        │
      └────────┼────────┘
               ▼
             Join
```

O plano deve declarar:

```text
parallel_group
join_condition
timeout
partial_result_policy
```

Paralelismo deve reduzir latência sem multiplicar custo indiscriminadamente.

---

# 13. Fan-out control

A Explosão Atômica pode gerar muitos candidatos.

O Orchestrator precisa limitar fan-out:

```text
max_children_per_node
max_parallel_nodes
max_related_memories
max_candidate_relations
max_active_branches
```

Uma capability pode retornar 10.000 candidatos, mas o Orchestrator pode admitir apenas os top-k elegíveis conforme policy e budget.

---

# 14. Capabilities não criam trabalho ilimitado diretamente

**DECISÃO APROVADA COMO INVARIANTE**

Uma capability pode sugerir continuidade, mas não deve abrir recursão ilimitada fora do controle de orquestração.

Em vez de:

```text
CAP_A chama CAP_B chama CAP_C chama CAP_D ...
```

preferir:

```text
CAP_A
  ↓
NextStepCandidate[]
  ↓
ORCHESTRATOR
  ↓ admission / budget / policy
  ↓
CAP_B autorizado
```

Contrato conceitual:

```text
NextStepCandidate
├── proposed_requirement
├── reason
├── expected_information_gain?
├── expected_cost?
├── expected_risk_change?
├── evidence_refs[]
├── proposed_by
└── parent_trace
```

Princípio:

> **A capability pode pedir para continuar; o Orchestrator decide se o organismo continua.**

---

# 15. Ondas da Explosão Atômica

A recursão deve ser tratada como execução em ondas controladas.

```text
WAVE 0
entrada original
   │
   ▼
WAVE 1
primeiros derivados
   │
   ▼
WAVE 2
relações / novas hipóteses
   │
   ▼
WAVE 3
counter-evidence / expansão contextual
   │
   ▼
STOP / ESCALATE / CONTINUE
```

Cada nova onda precisa passar por Admission Control.

Campos:

```text
wave_id
wave_depth
parent_wave
budget_remaining
new_information_gain
novelty
risk_delta
active_branches
stop_reason?
```

---

# 16. Stop Controller

O motor precisa de razões explícitas para parar.

Condições iniciais:

```text
OBJECTIVE_SATISFIED
QUALITY_THRESHOLD_REACHED
EVIDENCE_THRESHOLD_REACHED
MARGINAL_INFORMATION_GAIN_LOW
NOVELTY_BELOW_THRESHOLD
BUDGET_EXHAUSTED
DEADLINE_REACHED
MAX_WAVES_REACHED
MAX_DEPTH_REACHED
MAX_FANOUT_REACHED
NO_ELIGIBLE_CAPABILITY
POLICY_DENIED
RISK_EXCEEDED
DUPLICATE_LOOP_DETECTED
CONFIDENCE_PLATEAU
HUMAN_REQUIRED
```

Princípio:

> **Saber parar é uma capability estrutural do Orchestrator.**

---

# 17. Backpressure

Em escala enterprise, o sistema precisa lidar com pressão de entrada.

O Orchestrator deve cooperar com mecanismos de **backpressure**.

Possíveis ações:

```text
queue
defer
sample
reduce_fanout
use_cached_result
switch_to_cheaper_capability
shed_noncritical_work
escalate capacity
reject low-priority request
```

Nunca degradar silenciosamente requisito crítico.

---

# 18. Bulkheads

Falha de uma família de capabilities não deve derrubar o organismo inteiro.

Usar conceito de **bulkhead isolation** quando aplicável:

```text
DOMAIN A / CAPABILITY GROUP A
        X failure

DOMAIN B / CAPABILITY GROUP B
        continua operando
```

O isolamento pode ocorrer por:

```text
tenant
capability group
provider
risk class
queue
resource pool
region
```

---

# 19. Circuit Breakers

Para dependências instáveis, o sistema deve considerar **circuit breakers**.

Estados conceituais:

```text
CLOSED
  ↓ failures
OPEN
  ↓ cooldown / probe
HALF_OPEN
  ↓ success
CLOSED
```

O Health Registry alimenta a decisão.

Circuit breaker não é apenas disponibilidade; pode ser acionado por:

```text
technical failure
quality degradation
cost explosion
policy violation
provider instability
```

---

# 20. Retry não é reflexo automático

Retries precisam ser conscientes de idempotência, custo e risco.

```text
read-only deterministic task
→ retry pode ser seguro

external payment action
→ retry pode duplicar efeito
```

Cada capability deve declarar propriedades como:

```text
idempotent
side_effecting
retry_safe
max_retries
retry_backoff
```

---

# 21. Replanning

O plano inicial pode ficar inválido durante execução.

Exemplos:

```text
capability ficou UNHEALTHY
budget caiu
nova evidência eliminou uma hipótese
policy mudou
prazo ficou inviável
counter-evidence mudou o risco
```

Então o Orchestrator pode produzir uma nova versão:

```text
PLAN v1
  ↓ runtime change
PLAN v2
```

Toda replanejamento relevante deve registrar:

```text
old_plan_id
new_plan_id
reason
changed_nodes[]
changed_budget
changed_risk
trace_id
```

---

# 22. Escalation Manager

Escalonar não é simplesmente “chamar IA”.

Possíveis destinos:

```text
specialist capability
more expensive local model
external AI
multi-agent review
human authority
manual investigation
fail closed
```

Contrato conceitual:

```text
EscalationRequest
├── reason
├── unresolved_requirement
├── attempted_capabilities[]
├── evidence_refs[]
├── uncertainty
├── risk
├── budget_remaining
├── deadline_remaining
├── recommended_authority
└── trace_id
```

---

# 23. Supervisory AI como capability de alto nível

A IA supervisora fica **acima da malha mecânica**, não embutida em cada etapa.

```text
NORMAL EXECUTION
      │
      ▼
mechanical / deterministic / statistical fabric
      │
      ├── objective satisfied → RESULT
      │
      └── unresolved / conflict / high risk
                         │
                         ▼
                  ESCALATION MANAGER
                         │
                         ▼
                    SUPERVISORY AI
                         │
                         ▼
                  evaluator / policy
```

A saída da IA supervisora continua sendo Artifact/Evidence Candidate, não verdade automática.

---

# 24. Human Authority

Humano é uma autoridade legítima do grafo de orquestração.

Não deve aparecer apenas como “último recurso”.

Policy pode exigir humano diretamente em:

```text
high consequence
irreversible action
regulated process
insufficient evidence
novel out-of-distribution event
conflicting authority
legal/compliance requirement
```

O resultado humano também precisa de provenance e trace quando entra no sistema.

---

# 25. Orchestrator Health

O Orchestrator também pode falhar.

Portanto ele precisa de health próprio.

Métricas candidatas:

```text
planning_latency
plan_failure_rate
unnecessary_fanout_rate
budget_overrun_rate
fallback_rate
replan_rate
ai_escalation_rate
human_escalation_rate
stop_reason_distribution
orphan_node_rate
loop_detection_rate
policy_denial_rate
quality_per_cost
```

Um supervisor não deve presumir que o Maestro está sempre certo.

---

# 26. Meta-Orchestration

Em escala maior, o sistema pode avaliar a qualidade da própria orquestração.

Exemplo:

```text
ROUTING POLICY A
quality = 0.97
cost = 1.00

ROUTING POLICY B
quality = 0.971
cost = 4.80

→ A pode ser preferível em determinado risco
```

Isso cria candidatos de aprendizagem sobre:

```text
routing weights
capability preferences
budget allocation
stop thresholds
fallback ordering
parallelization strategy
```

Essas mudanças continuam entrando no **Learning Quarantine**.

O Orchestrator não deve reescrever silenciosamente sua própria política de roteamento em produção.

---

# 27. Orchestrator não deve virar gargalo central

Direções de engenharia:

```text
stateless orchestration workers quando possível
partitioning por tenant/scope
subplans independentes
queues/workers especializados
registry caches controlados
idempotent scheduling
event-driven state transitions
horizontal scaling
```

O estado durável do plano deve estar em storage/event log apropriado, não na memória de um único processo.

O monólito modular inicial pode implementar tudo no mesmo deploy sem perder essas fronteiras lógicas.

---

# 28. Exemplo B2B enterprise

Problema:

```text
“Reconstruir por que uma cadeia de entregas atrasou e indicar quais hipóteses merecem investigação.”
```

Fluxo possível:

```text
ROOT REQUIREMENT
      │
      ▼
SCHEMA + SCOPE VALIDATION
      │
      ▼
REGISTRY QUERY
      │
      ├── entity resolution
      ├── temporal reconstruction
      ├── event correlation
      ├── anomaly detection
      └── evidence assembly
      │
      ▼
ORCHESTRATION PLAN
      │
      ├── parallel: entity + time + retrieval
      │
      └── join
             │
             ▼
         hypotheses
             │
             ▼
         challenger
             │
       ┌─────┴─────┐
       ▼           ▼
   sufficient   conflict
   evidence        │
       │           ▼
       │      supervisory AI?
       │           │
       └─────┬─────┘
             ▼
          RESULT
             │
             └──► learning candidates → quarantine
```

O plano, capabilities, custo e razões de escalonamento ficam no trace.

---

# 29. Invariantes v0.1

**DECISÃO APROVADA COMO BASE PARA TESTE**

1. O Orchestrator coordena capabilities por contrato, não por acoplamento a implementações específicas.
2. Control Plane e Execution Plane permanecem conceitualmente separados.
3. Toda execução possui Processing Context e budget explícito.
4. Capabilities não podem criar recursão ilimitada diretamente.
5. Continuação recursiva entra como `NextStepCandidate` e passa por Admission Control.
6. Hard constraints filtram antes de ranking econômico/qualitativo.
7. Fallback, retry, parallelism e escalation são decisões rastreáveis.
8. Alto risco pode exigir IA/humano sem percorrer toda a escada de mecanismos baratos.
9. Orchestration Plans relevantes são versionáveis e replanejamentos preservam lineage.
10. Toda onda da Explosão Atômica precisa de budget e condição de parada.
11. Orchestrator também possui health e métricas próprias.
12. Políticas de roteamento aprendidas entram em Learning Quarantine antes de promoção.
13. Falha ou ausência de capability crítica não pode ser mascarada por improvisação silenciosa.
14. O Orchestrator deve poder escalar horizontalmente sem concentrar estado crítico em um único processo.
15. A decisão de parar precisa ser explícita e registrada.

---

# 30. Questões em aberto

- formato físico do Work Graph;
- algoritmo inicial de ranking de capabilities;
- política exata de budget allocation;
- regra inicial de reserve budget;
- definição de `expected_information_gain`;
- scheduler inicial;
- tecnologia de queue/work execution;
- granularidade dos subplans;
- limites iniciais de fan-out e parallelism;
- circuit breaker thresholds;
- backpressure policy;
- timeout defaults;
- retry matrix por mechanism class;
- estratégia de distributed locks/leases se necessária;
- persistence model de plans;
- política de prioridade entre tenants;
- critérios de escalonamento para Supervisory AI;
- critérios de escalonamento humano;
- métricas mínimas para Orchestrator Health;
- política de replanejamento automático.

---

# 31. Frases de fundação

> **O Orchestrator não precisa saber fazer o trabalho. Precisa saber descobrir quem pode fazê-lo, autorizar a execução, medir o resultado e interromper a cadeia quando continuar deixa de valer a pena.**

> **A capability pode pedir para continuar; o Orchestrator decide se o organismo continua.**

> **Delegar trabalho não significa delegar autoridade ilimitada.**

> **Um bom Maestro não toca todos os instrumentos; ele impede que a orquestra vire barulho.**
