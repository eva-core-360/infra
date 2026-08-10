# Eva Engine® — Capability, Health & Schema Registries v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** definir como o Eva Engine® descobre, descreve, seleciona, monitora e governa suas capacidades sem acoplar o Orchestrator a implementações específicas.

---

# 1. Por que registries são parte do organismo

À medida que o Eva Engine® cresce, o Orchestrator não pode conhecer manualmente cada agente, regra, parser, modelo, lente, índice, algoritmo ou integração.

Ele precisa perguntar ao sistema:

```text
quem existe?
o que sabe fazer?
com quais entradas?
qual versão?
em qual domínio?
qual risco?
qual custo?
qual latência?
está saudável?
qual evidência de qualidade possui?
qual fallback existe?
posso usar neste tenant/contexto?
```

Os registries formam o **catálogo vivo do organismo**.

Princípio:

> **O Orchestrator não chama componentes por familiaridade; ele seleciona capabilities por contrato, saúde, policy, custo e evidência.**

---

# 2. Três registries, três perguntas diferentes

```text
SCHEMA REGISTRY
"Que estrutura é esta?"

CAPABILITY REGISTRY
"Quem sabe fazer o quê?"

HEALTH REGISTRY
"Quem está apto a fazer agora?"
```

Eles se relacionam, mas não devem ser fundidos em um único catálogo opaco.

---

# 3. Schema Registry

O **Schema Registry** descreve estruturas canônicas e extensões permitidas.

Exemplos:

```text
EventEnvelope v1
AtomicEnvelope v1
EvidenceRecord v1
ClaimRecord v1
InferenceRecord v1
LearningCandidate v1
CapabilityDescriptor v1
HealthSnapshot v1
DomainPack schema
```

Cada schema deve possuir, no mínimo:

```text
schema_id
version
status
compatibility_policy
required_fields
optional_fields
constraints
owner_scope
introduced_at
deprecated_at?
supersedes?
```

Objetivos:

- validação previsível;
- evolução sem quebrar consumidores;
- auditabilidade;
- compatibilidade entre módulos;
- migrações controladas;
- extensões por Domain Pack sem contaminar o Core.

Princípio:

> **O Schema Registry define a forma dos objetos; não decide o significado operacional de uma capability.**

---

# 4. Capability Registry

Uma **Capability** é uma função que o sistema sabe executar sob um contrato conhecido.

Ela pode ser implementada por:

```text
regra determinística
função TypeScript
SQL
algoritmo de grafo
estatística
parser
modelo local
LLM externo
agente especializado
humano
combinação de mecanismos
```

O Registry não deve presumir tecnologia.

Exemplo conceitual:

```text
capability_id: CAP_TEMPORAL_PARSE
version: 1.3.0
purpose: "extract explicit and relative temporal expressions"
input_schema: EventEnvelope@1
output_schema: TemporalSignal@2
modes: [deterministic]
languages: [pt-BR, en, es]
risk_class: LOW
cost_class: VERY_LOW
latency_class: FAST
privacy_class: LOCAL_SAFE
quality_tier: VALIDATED
fallback: CAP_TEMPORAL_PARSE_BASIC
health_requirement: HEALTHY_OR_DEGRADED
```

---

# 5. Capability Descriptor

Contrato inicial sugerido:

```text
CapabilityDescriptor
├── capability_id
├── version
├── name
├── purpose
├── category
├── owner_module
├── input_schemas[]
├── output_schemas[]
├── supported_domains[]
├── supported_languages[]
├── mechanism_class
│   ├── deterministic
│   ├── heuristic
│   ├── statistical
│   ├── local_model
│   ├── external_model
│   ├── agent
│   └── human
├── risk_class
├── privacy_class
├── cost_class
├── latency_class
├── expected_quality
├── evidence_level
├── required_context[]
├── required_capabilities[]
├── incompatible_capabilities[]
├── fallback_capabilities[]
├── policy_tags[]
├── activation_conditions[]
├── stop_conditions[]
├── evaluator_id
├── health_probe_id
├── status
│   ├── experimental
│   ├── shadow
│   ├── active
│   ├── degraded
│   ├── suspended
│   └── deprecated
└── provenance
```

Esse descriptor é **metadado operacional**, não implementação.

---

# 6. Health Registry

O **Health Registry** responde se uma capability está apta para uso naquele momento.

Saúde não é binária.

Estados iniciais:

```text
HEALTHY
DEGRADED
UNHEALTHY
UNKNOWN
SUSPENDED
```

Exemplo:

```text
CAP_RELATION_DISCOVERY
status = DEGRADED
reason = false_positive_rate_above_baseline
last_success = 2026-08-10T09:58:00-03:00
latency_p95 = 412ms
error_rate = 1.8%
quality_delta = -7.4%
recommended_action = restrict_to_low_risk
```

Uma capability pode estar tecnicamente disponível e cognitivamente degradada.

Essa distinção é central.

---

# 7. Health técnico ≠ Health cognitivo

O Eva Engine® deve separar pelo menos:

```text
TECHNICAL HEALTH
- processo responde?
- dependência está acessível?
- latência está aceitável?
- erro de execução está alto?

COGNITIVE HEALTH
- qualidade caiu?
- false positives subiram?
- confiança ficou mal calibrada?
- drift aumentou?
- challenger está rejeitando mais?
- output está divergindo do baseline?

ECONOMIC HEALTH
- custo por evento subiu?
- escalonamento para IA aumentou?
- ganho marginal caiu?
```

Assim, um componente pode estar:

```text
technical = HEALTHY
cognitive = DEGRADED
economic = UNHEALTHY
```

O Orchestrator deve conseguir agir sobre essa combinação.

---

# 8. O Orchestrator consulta, não adivinha

Fluxo desejado:

```text
EVENTO
  ↓
ORCHESTRATOR
  ↓
qual tarefa precisa ser resolvida?
  ↓
CAPABILITY REGISTRY
  ↓
quais candidatos sabem fazer?
  ↓
POLICY FILTER
  ↓
quais podem fazer neste contexto?
  ↓
HEALTH REGISTRY
  ↓
quais estão aptos agora?
  ↓
COST / LATENCY / QUALITY RANKING
  ↓
seleciona capability
  ↓
EXECUÇÃO
  ↓
TRACE + METRICS + EVIDENCE
```

Princípio:

> **Seleção é uma decisão explícita e auditável.**

---

# 9. Missing Capability Detection

Em um organismo grande, falha crítica não é apenas uma capability cair.

Pode ser **a capability necessária nem existir** para aquele evento.

Fluxo:

```text
TASK REQUIREMENT
      ↓
CAPABILITY QUERY
      ↓
nenhuma capability compatível
      ↓
MISSING_CAPABILITY
      ↓
Risk Assessment
      ↓
┌──────────────┬──────────────┬──────────────┐
▼              ▼              ▼
FALLBACK       ESCALATE       FAIL CLOSED
```

Regra:

> **Falha conhecida é preferível a sucesso aparente produzido sem a capacidade necessária.**

O supervisor deve gerar alerta quando uma peça crítica faltar, estiver degradada ou tiver sido removida por policy.

---

# 10. Fallback Graph

Fallback não deve ser uma lista improvisada.

Deve existir como grafo explícito:

```text
CAP_A
 ├── fallback_to → CAP_B
 │                  └── fallback_to → CAP_C
 └── escalate_to → SUPERVISORY_AI
```

Cada aresta deve declarar:

```text
allowed_when
quality_loss_expected
risk_change
cost_change
latency_change
requires_human?
```

Uma capability mais barata não é fallback válido se perder qualidade além do tolerado para o risco atual.

---

# 11. Capability Composition

Uma capability pode nascer da composição de outras.

Exemplo:

```text
CAP_CONTEXTUAL_INCIDENT_RECONSTRUCTION
        │
        ├── CAP_ENTITY_RESOLUTION
        ├── CAP_TEMPORAL_PARSE
        ├── CAP_EVENT_SEQUENCE
        ├── CAP_RETRIEVAL
        ├── CAP_RELATION_DISCOVERY
        └── CAP_EVIDENCE_ASSEMBLY
```

Isso materializa o princípio de crescimento exponencial por composição.

A capability composta deve possuir health próprio, além do health das dependências.

---

# 12. Dependency Graph

O Registry precisa conhecer dependências:

```text
CAP_X
  ↓ requires
CAP_Y
  ↓ requires
CAP_Z
```

Se `CAP_Z` falha, o Health Registry deve conseguir calcular impacto ascendente:

```text
CAP_Z = UNHEALTHY
   ↓
CAP_Y = DEGRADED
   ↓
CAP_X = DEGRADED / UNAVAILABLE
```

Isso é o equivalente arquitetural ao organismo perceber que uma pequena peça ausente afeta um sistema maior.

---

# 13. Supervisão e watchdogs

O sistema deve possuir watchers independentes do componente observado.

Exemplos:

```text
availability_watchdog
latency_watchdog
quality_watchdog
drift_watchdog
cost_watchdog
policy_watchdog
schema_compatibility_watchdog
```

Um componente não deve ser a única fonte sobre a própria saúde.

Princípio:

> **Quem executa não deve ser o único responsável por declarar que executou bem.**

---

# 14. Capability Promotion

Capabilities novas não entram diretamente como `active`.

Ciclo de maturidade:

```text
DRAFT
  ↓
EXPERIMENTAL
  ↓
SHADOW
  ↓
VALIDATED
  ↓
ACTIVE
  ↓
DEGRADED? / SUSPENDED?
  ↓
DEPRECATED
```

A passagem entre estados precisa considerar:

- testes;
- baseline;
- evaluator;
- holdout;
- fault injection quando aplicável;
- custo;
- segurança;
- privacidade;
- compatibilidade;
- rollback.

Capability aprendida ou alterada pelo Learning Plane continua sujeita ao **Learning Quarantine + Promotion Gate**.

---

# 15. Capabilities e Lentes

Uma Lente Cognitiva não é necessariamente uma capability executável.

```text
LENS
"como observar"

CAPABILITY
"o que o sistema sabe executar"

AGENT / MECHANISM
"quem/como executa"
```

Exemplo:

```text
LENS_TEMPORAL
      ↓ pode ativar
CAP_TEMPORAL_PARSE
CAP_SEQUENCE_ANALYSIS
CAP_RECENCY_WEIGHTING
```

Isso preserva a separação conceitual definida anteriormente.

---

# 16. Capabilities e agentes

Um agente pode implementar uma ou várias capabilities.

Uma capability pode possuir várias implementações.

```text
CAP_SUMMARIZE_INCIDENT
     ├── impl_local_rules
     ├── impl_small_model
     └── impl_external_llm
```

O Orchestrator seleciona a implementação conforme:

```text
quality
risk
privacy
cost
latency
health
policy
context
```

Isso impede acoplamento do contrato ao fornecedor.

---

# 17. Capability Economics

Para B2B enterprise, cada capability deve poder produzir métricas econômicas.

Exemplos:

```text
cost_per_call
cost_per_1k_events
compute_time
external_api_cost
cache_hit_rate
human_escalation_rate
ai_escalation_rate
value_proxy
quality_per_cost
```

Objetivo:

> **medir não apenas se uma capability funciona, mas se vale a pena usá-la naquela posição da cadeia.**

---

# 18. Exemplo de roteamento enterprise

```text
INCIDENT_EVENT
      │
      ▼
CAPABILITY QUERY
      │
      ├── CAP_RULE_TRIAGE        cost 1   health HEALTHY   quality 0.93
      ├── CAP_LOCAL_CLASSIFIER   cost 3   health HEALTHY   quality 0.96
      └── CAP_LLM_TRIAGE         cost 25  health HEALTHY   quality 0.97

Policy:
risk = LOW
required_quality = 0.92

Decision:
CAP_RULE_TRIAGE
```

Em outro caso:

```text
risk = HIGH
required_quality = 0.985

CAP_RULE_TRIAGE      insufficient
CAP_LOCAL_CLASSIFIER insufficient
CAP_LLM_TRIAGE       insufficient

→ escalate_to HUMAN_AUTHORITY
```

Não existe “modelo preferido”. Existe **requisito + evidência + custo + risco**.

---

# 19. Relação com o Cognitive Kernel

O Kernel conhece os contratos mínimos para consultar registries, mas não conhece o catálogo inteiro.

```text
KERNEL
  ↓ query
REGISTRY INTERFACE
  ↓
CAPABILITIES / SCHEMAS / HEALTH
```

O catálogo pode crescer de dezenas para milhares de capabilities sem o Kernel aumentar na mesma proporção.

Princípio:

> **O Kernel governa o mecanismo de descoberta; não carrega a lista do mundo.**

---

# 20. Invariantes v0.1

**DECISÃO APROVADA COMO BASE PARA TESTE**

1. Toda capability executável possui `capability_id` e versão.
2. Toda capability declara input/output compatíveis com schemas registrados.
3. O Orchestrator não deve depender de nomes de implementação específicos.
4. Health precisa ser consultável e pode diferenciar saúde técnica, cognitiva e econômica.
5. Capability crítica ausente ou degradada não pode ser ignorada silenciosamente.
6. Fallback precisa ser explícito e proporcional ao risco.
7. Dependências precisam ser rastreáveis.
8. Capabilities novas percorrem ciclo de maturidade antes de produção.
9. Learning Candidates não podem registrar/promover capability diretamente no Trusted Core.
10. Métricas de custo e qualidade fazem parte da governança enterprise.
11. Uma capability pode possuir múltiplas implementações intercambiáveis.
12. Um agente é executor; a capability é o contrato de capacidade.

---

# 21. Questões em aberto

- armazenamento físico inicial dos registries;
- formato final dos descriptors;
- taxonomia de `risk_class`, `cost_class` e `privacy_class`;
- frequência de health probes;
- composição do cognitive health score;
- política de circuit breaker;
- algoritmo de ranking de implementações;
- propagação de health por dependências;
- política de cache de registry;
- resolução de conflito entre capabilities equivalentes;
- formato do capability graph;
- critérios mínimos para `VALIDATED` e `ACTIVE`;
- limites para auto-degradação/auto-suspensão.

---

# 22. Frase de fundação

> **O organismo não precisa conhecer todas as células de memória. Precisa saber descobri-las, verificar se estão saudáveis, entender o que cada uma pode fazer e impedir que uma célula inadequada seja usada no lugar errado.**
