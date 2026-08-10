# Eva Engine® — Evaluation Plane v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** definir como o Eva Engine® mede qualidade, regressão, custo, latência, calibração, segurança, robustez e impacto de cada capability, composição e versão do organismo antes de afirmar melhoria ou promover mudanças.

---

# 1. Definição

O **Evaluation Plane** é a camada que responde:

```text
isso funciona?
funciona melhor que antes?
em quais casos?
quanto melhorou?
onde piorou?
quanto custa?
quanto demora?
continua calibrado?
continua seguro?
a melhora sobrevive em holdout?
a melhora sobrevive em escala?
a melhora justifica promoção?
```

Princípio:

> **Nenhuma mudança é “mais inteligente” apenas porque produz uma saída mais convincente.**

---

# 2. Evaluator não é test runner

Testes tradicionais respondem se comportamento esperado quebrou.

O Evaluation Plane precisa ir além:

```text
TEST
pass / fail de contrato

EVALUATION
medida comparável de qualidade, custo, risco e estabilidade
```

Exemplo:

```text
unit test:
CAP_TEMPORAL_PARSE reconhece “amanhã”? yes/no

evaluation:
precision = 0.98
recall = 0.96
latency_p95 = 4ms
cost = near-zero
regression_vs_baseline = +0.8pp
```

---

# 3. Avaliação em três níveis

O Eva Engine® precisa avaliar:

```text
LEVEL 1 — CAPABILITY
uma função isolada

LEVEL 2 — COMPOSITION
capabilities combinadas

LEVEL 3 — SYSTEM
resultado do organismo inteiro
```

Uma capability pode melhorar isoladamente e piorar a composição.

Exemplo:

```text
CAP_RELATION_DISCOVERY ↑ recall
            +
CAP_COGNITIVE_EXPANSION
            ↓
false relations ↑
```

Portanto:

> **melhoria local não implica melhoria sistêmica.**

---

# 4. Baseline é obrigatório

Toda avaliação de melhoria precisa de referência.

Baseline pode ser:

```text
versão anterior
regra simples
algoritmo clássico
sem feature
modelo menor
processo humano atual
custo operacional atual
```

Exemplo:

```text
candidate v2
vs
baseline v1
```

Sem baseline existe resultado; não existe prova de melhoria.

---

# 5. Evaluation Unit

Contrato conceitual:

```text
EvaluationRun
├── evaluation_id
├── subject_type
├── subject_id
├── subject_version
├── baseline_id
├── dataset_version
├── evaluator_version
├── scope
├── started_at
├── finished_at
├── metrics{}
├── slices{}
├── regressions[]
├── warnings[]
├── cost_metrics{}
├── latency_metrics{}
├── calibration_metrics{}
├── safety_metrics{}
├── result
└── trace_refs[]
```

---

# 6. Dataset Registry

Datasets são patrimônio tecnológico e precisam de identidade/versionamento.

Cada dataset deve registrar:

```text
dataset_id
version
purpose
scope
languages[]
domains[]
source_provenance
license/usage_policy
privacy_class
creation_method
known_biases
known_gaps
created_at
frozen_hash
```

Datasets sintéticos e reais devem ser distinguíveis.

---

# 7. Split de dados

Separar pelo menos:

```text
TRAIN / DEVELOPMENT
ajuste

VALIDATION
seleção de configuração

HOLDOUT / TEST
estimativa final não vista
```

Para mecanismos sem “treinamento” formal, a lógica continua válida:

não otimizar continuamente em cima do mesmo conjunto que será usado para afirmar melhoria.

---

# 8. Golden Dataset

Golden cases funcionam como contrato de regressão.

Eles preservam comportamentos importantes já conquistados.

Exemplo:

```text
input
expected artifacts
forbidden artifacts
allowed uncertainty
expected policy outcome
```

Golden não substitui holdout.

Ele protege o conhecido; holdout mede generalização.

---

# 9. Regression Dataset

Todo bug cognitivo relevante deve gerar caso permanente.

Fluxo:

```text
FAILURE FOUND
    ↓
MINIMAL REPRODUCTION
    ↓
REGRESSION CASE
    ↓
SUITE PERMANENTE
```

O organismo transforma erro conhecido em barreira futura.

---

# 10. Adversarial Evaluation

Avaliar casos desenhados para enganar mecanismos.

Exemplos:

```text
negação
ambiguidade
ironia
metáfora
duplicata
base-rate trap
confounder
source echo
prompt injection
contradição
out-of-distribution
schema edge cases
```

Objetivo:

> **medir onde o motor quebra, não apenas onde ele brilha.**

---

# 11. Evaluation Slices

Uma média global pode esconder falhas graves.

Resultados precisam ser fatiáveis por:

```text
idioma
domínio
risk_class
source_type
tenant profile
input size
ambiguity level
mechanism class
cost tier
artifact type
schema version
time window
```

Exemplo:

```text
overall accuracy = 96%

pt-BR = 98%
en = 97%
es = 91%
```

A média não pode esconder o 91% se o requisito daquele slice for maior.

---

# 12. No single magic score

**DECISÃO APROVADA COMO PRINCÍPIO**

O sistema não deve comprimir tudo em um único “Eva Score”.

Porque:

```text
quality ↑
cost ↑↑↑
latency ↑↑
```

pode ser pior para o negócio.

Preferir scorecards multidimensionais.

---

# 13. Quality Metrics

Métricas dependem da capability.

Possíveis:

```text
precision
recall
f1
accuracy
top-k recall
mean reciprocal rank
nDCG
relation precision
entity-linking accuracy
false-positive rate
false-negative rate
correction rate
continuity recovery rate
```

Nenhuma métrica deve ser escolhida apenas por popularidade.

---

# 14. Calibration Metrics

Para outputs com confidence calibrada:

```text
Brier Score
Expected Calibration Error (ECE)
log loss
reliability bins
```

Regra:

> **se não conseguimos validar calibração, não chamamos score de confidence.**

---

# 15. Retrieval Evaluation

Possíveis métricas:

```text
Recall@K
Precision@K
MRR
nDCG
silence accuracy
false retrieval rate
```

Também medir:

```text
relevant but not retrieved
retrieved but harmful/noisy
```

---

# 16. Relation Evaluation

Medir separadamente:

```text
relation precision
relation recall
false relation rate
unsupported relation rate
causal overreach rate
evidence echo rate
```

Quanto maior a Explosão Atômica, mais importante medir crescimento de relações espúrias.

---

# 17. Orchestration Evaluation

O Orchestrator também precisa ser avaliado.

Métricas:

```text
plan success rate
unnecessary capability calls
missed capability rate
fallback rate
replan rate
budget overrun rate
stop accuracy
fan-out distribution
wave distribution
AI escalation rate
human escalation rate
```

Pergunta importante:

> o Maestro está chamando peças demais para resolver coisas simples?

---

# 18. Economic Evaluation

Para B2B enterprise:

```text
cost_per_event
cost_per_success
cost_per_1k_events
external_api_cost
compute_cost
human_review_cost
AI_escalation_cost
quality_per_cost
latency_per_cost
```

Mais tarde, em piloto real:

```text
time_saved
manual_steps_avoided
incident_resolution_time
rework_reduction
operational_loss_avoided
```

Nenhuma métrica econômica deve virar alegação externa antes de E5/E6 apropriado.

---

# 19. Latency Evaluation

Medir:

```text
p50
p95
p99
queue_wait
external_call_time
replan_time
recovery_time
```

Média simples não é suficiente para workloads enterprise.

---

# 20. Robustness Evaluation

Testar estabilidade sob variações:

```text
input noise
missing fields
schema evolution
large inputs
burst traffic
provider failure
latency injection
partial dependency failure
stale health data
```

---

# 21. Security & Policy Evaluation

Casos mínimos:

```text
cross-tenant access denied
restricted data not sent to external AI
policy bypass impossible
missing authorization fails safely
prompt injection does not alter policy authority
learning candidate cannot self-promote
```

Resultados de segurança não devem ser diluídos numa média geral.

---

# 22. Integrity Evaluation

Medir se o sistema detecta e recupera:

```text
corrupted artifact
revoked evidence
poisoned candidate
tainted ancestor
missing watchdog
stale health
broken capability dependency
```

Métricas:

```text
MTTD
MTTC
MTTR
blast_radius_accuracy
recompute_success_rate
rollback_success_rate
false_alarm_rate
```

---

# 23. Learning Evaluation

Cada nível de aprendizagem exige avaliação compatível.

```text
L1 session
local usefulness

L2 tenant
personalization gain without contamination

L3 domain
generalization across domain holdout

L4 global
broad evaluation + regression + explicit promotion
```

Métricas candidatas:

```text
personalization_gain
cross-tenant_leakage = 0
regression_count
holdout_gain
calibration_delta
```

---

# 24. Shadow Evaluation

Uma candidate version pode rodar sem influenciar produção.

```text
PRODUCTION PATH
CAP_V1 → result used

SHADOW PATH
same input → CAP_V2 → result NOT used
```

Comparar:

```text
quality
latency
cost
error modes
```

Shadow é especialmente útil antes de promover mecanismos de alto impacto.

---

# 25. Canary Evaluation

Após validação offline/shadow:

```text
small traffic slice
      ↓
monitor
      ↓
expand gradually
      ↓
full rollout
```

Com rollback automático/assistido quando critérios críticos forem violados.

---

# 26. Counterfactual Evaluation

Quando possível, comparar:

```text
WITH CAPABILITY
vs
WITHOUT CAPABILITY
```

ou:

```text
ROUTE A
vs
ROUTE B
```

Isso ajuda a medir contribuição marginal real.

---

# 27. Ablation Testing

Em composições complexas, remover uma peça temporariamente em avaliação:

```text
full stack
minus Lens X
minus CAP_Y
minus Challenger
```

Pergunta:

> esta peça realmente acrescenta valor ou apenas complexidade?

Ablation é central para controlar crescimento arquitetural.

---

# 28. Evaluation of Explosão Atômica

Precisamos medir se waves adicionais ajudam.

Por wave:

```text
new_information_gain
new_evidence_count
independent_evidence_gain
noise_added
false_relation_delta
latency_added
cost_added
```

Curva desejada:

```text
Wave 0 → high gain
Wave 1 → high gain
Wave 2 → moderate gain
Wave 3 → low gain
Wave 4 → negligible
STOP
```

A condição de parada deve ser empiricamente calibrada.

---

# 29. Promotion Scorecard

Uma promoção não deve depender de uma única métrica.

Exemplo conceitual:

```text
QUALITY        pass
REGRESSION     pass
CALIBRATION    pass
SAFETY         pass
PRIVACY        pass
LATENCY        pass
COST           pass
ROBUSTNESS     pass
HOLDOUT        pass
SHADOW         pass
ROLLBACK       verified
```

Policy define quais itens são obrigatórios por risk class.

---

# 30. Hard gates versus soft goals

Separar:

```text
HARD GATE
cross-tenant leak = 0
critical policy bypass = 0
schema incompatibility = 0

SOFT GOAL
latency improve 5%
cost reduce 10%
recall improve 1pp
```

Uma melhoria em soft goal não compensa falha em hard gate.

---

# 31. Evaluator Registry

Evaluators também precisam ser versionados.

```text
EvaluatorDescriptor
├── evaluator_id
├── version
├── subject_types[]
├── metrics[]
├── dataset_requirements[]
├── risk_classes[]
├── threshold_policy
├── implementation_ref
└── status
```

Uma capability pode declarar qual evaluator valida sua qualidade.

---

# 32. Evaluator independence

O mecanismo avaliado não deve controlar sozinho sua própria avaliação.

Preferir:

```text
CAP_X
  ↓ outputs
EVALUATOR_X
  ↓ metrics
EVALUATION LEDGER
```

Para avaliações críticas, considerar evaluator alternativo ou auditoria humana.

---

# 33. Evaluation Ledger

Resultados de avaliação precisam ser históricos e comparáveis.

Objetivos:

```text
reproduzir decisão de promoção
comparar versões
investigar regressão
provar baseline
acompanhar drift
explicar rollback
```

Não significa blockchain; significa histórico confiável e versionado.

---

# 34. Reproducibility

Uma avaliação deve registrar o suficiente para ser repetida quando tecnicamente possível:

```text
dataset version
subject version
config
seed?
provider/model version
evaluator version
policy version
runtime environment reference
```

Providers externos podem limitar determinismo absoluto; isso deve ser registrado.

---

# 35. Statistical significance e practical significance

Uma diferença pequena pode ser estatisticamente detectável e economicamente irrelevante.

Portanto distinguir:

```text
statistical significance
vs
practical / operational significance
```

Exemplo:

```text
+0.05% accuracy
+300% cost
```

pode não ser uma melhoria útil.

---

# 36. Confidence intervals

Quando aplicável, métricas devem incluir intervalo de incerteza.

Evitar comparar:

```text
0.941
vs
0.943
```

como diferença real sem tamanho amostral e incerteza suficientes.

---

# 37. Drift Evaluation

A performance precisa ser acompanhada no tempo.

Tipos:

```text
data drift
concept drift
performance drift
cost drift
latency drift
calibration drift
```

Drift pode disparar:

```text
DEGRADED health
shadow reevaluation
rollback
new learning candidate
```

---

# 38. Evaluation cadence

Nem tudo roda na mesma frequência.

Exemplo conceitual:

```text
unit/regression     every change
core golden         every build/release
large holdout       pre-promotion
shadow              continuous window
cost/latency        continuous
calibration         periodic/sample-based
red team            scheduled + pre-major-release
```

Cadência final depende de custo e risco.

---

# 39. E0–E6 e Evaluation Plane

A escada de evidência se conecta diretamente:

```text
E0 — idea
no proof

E1 — mechanism proof
small controlled evaluator

E2 — reproducible battery
versioned dataset + baseline

E3 — synthetic scale
load + cognitive scale

E4 — domain pilot
real domain + shadow/controlled production

E5 — operational proof
real operation KPI improvement

E6 — economic proof
verified financial impact
```

O Evaluation Plane é o mecanismo que permite subir de degrau sem pular etapas.

---

# 40. Invariantes v0.1

**DECISÃO APROVADA COMO BASE PARA TESTE**

1. Toda alegação de melhoria precisa de baseline explícito.
2. Capability, composição e sistema são avaliados separadamente.
3. Golden protege regressão; holdout mede generalização.
4. Uma média global não pode ocultar slices críticos.
5. Hard safety/privacy gates não são compensados por ganhos de qualidade/custo.
6. Evaluators e datasets são versionados.
7. Resultados de avaliação precisam ser reproduzíveis quando tecnicamente possível.
8. Custo e latência fazem parte da avaliação enterprise.
9. Confidence exige avaliação de calibração quando usada como probabilidade operacional.
10. Explosão Atômica precisa demonstrar ganho marginal por waves.
11. Learning Candidate global não é promovido sem avaliação compatível com seu alcance.
12. Shadow/canary são preferidos para mudanças de alto risco antes de rollout amplo.
13. Rollback precisa ser testável.
14. Melhorar uma capability isolada não prova melhoria do sistema inteiro.
15. Evaluation results alimentam Health Registry e Promotion Gate.

---

# 41. Questões em aberto

- formato físico do Evaluation Ledger;
- Dataset Registry físico;
- conjunto inicial de evaluators;
- thresholds por risk class;
- tamanho mínimo de holdout;
- métodos estatísticos por output type;
- scorecard de promoção v1;
- cadência de red team;
- online evaluation sampling;
- privacy de datasets reais;
- synthetic data policy;
- evaluator compute budget;
- regra de promoção quando qualidade melhora e custo piora;
- practical-significance thresholds;
- critérios E3→E4 e E4→E5.

---

# 42. Frase de fundação

> **O Eva Engine® não melhora quando parece mais inteligente. Ele melhora quando uma versão nova supera a anterior em critérios definidos, sobre dados que não pôde decorar, sem violar os limites que tornam o sistema confiável e economicamente útil.**
