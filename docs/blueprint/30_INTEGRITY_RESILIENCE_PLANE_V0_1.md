# Eva Engine® — Integrity & Resilience Plane v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** transformar a metáfora do “sistema imunológico” do Eva Engine® em mecanismos operacionais de detecção, contenção, degradação controlada, quarentena, propagação de integridade, recuperação, verificação e supervisão.

---

# 1. Definição

O **Integrity & Resilience Plane** é a camada transversal responsável por impedir que falhas locais se transformem silenciosamente em falhas sistêmicas.

Ele observa:

```text
entrada
envelopes
capabilities
orquestração
modelos
agentes
registries
learning quarantine
storage
integrações
outputs
```

Princípio:

> **O organismo pode tolerar falhas de peças; não pode tolerar perda silenciosa de integridade.**

---

# 2. Resiliência não significa “nunca falhar”

Nenhum sistema enterprise real é infalível.

A meta é:

```text
DETECTAR CEDO
      ↓
CONTER LOCALMENTE
      ↓
EVITAR PROPAGAÇÃO
      ↓
CONTINUAR QUANDO SEGURO
      ↓
DEGRADAR QUANDO NECESSÁRIO
      ↓
RECUPERAR
      ↓
VERIFICAR
      ↓
APRENDER COM O INCIDENTE
```

Resiliência é capacidade de manter função útil e recuperar estado confiável sob falhas conhecidas ou inesperadas.

---

# 3. Integrity Plane é transversal

```text
┌───────────────────────────────────────────────────────────────────────┐
│                    INTEGRITY & RESILIENCE PLANE                      │
│                                                                       │
│ detect · classify · contain · quarantine · recover · verify · alert  │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │                    TRUSTED COGNITIVE FABRIC                    │ │
│  │                                                                 │ │
│  │ Kernel → Orchestrator → Registries → Execution → Evidence      │ │
│  │                  → Result → Derivatives → New Wave             │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                                                                       │
│ health · watchdogs · taint · blast radius · circuit breakers        │
└───────────────────────────────────────────────────────────────────────┘
```

O Plane não substitui cada componente.

Ele cria supervisão independente sobre o conjunto.

---

# 4. Classes de falha

O sistema deve distinguir pelo menos:

```text
DATA FAULT
schema inválido
corrupção
duplicata enganosa
fonte inconsistente
poisoning

CAPABILITY FAULT
crash
timeout
latência extrema
resultado degradado
drift

ORCHESTRATION FAULT
loop
fan-out excessivo
budget leak
stuck plan
scheduler failure

POLICY FAULT
policy ausente
configuração inválida
policy conflitante
bypass detectado

DEPENDENCY FAULT
API externa indisponível
banco degradado
fila indisponível
modelo externo falhando

SECURITY / ADVERSARIAL FAULT
prompt injection
data poisoning
credential misuse
tenant boundary violation
unexpected external call

COGNITIVE QUALITY FAULT
false positives acima do baseline
confidence descalibrada
evidence echo
relation explosion
semantic drift

LEARNING FAULT
candidate contaminado
promotion incorreta
overfitting
feedback fraudulento
```

Classificar a falha é necessário porque cada classe possui resposta diferente.

---

# 5. Failure Severity

Escala conceitual inicial:

```text
S0 — INFO
nenhuma degradação; apenas observação

S1 — MINOR
degradação pequena, sem risco relevante

S2 — DEGRADED
qualidade/latência/custo fora do esperado; fallback possível

S3 — MAJOR
capability/fluxo crítico afetado; contenção necessária

S4 — CRITICAL
integridade, segurança, tenant isolation ou decisão crítica em risco

S5 — SYSTEMIC
propagação ampla ou confiança no estado global comprometida
```

A taxonomia final será calibrada por domínio e operação.

---

# 6. Detecção em múltiplas camadas

Não existe um único “antivírus”.

Detecção é composta:

```text
INGRESS DETECTORS
schema · auth · provenance · anomaly · duplication

RUNTIME WATCHDOGS
availability · latency · errors · resource usage

COGNITIVE WATCHDOGS
quality · drift · calibration · evidence echo · relation explosion

ECONOMIC WATCHDOGS
cost spike · AI escalation spike · low value-per-cost

POLICY WATCHDOGS
bypass · missing authorization · scope mismatch

LEARNING WATCHDOGS
promotion anomaly · distribution drift · holdout regression
```

Princípio:

> **Quem executa não deve ser o único responsável por declarar que executou corretamente.**

---

# 7. Watchdog independence

Um watchdog precisa ser suficientemente independente da peça observada.

Exemplo ruim:

```text
CAP_X executa
CAP_X calcula a própria qualidade
CAP_X declara HEALTHY
```

Preferível:

```text
CAP_X executa
   │
   ├── metrics
   ├── samples
   └── outputs
         │
         ▼
INDEPENDENT EVALUATOR / WATCHDOG
         │
         ▼
Health Registry
```

Não significa processo físico separado em v0, mas a responsabilidade lógica deve ser separada.

---

# 8. Health Signals

O Health Registry recebe sinais como:

```text
availability
error_rate
latency_p50/p95/p99
timeout_rate
retry_rate
quality_delta
false_positive_rate
false_negative_rate
calibration_error
drift_score
cost_per_call
ai_escalation_rate
fallback_rate
circuit_open_rate
```

Health não é apenas uptime.

Uma capability pode estar online e cognitivamente imprópria para uso.

---

# 9. Fault Containment Zones

**DECISÃO APROVADA COMO PRINCÍPIO**

O organismo deve possuir **fault containment zones** / zonas de contenção para impedir propagação horizontal.

Exemplos:

```text
tenant boundary
domain boundary
capability group
provider group
learning quarantine
external AI boundary
high-risk action boundary
```

Quando possível, falha em uma zona não deve consumir recursos ou contaminar estado de outras zonas.

---

# 10. Bulkheads

Aplicar o padrão **bulkhead** quando apropriado:

```text
POOL A — deterministic workers
POOL B — model workers
POOL C — external AI calls
POOL D — learning jobs
POOL E — high-risk review
```

Se C saturar, A não deve necessariamente parar.

O desenho físico depende da escala; o princípio nasce no Blueprint.

---

# 11. Circuit Breaker

Capabilities/dependências instáveis podem ser protegidas por circuit breaker:

```text
CLOSED
  │ falhas acima do limite
  ▼
OPEN
  │ cooldown
  ▼
HALF_OPEN
  │ probes controlados
  ├── sucesso → CLOSED
  └── falha   → OPEN
```

A abertura precisa aparecer no Health Registry e no trace do Orchestrator.

---

# 12. Degradação controlada

Nem toda falha exige desligar tudo.

Possíveis modos:

```text
FULL
normal

DEGRADED
capabilities secundárias reduzidas

SAFE_MODE
somente capacidades determinísticas/promovidas de baixo risco

READ_ONLY
nenhuma mutação de estado crítico

QUARANTINE_ONLY
entrada aceita, mas não promovida/propagada

FAIL_CLOSED
operação crítica recusada
```

Policy decide quais modos são válidos por contexto.

---

# 13. Fail-open versus Fail-closed

A escolha depende do risco.

```text
LOW RISK
pode aceitar fallback ou resposta parcial

HIGH RISK
pode exigir fail-closed
```

Exemplo:

```text
“sugerir documentos relacionados”
```

pode tolerar degradação maior que:

```text
“autorizar pagamento de alto valor”
```

Nenhuma regra universal `sempre fail-closed` ou `sempre fail-open` deve ser aplicada.

---

# 14. Integrity State propagation

O Cognitive Envelope define:

```text
CLEAN
SUSPECT
QUARANTINED
TAINTED
INVALIDATED
REQUIRES_RECOMPUTE
```

Quando um ancestral muda de integridade:

```text
SOURCE S
   ↓
ARTIFACT A
   ↓
RELATION R
   ↓
CLAIM C
   ↓
DECISION D
```

se `A = TAINTED`, o sistema precisa avaliar R, C e D.

Princípio:

> **Taint propagation é avaliação orientada por lineage, não apagamento cego de toda a árvore.**

---

# 15. Taint rules por tipo de lineage

Nem toda relação transmite contaminação da mesma forma.

Exemplos conceituais:

```text
DERIVED_FROM
forte propagação

INFERRED_FROM
forte propagação para reavaliação

SUPPORTED_BY
pode reduzir suporte sem invalidar claim inteira

GENERATED_BY
pode invalidar saída se produtor estava comprometido

RELATED_TO
não implica propagação automática
```

A matriz final de propagação é questão em aberto e deve ser testada.

---

# 16. Blast Radius

**Blast Radius** responde:

> quais objetos, decisões, tenants, capabilities ou resultados podem ter sido afetados?

Fluxo:

```text
FAULT ROOT
    │
    ▼
LINEAGE / DEPENDENCY GRAPH
    │
    ├── descendants
    ├── dependent capabilities
    ├── affected claims
    ├── promoted learning
    ├── outputs/actions
    └── tenants/scopes
    │
    ▼
IMPACT SET
```

O sistema precisa distinguir blast radius potencial de confirmado.

---

# 17. Incident Record

Todo incidente relevante deve possuir registro próprio.

```text
IntegrityIncident
├── incident_id
├── detected_at
├── detected_by
├── severity
├── fault_class
├── root_object_ref?
├── affected_scope
├── suspected_components[]
├── blast_radius_estimate
├── containment_actions[]
├── recovery_actions[]
├── verification_results[]
├── status
├── owner / authority?
└── trace_refs[]
```

Estados possíveis:

```text
DETECTED
TRIAGED
CONTAINING
CONTAINED
RECOVERING
VERIFYING
RESOLVED
POSTMORTEM
```

---

# 18. Containment Protocol

Fluxo padrão:

```text
DETECT
  ↓
CLASSIFY
  ↓
ASSESS RISK
  ↓
ISOLATE
  ↓
STOP PROPAGATION
  ↓
QUARANTINE SUSPECT ARTIFACTS
  ↓
CALCULATE BLAST RADIUS
  ↓
CHOOSE RECOVERY STRATEGY
```

A prioridade inicial é impedir piora.

Não é explicar tudo antes de conter.

---

# 19. Recovery Strategies

Possíveis estratégias:

```text
RETRY
quando operação é segura/idempotente

FALLBACK
usar capability alternativa validada

REPLAY
reexecutar evento com versão/estado conhecido

RECOMPUTE
regenerar derivados a partir de ancestral limpo

ROLLBACK
retornar versão/configuração promovida anterior

REVOKE
retirar autoridade de artefato/regra/modelo

SUPERSEDE
substituir por versão corrigida preservando histórico

RESTORE
recuperar estado persistente conhecido

HUMAN_REVIEW
quando risco/ambiguidade excedem autonomia permitida
```

---

# 20. Recovery nunca termina no “parece que voltou”

Toda recuperação precisa de **Verification Gate**.

```text
RECOVERY ACTION
      │
      ▼
REPLAY / TEST
      │
      ▼
COMPARE TO BASELINE
      │
      ▼
HEALTH CHECK
      │
      ▼
INTEGRITY CHECK
      │
      ├── PASS → RESTORE SERVICE
      └── FAIL → REMAIN CONTAINED / ESCALATE
```

Princípio:

> **Recuperação não é sucesso até que o sistema prove que voltou a operar dentro dos limites esperados.**

---

# 21. Supervisor do Supervisor

O Orchestrator e os próprios watchdogs também podem falhar.

Por isso o sistema deve prever supervisão sobre o Control Plane:

```text
ORCHESTRATOR
   ↓ observed by
CONTROL-PLANE WATCHDOG

HEALTH REGISTRY
   ↓ observed by
REGISTRY CONSISTENCY WATCHDOG

WATCHDOGS
   ↓ observed by
WATCHDOG HEARTBEAT / COVERAGE CHECK
```

Pergunta operacional:

```text
“quem está verificando se o verificador ainda existe?”
```

Não precisa virar regressão infinita.

A arquitetura define camadas críticas com sinais independentes e alarmes externos quando necessário.

---

# 22. Missing Supervisor Detection

O organismo precisa detectar ausência de função de supervisão esperada.

Exemplo:

```text
CAP_CRITICAL_X active
  ↓ requires
WATCHDOG_QUALITY_X

WATCHDOG_QUALITY_X missing/stale
  ↓
COVERAGE_GAP
  ↓
restrict / alert / fail-closed depending on risk
```

Princípio:

> **Ausência de monitoramento crítico é um estado de health, não um detalhe operacional.**

---

# 23. Resilience Budget

Resiliência também consome recursos.

O Orchestrator pode reservar capacidade para:

```text
retries
fallbacks
recovery
health probes
verification
emergency escalation
```

Sem reserva, um sistema no limite pode não ter recursos justamente para se recuperar.

Nome conceitual:

**Resilience Reserve / Recovery Budget**.

---

# 24. Backpressure

Quando a entrada excede capacidade segura:

```text
INGRESS RATE ↑
    │
    ▼
QUEUE PRESSURE ↑
    │
    ▼
BACKPRESSURE
    │
    ├── slow producers
    ├── defer non-critical work
    ├── reduce fan-out
    ├── disable optional lenses
    └── protect critical flows
```

A resposta não deve ser simplesmente “aceitar tudo e quebrar depois”.

---

# 25. Load Shedding

Em saturação, o sistema pode descartar/deferir trabalho não crítico conforme policy.

Exemplo:

```text
P0 critical
P1 high
P2 normal
P3 opportunistic
```

Sob pressão:

```text
P3 → defer
P2 → reduce optional branches
P1 → preserve
P0 → reserve capacity
```

Nunca descartar silenciosamente artefatos que policy exige preservar.

---

# 26. Resilience e External AI

Providers externos podem falhar ou degradar.

O sistema deve observar:

```text
availability
latency
cost spikes
rate limits
model/version changes
quality regression
policy compatibility
```

Fallback possível:

```text
external model A
    ↓ failure
local model B
    ↓ insufficient
human authority
```

Cada fallback registra perda esperada de qualidade/custo/latência.

---

# 27. Resilience e Learning Quarantine

Falha em aprendizado é tratada com isolamento mais forte.

Se candidato foi promovido e depois considerado nocivo:

```text
PROMOTED CHANGE
      │
      ▼
INCIDENT
      │
      ▼
REVOKE / ROLLBACK
      │
      ▼
FIND DEPENDENT ARTIFACTS
      │
      ▼
RECOMPUTE / REEVALUATE
      │
      ▼
VERIFY
```

O Learning Quarantine continua separado do Trusted Core durante recuperação.

---

# 28. Resilience e Evidence Model

Uma fonte revogada pode alterar claims existentes.

```text
EVIDENCE E4 = REVOKED
       │
       ▼
CLAIMS DEPENDENTES
       │
       ├── still supported by independent evidence
       └── insufficient support → CHALLENGED / REQUIRES_RECOMPUTE
```

O Integrity Plane não decide sozinho a verdade da claim.

Ele dispara reavaliação no Evidence Model.

---

# 29. Resilience e multi-tenant

Falha em um tenant deve permanecer isolada quando possível.

```text
TENANT A poisoning attempt
        │
        ▼
contain A scope
        │
        X
        │ no propagation
        ▼
TENANT B
```

Cross-tenant contamination é incidente crítico.

O Envelope e os boundaries de storage/policy precisam impedir que o grafo cognitivo atravesse escopo sem autorização.

---

# 30. Fault Injection

O sistema não deve esperar produção para descobrir que recuperação não funciona.

Testes futuros incluem:

```text
kill capability worker
inject latency
return corrupted payload
break schema compatibility
revoke evidence source
simulate provider outage
inject duplicate events
exhaust cost budget
open circuit breaker
simulate watchdog failure
simulate stale health data
poison learning candidate
force tenant-scope mismatch
```

Objetivo:

> **testar não apenas se o motor funciona, mas se sabe falhar.**

---

# 31. Chaos Engineering — uso controlado

Chaos Engineering pode ser útil em estágios maduros.

Não significa quebrar produção aleatoriamente.

Significa introduzir falhas controladas, com hipóteses e limites, para verificar resiliência.

Na fase atual, começar com fault injection em testes e ambientes isolados.

---

# 32. SLOs de integridade e recuperação

Métricas futuras podem incluir:

```text
MTTD — mean time to detect
MTTC — mean time to contain
MTTR — mean time to recover
false alarm rate
blast radius size
recompute success rate
rollback success rate
watchdog coverage
stale health rate
integrity incident rate
```

Os SLOs finais dependem do domínio e risco.

---

# 33. Autonomia de resposta

Nem toda resposta pode ser automática.

Matriz conceitual:

```text
LOW RISK
circuit breaker / retry / fallback automático permitido

MEDIUM RISK
auto-containment + alerta

HIGH RISK
containment + supervisory approval

CRITICAL
fail-closed + human authority quando definido por policy
```

Auto-recuperação só deve atuar em caminhos testados e reversíveis.

---

# 34. Postmortem e aprendizado operacional

Todo incidente relevante deve poder gerar:

```text
root cause candidate
contributing factors
missing detector
missing guardrail
recovery gap
new test case
new evaluator case
new policy candidate
new capability candidate
```

Esses itens podem alimentar Learning Quarantine.

O incidente não altera o Core diretamente.

---

# 35. Invariantes v0.1

**DECISÃO APROVADA COMO BASE PARA TESTE**

1. Falha crítica nunca deve permanecer silenciosa quando houver sinal detectável.
2. Health técnico, cognitivo e econômico permanecem distinguíveis.
3. Componentes críticos possuem supervisão independente suficiente ao risco.
4. Taint/invalidity de ancestral relevante precisa ser propagável via lineage.
5. Contenção precede recuperação quando propagação continua possível.
6. Recuperação exige verificação antes de restaurar confiança plena.
7. Circuit breaker/fallback/retry são rastreáveis no trace.
8. Retry automático exige idempotência ou segurança equivalente.
9. Cross-tenant contamination é incidente crítico.
10. Ausência de watchdog crítico gera coverage gap observável.
11. Learning Quarantine permanece isolado durante incidentes e recuperação.
12. Fail-open/fail-closed depende de risk + policy; não existe default universal.
13. Falha em provider externo não autoriza downgrade silencioso abaixo do requisito de qualidade/risco.
14. Recovery e fault injection precisam ser testados antes de alegar resiliência enterprise.
15. Postmortem pode gerar candidatos; não modifica Trusted Core diretamente.

---

# 36. Questões em aberto

- matriz final de severity;
- propagação de taint por tipo de lineage;
- thresholds de circuit breaker;
- definição de health staleness;
- implementação física de watchdogs;
- isolation pools/bulkheads da primeira versão;
- Resilience Reserve inicial;
- políticas de load shedding;
- métricas/SLOs por classe de risco;
- incident storage;
- alert routing;
- recovery runbooks;
- authority model para incidentes críticos;
- escopo de auto-recovery;
- fault-injection suite inicial;
- estratégia futura de chaos engineering.

---

# 37. Frase de fundação

> **Um organismo confiável não é o que nunca adoece. É o que percebe a alteração, contém o dano, preserva o que está saudável, recupera o que pode ser recuperado e prova que voltou a funcionar antes de confiar novamente em si mesmo.**
