# Eva Engine® — Executable Architecture Spec v0.1

**Status:** especificação de implementação inicial  
**Função:** converter o Blueprint enterprise em um primeiro coração executável pequeno, testável e fiel à arquitetura, sem reduzir o projeto a notas, chatbot ou wrapper de IA.

---

# 1. Objetivo

A primeira implementação não precisa provar toda a inteligência do Eva Engine®.

Ela precisa provar que o **organismo básico consegue bater com integridade**.

Primeiro heartbeat:

```text
EVENT
  ↓
INGRESS VALIDATION
  ↓
COGNITIVE ENVELOPE
  ↓
SCOPE / POLICY
  ↓
CAPABILITY DISCOVERY
  ↓
ORCHESTRATION PLAN
  ↓
DETERMINISTIC CAPABILITY
  ↓
COGNITIVE ARTIFACT
  ↓
EVIDENCE / TRACE
  ↓
RESULT
  ↓
OBSERVABILITY
```

Sem:

```text
LLM obrigatório
embeddings obrigatórios
notas como abstração central
microserviços
aprendizado global
UI
agentes autônomos
```

---

# 2. O que esta v0.1 precisa provar

A execução mínima precisa demonstrar:

1. um evento genérico entra por contrato;
2. tenant/scope acompanha o fluxo;
3. RAW é preservado;
4. um Cognitive Envelope é criado;
5. Schema Registry valida estrutura;
6. Capability Registry descobre capability compatível;
7. Health Registry confirma aptidão;
8. Orchestrator cria plano explícito;
9. capability determinística executa;
10. saída vira Cognitive Artifact;
11. lineage aponta para o evento raiz;
12. trace registra caminho, versões e custo;
13. Policy pode negar um caminho;
14. retry idempotente não duplica resultado;
15. falha conhecida gera estado explícito;
16. nenhum Learning Candidate altera Trusted State.

---

# 3. O que esta v0.1 NÃO precisa provar

Não incluir como requisito de conclusão:

- semântica profunda;
- classificação universal de texto;
- atomização completa;
- 32 lentes;
- LLM supervisionando;
- embeddings;
- graph database dedicado;
- aprendizagem contínua plena;
- Promotion Gate físico enterprise;
- multi-region;
- milhares de capabilities;
- ROI B2B;
- domínio empresarial real.

Princípio:

> **A v0.1 prova o esqueleto. As capabilities futuras provarão músculos específicos.**

---

# 4. Arquitetura de código

Direção: **monólito modular TypeScript**.

Estrutura sugerida para o repositório executável:

```text
eva-engine/
├── apps/
│   ├── api/
│   └── worker/
│
├── packages/
│   ├── kernel/
│   ├── contracts/
│   ├── schemas/
│   ├── events/
│   ├── envelope/
│   ├── registry/
│   ├── orchestration/
│   ├── capabilities/
│   ├── evidence/
│   ├── policy/
│   ├── integrity/
│   ├── evaluation/
│   ├── observability/
│   ├── learning-quarantine/
│   ├── integrations/
│   └── testing/
│
├── domain-packs/
│   └── README.md
│
├── datasets/
│   ├── golden/
│   ├── adversarial/
│   └── regression/
│
├── migrations/
├── docs/
├── package.json
├── tsconfig.json
└── README.md
```

Esse desenho é lógico; monorepo tool específica ainda é decisão de implementação.

---

# 5. Fronteiras de pacote

## `packages/kernel`

Conhece apenas contratos universais:

```text
identity
scope
state transitions
lineage
policy invocation
capability invocation
budgets
trace
version/integrity
```

Não conhece linguagem, domínio, provider ou produto.

## `packages/contracts`

Tipos compartilhados e estáveis:

```text
KernelEnvelope
CognitiveEnvelope
Event
CognitiveArtifact
CapabilityInvocation
CapabilityResult
TaskRequirement
OrchestrationPlan
EvidenceItem
PolicyDecision
ProcessingTrace
```

## `packages/schemas`

Runtime validation + schema versions.

## `packages/registry`

Interfaces e implementação inicial in-memory para:

```text
SchemaRegistry
CapabilityRegistry
HealthRegistry
```

Persistência posterior.

## `packages/orchestration`

Planner, Admission Control, budget, dispatch, stop reason.

## `packages/capabilities`

Capabilities concretas iniciais.

## `packages/evidence`

Evidence Item, eligibility e lineage de suporte.

## `packages/policy`

Policy gates determinísticos iniciais.

## `packages/integrity`

Validation failures, integrity states, quarantine decisions.

## `packages/evaluation`

Evaluator contracts e primeiros regression gates.

## `packages/observability`

Structured traces, metrics e cognitive cost.

## `packages/learning-quarantine`

Somente contratos/state machine inicial; sem aprendizado autônomo na v0.1.

---

# 6. Primeiro evento canônico

Não usar `content.created` como único caso.

Evento genérico de teste:

```json
{
  "event_id": "evt_001",
  "event_type": "system.observation",
  "schema_version": "1.0",
  "source": "fixture",
  "tenant_id": "tenant_test_a",
  "occurred_at": "2026-08-10T12:00:00Z",
  "correlation_id": "cor_001",
  "causation_id": null,
  "payload": {
    "subject": "resource-17",
    "metric": "latency_ms",
    "value": 842,
    "unit": "ms"
  }
}
```

O tipo é fixture de engenharia, não contrato final universal de domínio.

---

# 7. Primeira capability determinística

Capability de prova:

```text
CAP_STRUCTURED_OBSERVATION_EXTRACT
```

Objetivo:

Extrair fatos explicitamente declarados de um payload já estruturado, sem inferência semântica.

Entrada:

```text
EventEnvelope@1
```

Saída:

```text
StructuredObservation@1
```

Exemplo:

```text
subject = resource-17
metric = latency_ms
value = 842
unit = ms
occurred_at = ...
```

Epistemic level:

```text
DERIVED
```

Confidence probabilística:

```text
não necessária
```

Porque a capability apenas transforma campos válidos de schema.

---

# 8. Segunda capability opcional da v0.1

```text
CAP_THRESHOLD_COMPARE
```

Recebe uma observação numérica e threshold explicitamente configurado.

```text
842ms > 500ms
```

Produz:

```text
Signal
threshold_exceeded = true
```

Isso prova composição sem IA.

Não afirmar causa, gravidade empresarial ou anomalia estatística.

---

# 9. Capability Descriptor inicial

```text
CapabilityDescriptor
├── capability_id
├── version
├── input_schema
├── output_schema
├── mechanism_class
├── risk_class
├── cost_class
├── latency_class
├── status
├── policy_tags[]
├── evaluator_id
└── health_probe_id
```

Implementação in-memory é suficiente na v0.1.

---

# 10. Health inicial

HealthSnapshot mínimo:

```text
capability_id
version
technical_status
cognitive_status
economic_status
last_checked_at
reason?
```

Para capability determinística inicial:

```text
technical = HEALTHY
cognitive = HEALTHY quando regression suite passa
economic = HEALTHY quando budget local definido não é excedido
```

---

# 11. Orchestration v0.1

Sem planner de IA.

Planejamento inicial pode ser determinístico baseado em requirement + registry.

```text
TaskRequirement
      ↓
Registry query
      ↓
Hard constraints
      ↓
Candidate list
      ↓
Deterministic rank
      ↓
OrchestrationPlan
      ↓
Dispatch
```

Primeiro Work Graph:

```text
EVENT
  ↓
CAP_STRUCTURED_OBSERVATION_EXTRACT
  ↓
CAP_THRESHOLD_COMPARE? [if configured]
  ↓
RESULT
```

---

# 12. Admission Control v0.1

Antes de cada node:

```text
schema valid?
tenant/scope valid?
policy allow?
capability healthy?
budget remaining?
max nodes not exceeded?
```

Falhou hard constraint:

```text
do not execute
```

Registrar reason.

---

# 13. Budget v0.1

Mesmo sem API paga, orçamento existe.

```text
ProcessingBudget
├── max_nodes
├── max_duration_ms
├── max_external_cost
└── max_waves
```

Defaults de teste podem ser baixos.

Custo externo inicial esperado:

```text
0
```

---

# 14. Stop Reasons

Primeiros valores:

```text
OBJECTIVE_SATISFIED
NO_ELIGIBLE_CAPABILITY
POLICY_DENIED
BUDGET_EXHAUSTED
HEALTH_BLOCKED
SCHEMA_INVALID
ERROR
```

Stop reason obrigatório no ProcessingTrace.

---

# 15. Cognitive Envelope v1.0 na implementação

Core mínimo do envelope:

```text
object_id
object_type
root_event_id
parent_id?
tenant_id
scope_id
schema_id
schema_version
epistemic_level
trust_state
integrity_state
engine_version
created_at
trace_id
payload_ref / payload
```

Extended metadata por referência.

Não duplicar todos os traces/evidence no objeto.

---

# 16. Estados iniciais

Epistemic:

```text
RAW
DERIVED
INFERRED
LEARNED
```

Trust:

```text
UNVERIFIED
CANDIDATE
PROMOTED
SUPERSEDED
REVOKED
```

Integrity:

```text
CLEAN
SUSPECT
QUARANTINED
TAINTED
INVALIDATED
REQUIRES_RECOMPUTE
```

A v0.1 usará subconjunto necessário, mas enums devem preservar separação.

---

# 17. Policy v0.1

Policies determinísticas iniciais:

```text
P001 tenant_id required
P002 external cost must not exceed budget
P003 capability must be ACTIVE/allowed
P004 tenant scope must match artifact scope
P005 Learning Candidate cannot write trusted state
```

Sem policy DSL sofisticada inicialmente.

---

# 18. Persistence v0.1

PostgreSQL continua direção aprovada, mas a primeira bateria unitária pode usar repository in-memory.

Persistência mínima quando banco entrar:

```text
events
raw_objects
cognitive_artifacts
lineage_edges
processing_traces
capability_descriptors
health_snapshots
policy_decisions
```

Learning Candidates podem ficar em tabela separada já na primeira migration que os introduzir.

---

# 19. Repository Interfaces

Definir interfaces antes do provider físico:

```text
EventRepository
ArtifactRepository
LineageRepository
TraceRepository
RegistryRepository
LearningCandidateRepository
```

O Core não importa cliente Supabase diretamente.

---

# 20. API v0.1

Endpoint inicial:

```text
POST /v1/events
```

Resposta:

```text
202/200
trace_id
root_event_id
status
result_refs[]
stop_reason
```

Endpoint de debug local/test:

```text
GET /v1/traces/:trace_id
```

Não expor debug cru em produção sem policy.

---

# 21. Processing Trace mínimo

```text
ProcessingTrace
├── trace_id
├── root_event_id
├── tenant_id
├── started_at
├── finished_at
├── plan_id
├── invocations[]
├── policy_decisions[]
├── artifacts_created[]
├── stop_reason
├── duration_ms
├── external_cost
└── engine_version
```

---

# 22. Observability v0.1

Logs estruturados em JSON.

Nunca logar payload completo por default.

Métricas:

```text
events_processed_total
processing_duration_ms
capability_invocations_total
capability_errors_total
policy_denials_total
budget_stops_total
external_cost_total
artifacts_created_total
```

---

# 23. Cognitive Economics v0.1

Registrar:

```text
external_cost = 0
compute_duration
capability_count
wave_count
```

Não inventar CCU calibrada ainda.

CCU permanece hipótese até termos método mensurável.

---

# 24. Integrity v0.1

Casos obrigatórios:

```text
invalid schema
missing tenant
scope mismatch
unknown capability
unhealthy capability
duplicate event
policy denied
capability exception
budget exhausted
```

Cada caso produz estado/erro rastreável, não silent failure.

---

# 25. Learning Quarantine v0.1

A primeira implementação precisa provar somente a fronteira.

Teste:

```text
create LearningCandidate
      ↓
attempt direct trusted-state write
      ↓
DENIED
```

Não implementar auto-learning ainda.

---

# 26. Test Suites obrigatórias antes de qualquer demo

## Unit

- envelope validation;
- state transition;
- registry lookup;
- health filter;
- policy decision;
- budget accounting;
- stop reason.

## Integration

- event → result;
- duplicate event;
- scope mismatch;
- capability failure;
- Learning Candidate isolation.

## Golden

Mesmo fixture + mesma versão → mesmos deterministic artifacts.

## Fault Injection

- capability throws;
- registry unavailable;
- trace repository fails;
- health becomes UNHEALTHY mid-plan.

---

# 27. Invariantes executáveis

Transformar em testes:

```text
I01 RAW never overwritten
I02 tenant scope never silently changes
I03 artifact always has root_event_id
I04 derived artifact has parent/lineage
I05 invalid schema never reaches capability
I06 unhealthy critical capability is not silently used
I07 policy denial cannot be bypassed by executor
I08 budget cannot go negative silently
I09 duplicate event does not duplicate deterministic artifacts
I10 Learning Candidate cannot write Trusted State
I11 stop reason exists
I12 trace reconstructs executed path
I13 external cost starts at zero without external provider
I14 result version vector is available
```

---

# 28. Primeiro benchmark

Não medir “inteligência” ainda.

Medir:

```text
correctness of invariants
reproducibility
latency
memory
throughput
trace completeness
idempotency
failure containment
```

Checkpoints de volume sintético:

```text
1k
10k
100k events
```

Somente aumentar após validar gerador e workload.

---

# 29. Primeira demo interna

A demo deve mostrar arquitetura, não espetáculo.

```text
1. enviar evento
2. ver envelope
3. ver capability escolhida
4. ver artifact derivado
5. ver evidence/trace
6. repetir evento e provar idempotência
7. quebrar capability e ver containment
8. tentar cruzar tenant e ver bloqueio
9. tentar Learning Candidate → Trusted State e ver negação
10. mostrar external_cost = 0
```

Essa demo comprova o esqueleto do organismo.

---

# 30. Onde entra o Cursor

O Cursor deve implementar por fatias pequenas e verificáveis.

Ordem:

```text
STEP 1 contracts + schemas
STEP 2 envelope + state machines
STEP 3 in-memory registries
STEP 4 policy + budget
STEP 5 deterministic capability
STEP 6 orchestrator + trace
STEP 7 integrity/failures
STEP 8 API
STEP 9 persistence adapter
STEP 10 CI + benchmark
```

Cada step:

```text
spec
→ tests
→ implementation
→ typecheck
→ test
→ review
```

---

# 31. Primeira tarefa para o Cursor

Criar somente o foundation skeleton:

```text
packages/contracts
packages/schemas
packages/envelope
```

Entregáveis:

- TypeScript project foundation;
- core enums;
- Event schema;
- CognitiveEnvelope schema;
- CognitiveArtifact schema;
- runtime validation;
- unit tests;
- no database;
- no HTTP;
- no LLM;
- no domain code.

Critério de aceitação:

```text
npm/pnpm test passes
npm/pnpm typecheck passes
invalid envelopes fail validation
valid fixtures round-trip without mutation
```

---

# 32. Repositório de implementação

**HIPÓTESE FORTE:** manter código executável em repositório privado separado do repositório `infra`, preservando `infra` como fonte arquitetural e de P&D.

Nome sugerido:

```text
eva-core-360/engine
```

ou equivalente aprovado.

Motivos:

- reduzir mistura entre Blueprint e runtime;
- permissões/CI diferentes;
- releases de código independentes;
- evitar que experimentos de implementação poluam documentação canônica;
- permitir que `infra` permaneça mapa de longo prazo.

Essa decisão precisa ser confirmada antes do primeiro commit de código.

---

# 33. Definition of Done — Heartbeat v0.1

A primeira fase está concluída quando:

```text
✓ evento genérico processado end-to-end
✓ envelope válido
✓ scope preservado
✓ capability descoberta por registry
✓ orchestration plan explícito
✓ deterministic artifact gerado
✓ lineage reconstruível
✓ policy enforcement
✓ budget enforcement
✓ idempotência
✓ trace completo
✓ falhas contidas
✓ learning boundary testada
✓ external cost = 0 na baseline
✓ testes automatizados
✓ CI verde
```

Só depois começam capabilities cognitivas mais sofisticadas.

---

# 34. Frases de fundação

> **O primeiro coração não precisa pensar muito. Precisa bater certo.**

> **Antes de provar inteligência, vamos provar identidade, circulação, integridade, autoridade e memória do caminho percorrido.**
