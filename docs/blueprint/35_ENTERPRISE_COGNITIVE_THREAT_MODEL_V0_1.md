# Eva Engine® — Enterprise Cognitive Threat Model v0.1

**Status:** base arquitetural para refinamento, red team e implementação  
**Função:** identificar ameaças técnicas, cognitivas, econômicas e de governança capazes de comprometer confidencialidade, integridade, disponibilidade, escopo, evidência, aprendizagem, custo ou autoridade do Eva Engine®.

---

# 1. Definição

O Threat Model do Eva Engine® precisa proteger mais do que servidores e credenciais.

Ele protege também:

```text
VERDADE OPERACIONAL
LINEAGE
EVIDENCE
TENANT SCOPE
LEARNING
PROMOTION
ROUTING
COST
POLICY
HUMAN AUTHORITY
```

Princípio:

> **Em um sistema cognitivo, atacar o que o motor acredita pode ser tão perigoso quanto atacar o código que ele executa.**

---

# 2. Ativos críticos

```text
A1  dados RAW autorizados
A2  Cognitive Envelopes
A3  lineage graph
A4  Evidence Ledger
A5  claims / hypotheses / inferences
A6  trusted learned state
A7  Learning Quarantine
A8  Promotion Gate
A9  Capability / Health / Schema Registries
A10 Orchestration Control Plane
A11 Policy Engine
A12 secrets / credentials
A13 tenant isolation
A14 evaluation datasets / holdouts
A15 baselines / evaluator results
A16 audit logs / traces
A17 cost budgets / quotas
A18 external action authority
A19 human approvals
A20 version manifests / rollback targets
```

---

# 3. Trust Boundaries

```text
[ EXTERNAL ENTERPRISE ]
        │
        ▼
TB1 — Integration Boundary
        │
        ▼
[ TRUSTED COGNITIVE FABRIC ]
        │
        ├──────── TB2 ────────► [ EXTERNAL AI / PROVIDERS ]
        │
        ├──────── TB3 ────────► [ HUMAN AUTHORITY ]
        │
        ▼
TB4 — Learning Boundary
        │
        ▼
[ LEARNING QUARANTINE ]
        │
        ▼
TB5 — Promotion Gate
        │
        ▼
[ PROMOTED TRUSTED STATE ]
```

Cada boundary precisa de autenticação/autorização, schema, scope, logging e failure policy apropriados.

---

# 4. Threat Families

O Threat Model usa famílias amplas:

```text
IDENTITY / AUTHORITY
DATA / PROVENANCE
TENANT / SCOPE
COGNITIVE / EPISTEMIC
LEARNING / PROMOTION
AGENT / MODEL
ORCHESTRATION
ECONOMIC / RESOURCE
SUPPLY CHAIN
OBSERVABILITY / EVALUATION
AVAILABILITY / RESILIENCE
HUMAN / INSIDER
```

---

# 5. Identity & Authority Threats

Exemplos:

- credential theft;
- forged service identity;
- stale token reuse;
- confused deputy;
- privilege escalation;
- unauthorized human approval;
- service-to-service impersonation;
- compromised adapter credentials.

Controles arquiteturais:

```text
least privilege
short-lived credentials where possible
explicit service identity
policy gates
approval scope
credential rotation
audit trail
separation of duties
```

---

# 6. Tenant & Scope Threats

Risco enterprise crítico:

```text
TENANT A
   │
   X──► TENANT B DATA / LEARNING / EVIDENCE
```

Ameaças:

- missing tenant filter;
- cache poisoning across tenants;
- vector retrieval before scope filter;
- incorrect identity mapping;
- shared learning promoted across tenants;
- debug tools bypassing scope;
- cross-tenant trace leakage.

Regra:

> **Scope é constraint estrutural, não filtro de UI.**

---

# 7. Provenance Spoofing

Atacante ou sistema comprometido tenta fazer conteúdo parecer proveniente de fonte mais confiável.

Exemplos:

```text
fake source_system
forged source_event_id
altered signed payload
replayed valid event
fabricated human approval
```

Controles:

- transport integrity;
- source authentication;
- immutable/append-oriented provenance records;
- correlation with adapter identity;
- signatures/hashes when justified;
- replay protection.

---

# 8. Data Poisoning

Dados manipulados podem induzir inferências ou aprendizado incorreto.

Formas:

```text
high-volume repeated false signals
strategic label manipulation
feedback fraud
synthetic duplicate flooding
rare-event distortion
cross-scope contamination
backfill poisoning
```

Defesas:

- provenance;
- deduplication;
- independence groups;
- rate limits;
- source weighting;
- anomaly detection;
- quarantine;
- holdout;
- challenger;
- scope isolation.

---

# 9. Knowledge Poisoning

Diferente de apenas dados ruins: objetivo é alterar conhecimento durável.

Alvos:

```text
rules
weights
relations
routing
ontology
aliases
domain knowledge
prompts/model configuration
```

Defesa principal:

```text
Learning Quarantine
     +
Promotion Gate
     +
Evaluation Plane
     +
lineage
     +
rollback/unlearning
```

---

# 10. Evidence Forgery / Evidence Laundering

Ameaça: transformar uma origem fraca em aparência de múltiplas evidências fortes.

```text
SOURCE A
  ↓ copied
B
  ↓ summarized
C
  ↓ model output
D

fake conclusion: 4 independent sources
```

Defesas:

- source lineage;
- independence groups;
- Evidence Echo detection;
- primary-source references;
- counter-evidence search.

---

# 11. Self-Reinforcement Attack

A Explosão Atômica cria risco de ciclo auto-confirmatório.

```text
INFERENCE A
    ↓
DERIVATIVE B
    ↓
RELATION C
    ↓
B treated as evidence for A
```

Controles:

- derived evidence not automatically independent;
- wave ancestry;
- maximum recursion;
- novelty/information-gain gate;
- challenger;
- evidence eligibility checks.

---

# 12. Prompt Injection / Tool Injection

Qualquer capability que processe linguagem natural com modelo pode receber conteúdo tentando alterar sua função.

Riscos:

- override de instruções internas;
- tentativa de acesso a ferramentas;
- extração de dados de outro contexto;
- indução de ação externa;
- manipulação de saída para parecer evidence.

Defesas arquiteturais:

```text
untrusted content stays data
least-privilege tool access
policy outside model
structured tool contracts
output validation
tenant/scope enforced outside prompt
model output treated as Artifact
no secret material in prompts when avoidable
```

Princípio:

> **Modelo nunca é a fronteira final de autorização.**

---

# 13. Agent Hijacking

Agente comprometido ou desviado pode:

- pedir capabilities indevidas;
- gerar fan-out excessivo;
- mentir sobre resultado;
- tentar escalonar autoridade;
- produzir outputs incompatíveis;
- esconder failure.

Controles:

```text
capability contracts
control-plane admission
bounded subplans
health/watchdogs
structured outputs
independent evaluation
budget caps
no direct global writes
```

---

# 14. Orchestrator Abuse

O Orchestrator é alvo de alto valor.

Ameaças:

```text
route everything to expensive AI
skip challenger
skip policy
starve critical capability
infinite replanning
invalid fallback selection
budget misallocation
scope confusion
```

Defesas:

- hard constraints before ranking;
- plan trace;
- policy-enforced admission;
- cost budgets;
- health monitoring;
- deterministic invariants;
- routing evaluation;
- learning routing policies in quarantine.

---

# 15. Denial of Wallet / Cost Amplification

Atacante não precisa derrubar sistema; pode fazê-lo gastar demais.

Exemplos:

```text
trigger high-cost paths repeatedly
force external AI escalation
create deep recursive waves
induce expensive retries
cause human-review flood
```

Controles:

- per-tenant budgets;
- per-event cost caps;
- max waves/fan-out;
- escalation quotas;
- circuit breakers;
- admission control;
- anomaly detection;
- economic health.

---

# 16. Resource Exhaustion / Denial of Service

Vetores:

- event floods;
- oversized payloads;
- pathological graphs;
- queue saturation;
- expensive retrievals;
- recursive expansion;
- backfill abuse.

Controles:

```text
size limits
rate limits
quotas
backpressure
bulkheads
timeouts
bounded graphs
priority queues
load shedding
```

---

# 17. Schema Confusion

Duas versões interpretam o mesmo payload de maneira diferente.

Riscos:

- field meaning drift;
- old adapter emitting new schema id;
- incompatible mapping;
- silent default values;
- type confusion.

Defesas:

- Schema Registry;
- explicit versioning;
- compatibility policy;
- fail closed on critical ambiguity;
- schema health monitoring.

---

# 18. Replay Attack

Evento válido é reapresentado para causar efeito duplicado.

Defesas:

- event identity;
- idempotency keys;
- nonce/signature where appropriate;
- source sequence;
- replay mode explicit;
- external actions idempotent where possible.

---

# 19. Stale State / Rollback Attack

Uma versão antiga vulnerável ou regra revogada volta a ser ativada.

Defesas:

```text
version manifests
promotion ledger
revocation list
allowed-version policy
signed artifacts when needed
rollback target validation
```

Rollback não deve significar “qualquer versão antiga serve”.

---

# 20. Promotion Gate Compromise

Um dos cenários mais perigosos.

Ameaças:

- forged evaluation report;
- holdout leakage;
- approval spoofing;
- candidate substitution;
- scope escalation;
- stale baseline;
- bypass of counter-evidence;
- race condition.

Defesas:

```text
separation of duties
immutable Promotion Manifest
artifact hash
version-bound evaluation reports
explicit target scope
human approval for critical changes
independent gate audit
```

---

# 21. Evaluation Poisoning

Atacante manipula o sistema que mede qualidade.

Exemplos:

- contaminar holdout;
- esconder failing subgroup;
- escolher apenas métricas favoráveis;
- modificar baseline;
- alterar evaluator;
- reutilizar test cases vistos pelo candidate.

Controles:

- dataset versioning;
- evaluator versioning;
- frozen holdout;
- provenance;
- multidimensional scorecards;
- hard safety gates;
- independent oracle where useful.

---

# 22. Observability Blindness

Ameaça: sistema continua operando enquanto logs/traces/metrics deixam de mostrar falhas.

Controles:

```text
telemetry health
coverage watchdog
out-of-band alerts
trace completeness checks
sampling policy
immutable audit trail for critical actions
```

Falha de observabilidade pode exigir degradação ou fail-closed em caminhos críticos.

---

# 23. Supply Chain Threats

Dependências podem introduzir risco:

```text
NPM package
container image
model artifact
external API
CI/CD action
SDK
embedding model
runtime
```

Controles:

- pin/version;
- SBOM when mature;
- dependency review;
- minimal dependencies;
- artifact integrity;
- provider abstraction;
- secrets isolation;
- CI policy.

---

# 24. External Provider Threats

Riscos:

- outage;
- policy change;
- data retention change;
- model behavior drift;
- price change;
- region change;
- result instability;
- compromised credentials.

Defesas:

- provider abstraction;
- health monitoring;
- fallback;
- privacy policy;
- cost monitoring;
- version logging;
- disable switch.

---

# 25. Human / Insider Threat

Humano autorizado pode:

- promover candidato indevido;
- acessar dados fora de necessidade;
- modificar policy;
- alterar baseline;
- exportar informação;
- aprovar ação de alto risco.

Controles:

```text
least privilege
separation of duties
approval tiers
strong audit
break-glass logging
access review
scope-bound tooling
```

---

# 26. Privacy Leakage Through Derived Artifacts

Mesmo sem RAW, derivados podem revelar conteúdo sensível.

Exemplos:

```text
embedding
summary
entity graph
semantic profile
learned preference
```

Portanto privacy class e retention precisam alcançar também derivados.

---

# 27. Model Extraction / Prompt Leakage

Quando aplicável, proteger:

- proprietary prompts;
- routing rules;
- domain knowledge;
- internal evaluators;
- proprietary heuristics;
- confidential capability descriptors.

Não registrar segredo proprietário em output/log por conveniência.

---

# 28. Cognitive Integrity Incident Severity

Taxonomia inicial:

```text
S0 — informational
S1 — local/no durable impact
S2 — degraded capability
S3 — incorrect inference affecting workflow
S4 — cross-scope / promoted contamination / unauthorized action
S5 — systemic integrity or critical enterprise impact
```

O severity define containment, notification, rollback e human authority.

---

# 29. Threat-to-Control Matrix

Cada threat relevante precisa mapear para pelo menos:

```text
PREVENT
DETECT
CONTAIN
RECOVER
VERIFY
```

Não depender somente de prevenção.

---

# 30. Red Team Suites

Suites futuras:

```text
RT-INGRESS
RT-TENANT
RT-POISONING
RT-EVIDENCE
RT-AGENT
RT-PROMPT
RT-ORCHESTRATION
RT-LEARNING
RT-PROMOTION
RT-COST
RT-OBSERVABILITY
RT-ACTION
RT-SUPPLY-CHAIN
```

Cada caso registra:

```text
attack_goal
entry_boundary
expected_control
expected_detection
expected_containment
forbidden_outcome
recovery_path
```

---

# 31. Security Invariants

1. Tenant scope não é inferido por conveniência.
2. External input nunca ganha trust somente por autenticidade de transporte.
3. Model output nunca é autoridade final.
4. Learning Candidate nunca escreve no Trusted Core.
5. Promotion Gate não aceita artefato sem evaluation/version binding.
6. Holdout não é treino.
7. Evidence lineage impede multiplicação artificial de fontes.
8. Orchestrator não pode exceder budget/policy por decisão de capability.
9. External action exige policy explícita.
10. Sensitive derived artifacts recebem proteção proporcional.
11. Critical observability failure pode bloquear/degradar caminho.
12. Rollback só usa versão autorizada e íntegra.
13. Provider externo pode ser desligado/substituído.
14. Cost é superfície de ataque.
15. Recovery e verification fazem parte da segurança.

---

# 32. Questões em aberto

- framework formal de threat modeling usado no ciclo de engenharia;
- classificação de dados final;
- authN/authZ inicial;
- encryption/key management;
- CI/CD hardening;
- artifact signing;
- SBOM policy;
- secret manager;
- red-team tooling;
- tenant isolation physical model;
- security incident response process;
- log retention;
- admin plane;
- break-glass policy;
- provider risk scoring;
- threat coverage metrics.

---

# 33. Frases de fundação

> **Segurança não protege apenas o que a Eva pode executar. Protege também o que ela pode acreditar.**

> **Em um motor recursivo, integridade cognitiva é uma superfície de segurança de primeira classe.**
