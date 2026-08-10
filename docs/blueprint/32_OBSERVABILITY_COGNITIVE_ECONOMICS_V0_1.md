# Eva Engine® — Observability & Cognitive Economics v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** definir como o Eva Engine® observa seu próprio comportamento operacional, cognitivo e econômico, permitindo explicar custos, escalonamentos, gargalos, desperdícios, qualidade por mecanismo e valor marginal de cada etapa do processamento.

---

# 1. Definição

O Eva Engine® precisa observar não apenas:

```text
está funcionando?
```

mas também:

```text
como está funcionando?
por que escolheu este caminho?
quanto custou?
quanto demorou?
qual mecanismo consumiu mais?
quando escalou para IA?
por que escalou?
qual foi o ganho marginal?
qual parte do pipeline gera retrabalho?
onde a empresa está pagando caro sem ganho proporcional?
```

Esse conjunto forma dois planos complementares:

```text
OBSERVABILITY
entender comportamento e estado do sistema

COGNITIVE ECONOMICS
entender custo, valor e eficiência do trabalho cognitivo
```

---

# 2. Observability não é logging

Logs são apenas uma fonte.

O plano de observabilidade combina:

```text
LOGS
METRICS
TRACES
EVENTS
HEALTH
EVALUATION RESULTS
COST RECORDS
POLICY DECISIONS
```

Princípio:

> **Se uma decisão cognitiva relevante aconteceu, precisamos conseguir reconstruir seu caminho sem depender da memória de um processo ou de uma pessoa.**

---

# 3. Os quatro eixos de observabilidade

Separar pelo menos:

```text
OPERATIONAL OBSERVABILITY
latência, erro, saturação, retries, filas

COGNITIVE OBSERVABILITY
capabilities, evidência, claims, confidence, waves, stop reasons

GOVERNANCE OBSERVABILITY
policy, scope, autorização, promotion, quarantine

ECONOMIC OBSERVABILITY
custo, escalonamento, uso de IA, custo por sucesso, valor marginal
```

---

# 4. Trace como espinha dorsal

Cada execução relevante possui `trace_id`.

Um trace pode reconstruir:

```text
EVENT E1
  ↓
PLAN P7
  ↓
CAP_A
  ↓
CAP_B
  ↓
CHALLENGER
  ↓
EVIDENCE E4
  ↓
POLICY DECISION
  ↓
RESULT R9
```

E também:

```text
latency
cost
retries
fallbacks
warnings
health snapshots
stop reason
AI escalation
human escalation
```

---

# 5. Span model

Em implementação distribuída, traces podem ser divididos em spans.

```text
TRACE T1
├── span ingestion
├── span capability_query
├── span CAP_TEMPORAL_PARSE
├── span CAP_RETRIEVAL
├── span challenger
├── span policy
└── span output
```

O padrão físico pode adotar OpenTelemetry ou outra solução compatível no futuro.

A arquitetura não depende de fornecedor de observabilidade.

---

# 6. Structured logs

Logs relevantes devem ser estruturados.

Preferir:

```text
trace_id
span_id
object_id
capability_id
plan_id
severity
message_code
metrics
policy_ref
scope_ref
```

Evitar logar payload bruto sensível por conveniência.

---

# 7. Metrics taxonomy

Dividir métricas em famílias.

## 7.1 Operational

```text
request_rate
error_rate
latency_p50/p95/p99
queue_depth
worker_utilization
retry_rate
timeout_rate
circuit_breaker_state
```

## 7.2 Cognitive

```text
atoms_per_event
relations_per_event
claims_per_event
waves_per_event
false_relation_rate
challenger_rejection_rate
confidence_calibration
stop_reason_distribution
```

## 7.3 Orchestration

```text
capability_calls_per_plan
replan_rate
fallback_rate
fanout_distribution
budget_overrun_rate
AI_escalation_rate
human_escalation_rate
```

## 7.4 Learning

```text
learning_candidates_created
promotion_rate
rejection_rate
rollback_rate
post_promotion_regression
```

## 7.5 Integrity

```text
incident_rate
MTTD
MTTC
MTTR
tainted_artifacts
recompute_rate
watchdog_coverage
```

## 7.6 Economic

```text
cost_per_event
cost_per_success
cost_per_capability
cost_per_wave
external_api_cost
human_review_cost
quality_per_cost
```

---

# 8. Cognitive Cost Unit

O sistema precisa de uma unidade abstrata para comparar trabalho mesmo quando não há custo externo direto.

Nome inicial:

**Cognitive Cost Unit (CCU)**

Pode compor:

```text
CPU time
memory
I/O
external API
model inference
storage
network
human review
```

CCU não substitui moeda real.

É uma unidade interna de comparação operacional.

---

# 9. Monetary cost

Quando houver custo financeiro real, registrar separadamente:

```text
currency
amount
provider
service
billing_dimension
trace_id
capability_id
```

Nunca converter automaticamente custo computacional em valor econômico sem modelo explícito.

---

# 10. Cost attribution

Cada custo precisa ser atribuível quando possível.

```text
TOTAL TRACE COST
   │
   ├── ingestion
   ├── retrieval
   ├── graph
   ├── local model
   ├── external LLM
   ├── storage
   └── human review
```

Isso permite descobrir onde o dinheiro está indo.

---

# 11. Cost per capability

Para cada capability:

```text
calls
successes
failures
average_cost
p95_cost
average_latency
quality_score
fallback_rate
escalation_rate
```

Pergunta:

> **esta capability ainda merece ocupar esta posição da cadeia?**

---

# 12. Quality-per-cost

Uma capability mais precisa pode ser economicamente pior.

Exemplo:

```text
CAP_A
quality = 0.95
cost = 1

CAP_B
quality = 0.96
cost = 20
```

A escolha depende do requisito.

Não existe vencedor universal.

---

# 13. Marginal Cognitive Value

Cada nova etapa deve tentar responder:

```text
quanto essa chamada acrescentou?
```

Métrica conceitual:

```text
MarginalValue = gain_after_step - gain_before_step
```

Pode ser medido por:

```text
new independent evidence
uncertainty reduction
error reduction
retrieval improvement
claim resolution
risk reduction
```

---

# 14. Marginal cost

Da mesma forma:

```text
MarginalCost = cost_after_step - cost_before_step
```

Então podemos estudar:

```text
Value / Cost
```

sem fingir que existe uma fórmula única universal.

---

# 15. Economics of Waves

A Explosão Atômica precisa de economia por wave.

```text
WAVE 0
cost 1
gain 10

WAVE 1
cost 2
gain 6

WAVE 2
cost 4
gain 2

WAVE 3
cost 8
gain 0.2
```

O Orchestrator pode aprender que Wave 3 raramente vale a pena naquele contexto.

---

# 16. Stop Economics

Uma condição de parada pode considerar:

```text
expected_information_gain
expected_risk_reduction
expected_quality_gain
remaining_budget
marginal_cost
```

Conceitualmente:

```text
continue if expected_value > expected_cost
```

A fórmula final depende do domínio e será validada empiricamente.

---

# 17. AI Escalation Economics

Toda chamada de IA externa deve poder explicar:

```text
why_escalated
prior_attempts
remaining_ambiguity
risk_class
required_quality
expected_gain
estimated_cost
actual_cost
```

Assim podemos medir:

```text
AI calls that added value
AI calls that did not
AI calls that could be avoided
AI calls that should have happened earlier
```

---

# 18. AI Avoidance não é meta absoluta

Um baixo AI escalation rate não significa sistema melhor.

Exemplo:

```text
AI escalation caiu 80%
quality caiu 20%
```

isso é fracasso.

A métrica correta combina:

```text
quality
risk
cost
latency
```

---

# 19. Human Escalation Economics

Revisão humana possui custo e valor.

Registrar:

```text
human_review_count
review_time
review_cost
correction_rate
confirmation_rate
high-risk saves
```

O objetivo não é eliminar humano.

É chamar humano onde autoridade ou julgamento realmente agregam valor.

---

# 20. Cost of false positives

Em certos domínios, erro custa mais que computação.

Exemplo:

```text
false alert
  ↓
manual investigation
  ↓
time lost
```

Logo a avaliação econômica deve poder incorporar:

```text
false_positive_operational_cost
false_negative_operational_cost
```

quando houver baseline real.

---

# 21. Cost of context loss

Uma dor B2B central é reconstruir contexto repetidamente.

Métricas possíveis em piloto:

```text
manual lookup time
number of systems opened
handoff time
reconstruction time
repeat investigation count
```

O Eva Engine® poderá medir redução dessas tarefas quando chegar a E4/E5.

---

# 22. Cost of duplicate cognition

Organizações podem executar o mesmo trabalho várias vezes.

Exemplo:

```text
Agent A investigates X
Agent B investigates X
Analyst C investigates X
Consultant D investigates X
```

O motor pode medir:

```text
duplicate investigation signatures
reused evidence
reused context
avoided recomputation
```

---

# 23. Cognitive Cache Economics

Cache não serve apenas para performance.

Pode evitar custo cognitivo repetido.

Medir:

```text
cache_hit_rate
avoided_external_calls
avoided_compute
staleness_incidents
quality_delta_due_to_cache
```

Cache inválido pode ser mais caro que recomputar.

---

# 24. Cost of Observability

Observabilidade também custa.

Medir:

```text
log volume
trace volume
metric cardinality
storage cost
retention cost
query cost
```

Princípio:

> **não podemos economizar IA e gastar a economia inteira em telemetria inútil.**

---

# 25. Cardinality control

Tags de métricas não devem usar valores de alta cardinalidade sem necessidade.

Exemplo perigoso:

```text
user_id as metric label
```

Preferir traces/logs para identidade individual e métricas agregadas para tendências.

---

# 26. Privacy in observability

Logs e traces obedecem às mesmas fronteiras de privacy.

Nunca assumir:

```text
“é só telemetria”
```

como justificativa para copiar dado sensível.

Aplicar:

```text
redaction
minimization
retention
access control
scope isolation
```

---

# 27. Tenant economics

Em B2B, custos precisam ser atribuíveis por tenant sem misturar dados.

Possíveis métricas:

```text
cost_per_tenant
AI_spend_per_tenant
storage_per_tenant
human_review_per_tenant
quality_per_tenant
```

Isso permite billing, FinOps e investigação de uso atípico no futuro.

---

# 28. Domain economics

Também medir por domínio:

```text
finance
support
operations
engineering
logistics
```

O mesmo mecanismo pode ter ROI muito diferente em cada domínio.

---

# 29. Value proxies

Antes de E6, podemos usar proxies.

Exemplos:

```text
time_to_resolution
manual_steps
rework_count
false_alerts
AI_calls_avoided
context_reuse
investigation_depth
```

Eles não são equivalentes a dinheiro economizado.

---

# 30. ROI só em E6

Alegação econômica forte exige:

```text
baseline financeiro
período comparável
controle de variáveis relevantes
custo total do Eva Engine®
impacto operacional medido
```

Princípio:

> **“economizamos milhões” é resultado de prova econômica, não de arquitetura promissora.**

---

# 31. Cost Ledger

O sistema deve considerar um **Cost Ledger** lógico.

```text
CostRecord
├── cost_id
├── trace_id
├── capability_id
├── provider?
├── resource_type
├── amount
├── currency?
├── compute_units?
├── timestamp
├── tenant_scope
└── provenance
```

---

# 32. Value Ledger

Mais tarde, pilotos podem registrar:

```text
ValueRecord
├── value_id
├── trace_id
├── metric_type
├── baseline
├── observed
├── delta
├── confidence_interval?
├── domain
└── evidence_refs[]
```

Não transformar proxy em moeda sem modelo explícito.

---

# 33. Observability dashboards

Dashboards futuros podem incluir:

```text
SYSTEM HEALTH
COGNITIVE QUALITY
AI USAGE
COST BY CAPABILITY
COST BY TENANT
WAVES / FANOUT
INCIDENTS
PROMOTION HEALTH
EVALUATION REGRESSIONS
```

Dashboard é interface; o plano de dados existe independentemente da UI.

---

# 34. Alerts

Alertas candidatos:

```text
AI spend spike
cost_per_event spike
quality drop
latency spike
fallback spike
human escalation spike
wave explosion
policy denials spike
cross-tenant anomaly
watchdog missing
```

Thresholds serão calibrados.

---

# 35. Anomaly detection on economics

Custo também pode sofrer anomalia.

Exemplo:

```text
CAP_X cost baseline = 0.002/event
current = 0.08/event
```

Mesmo se quality estiver estável, economic health fica degradado.

---

# 36. Budget enforcement

O Orchestrator recebe budgets.

Observability verifica:

```text
budget allocated
budget consumed
budget remaining
overrun
stop triggered
reserve used
```

Budget sem telemetria vira desejo, não controle.

---

# 37. Cost-aware routing

Routing pode usar custo como critério após hard constraints.

Fluxo:

```text
eligible capabilities
      ↓
quality/risk constraints
      ↓
cost/latency ranking
      ↓
selected implementation
```

Nunca escolher o mais barato se ele não satisfaz requisito.

---

# 38. Economic health

Health Registry recebe sinais econômicos:

```text
cost_delta
quality_per_cost_delta
AI_escalation_delta
human_review_delta
provider_price_change
```

Uma capability pode ser:

```text
technical = HEALTHY
cognitive = HEALTHY
economic = DEGRADED
```

---

# 39. FinOps integration future

Em ambiente enterprise, o plano poderá integrar com práticas FinOps.

Objetivos:

```text
cost allocation
budget forecasting
provider comparison
usage optimization
chargeback/showback
```

Sem acoplar o Core a uma ferramenta FinOps específica.

---

# 40. Evaluation integration

Evaluation Plane produz qualidade.

Observability produz comportamento real.

Economics produz custo.

Juntos:

```text
QUALITY
+
RUNTIME BEHAVIOR
+
COST
=
OPERATIONAL SCORECARD
```

Sem criar um único score mágico.

---

# 41. Promotion economics

Uma candidate pode ser melhor cognitivamente e pior economicamente.

Promotion Gate precisa enxergar:

```text
quality_delta
cost_delta
latency_delta
risk_delta
AI_escalation_delta
```

A decisão depende de policy e valor operacional.

---

# 42. Postmortem economics

Incidentes também têm custo.

Registrar quando possível:

```text
recovery_compute
human_hours
external_calls
reprocessing
service degradation
```

Isso ajuda a comparar confiabilidade versus custo.

---

# 43. Invariantes v0.1

**DECISÃO APROVADA COMO BASE PARA TESTE**

1. Toda execução relevante possui trace correlacionável.
2. Custo deve ser atribuível a capability/trace quando tecnicamente viável.
3. AI escalation precisa registrar motivo e custo.
4. Human escalation precisa ser mensurável.
5. Cost e quality são dimensões separadas.
6. Observability data também obedece privacy e retention.
7. Metric cardinality precisa ser controlada.
8. Marginal value de waves deve ser mensurável quando possível.
9. Budget consumption precisa ser observável.
10. Economic Health é distinto de Technical/Cognitive Health.
11. Value proxy não pode ser apresentado como economia monetária.
12. ROI externo exige evidência E6.
13. Observability overhead também deve ser medido.
14. Cost-aware routing só ocorre depois de hard constraints.
15. Promotion decisions relevantes consideram quality, risk, latency e cost.

---

# 44. Questões em aberto

- formato físico do Cost Ledger;
- definição inicial de Cognitive Cost Unit;
- instrumentação inicial de traces;
- provider inicial de observabilidade;
- política de sampling;
- retention por classe de trace;
- dashboards iniciais;
- cardinality limits;
- cálculo de marginal information gain;
- quality-per-cost function;
- modelo de value proxies;
- integração futura com FinOps;
- showback/chargeback;
- limites de AI spend por tenant;
- alert thresholds;
- custo máximo de observability sobre custo total.

---

# 45. Frase de fundação

> **O Eva Engine® não deve apenas saber pensar. Precisa saber quanto custou pensar, por que escolheu pensar daquele jeito e se o ganho obtido justificou o trabalho realizado.**
