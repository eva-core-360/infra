# Eva Engine® — Enterprise Integration Boundary v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** definir a membrana entre o Eva Engine® e ambientes corporativos externos, garantindo que ERP, CRM, logs, documentos, sensores, agentes, APIs, filas, humanos e sistemas terceiros entrem e saiam por contratos explícitos, isolados, auditáveis e governados.

---

# 1. Definição

O Eva Engine® não deve permitir que sistemas externos “falem com o Core” diretamente.

Toda integração atravessa uma **Enterprise Integration Boundary**.

```text
ENTERPRISE SYSTEMS
ERP · CRM · DB · logs · docs · APIs · sensors · agents · humans
                          │
                          ▼
╔══════════════════════════════════════════════════════════════╗
║              ENTERPRISE INTEGRATION BOUNDARY               ║
║                                                              ║
║ authenticate · authorize · normalize · map · validate       ║
║ deduplicate · classify · scope · provenance · rate-limit    ║
║                                                              ║
╚═══════════════════════════╤══════════════════════════════════╝
                            │
                            ▼
                   COGNITIVE ENVELOPE
                            │
                            ▼
                    EVA TRUSTED FABRIC
```

Princípio:

> **Integração é uma membrana de tradução e proteção, não um atalho para dentro do Core.**

---

# 2. Anti-Corruption Layer

Termo arquitetural real e apropriado: **Anti-Corruption Layer (ACL)**.

A ACL impede que modelos de dados externos contaminem a linguagem interna do Eva Engine®.

Exemplo:

```text
SAP field: VBELN
Salesforce object: Opportunity
ServiceNow record: incident
Kafka event: machine_fault
custom ERP field: COD_MOV_17
```

Nenhum desses nomes precisa existir no Cognitive Kernel.

A Boundary traduz para contratos internos estáveis:

```text
Event
Entity
State
Time
Relation
Evidence
ActionRequest
```

---

# 3. Adapter ≠ Domain Pack

```text
ADAPTER
como conversar com um sistema externo

DOMAIN PACK
como interpretar conceitos específicos de um domínio
```

Exemplo:

```text
SAP Adapter
    ↓
normaliza evento
    ↓
Supply Chain Domain Pack
    ↓
interpreta significado de negócio
```

O Core não deve conhecer SAP nem “supply chain” como requisito universal.

---

# 4. Ingress Contract

Entrada corporativa deve ser convertida para evento versionado.

Contrato conceitual:

```text
IngressRecord
├── ingress_id
├── source_system
├── source_tenant
├── source_object_id?
├── source_event_id?
├── ingestion_mode
├── received_at
├── occurred_at?
├── actor?
├── auth_context
├── source_trust
├── schema_mapping_id
├── privacy_class
├── retention_class
├── idempotency_key
├── payload_ref / payload
└── provenance
```

Após validação:

```text
IngressRecord
      ↓
Schema Mapping
      ↓
Canonical Event
      ↓
Cognitive Envelope
```

---

# 5. Modos de ingestão

A Boundary deve suportar múltiplos padrões sem alterar o Core.

```text
SYNCHRONOUS API
WEBHOOK
MESSAGE QUEUE
EVENT STREAM
CHANGE DATA CAPTURE
BATCH
FILE DROP
SCHEDULED PULL
MANUAL IMPORT
HUMAN ENTRY
```

A implementação inicial pode suportar poucos modos, mas o contrato deve evitar acoplamento.

---

# 6. Source Trust

Fonte autenticada não significa conteúdo verdadeiro.

Separar:

```text
AUTHENTICATION TRUST
quem enviou?

TRANSPORT INTEGRITY
foi alterado no caminho?

SOURCE RELIABILITY
essa fonte costuma ser confiável?

CONTENT VALIDITY
o conteúdo é consistente?

EPISTEMIC STATUS
o que sabemos sobre a afirmação?
```

Princípio:

> **“Veio do ERP” é provenance, não prova automática de verdade.**

---

# 7. Tenant Boundary

Toda integração enterprise precisa resolver escopo antes de processamento cognitivo.

```text
REQUEST
   ↓
AUTHENTICATE
   ↓
RESOLVE TENANT
   ↓
RESOLVE DATA SCOPE
   ↓
POLICY CHECK
   ↓
ADMIT
```

Se tenant/scope não puder ser determinado de forma confiável:

```text
QUARANTINE / REJECT
```

Nunca “default tenant”.

---

# 8. Identity Mapping

Sistemas distintos podem representar a mesma entidade com IDs diferentes.

```text
CRM customer_id = 481
ERP customer_code = ACME-003
Support org_id = 9921
```

A Boundary pode produzir referências candidatas para Entity Resolution, mas não deve fundir identidades silenciosamente.

```text
ExternalIdentityRef
├── source_system
├── external_id
├── entity_type_hint?
├── tenant_id
├── mapping_confidence?
└── provenance
```

Fusão real pertence a capability de Entity Resolution + Evidence Model.

---

# 9. Schema Mapping

Cada integração usa mapeamento versionado.

```text
source_schema
      ↓
Mapping v3
      ↓
canonical_schema
```

Registrar:

```text
mapping_id
source_schema_version
canonical_schema_version
transform_rules_version
introduced_at
status
compatibility
```

Mudança no sistema externo não deve quebrar silenciosamente o Core.

---

# 10. Validation Pipeline

```text
RAW EXTERNAL INPUT
      │
      ▼
AUTH / SIGNATURE
      │
      ▼
SIZE / FORMAT LIMITS
      │
      ▼
SCHEMA VALIDATION
      │
      ▼
TENANT / SCOPE
      │
      ▼
IDEMPOTENCY / DEDUP
      │
      ▼
SECURITY SCAN / POLICY
      │
      ▼
NORMALIZATION
      │
      ▼
PROVENANCE STAMP
      │
      ▼
CANONICAL EVENT
```

Falhas devem possuir classe e destino explícitos.

---

# 11. Idempotency

Integrações reais repetem eventos.

Reentrega não pode produzir duplicação cognitiva silenciosa.

Chaves possíveis:

```text
source_system
+
source_event_id
+
tenant_id
```

ou idempotency key fornecida.

A deduplicação deve distinguir:

```text
same delivery
same event
same content
similar event
```

Somente os primeiros casos autorizam dedup determinístico simples.

---

# 12. Ordering e Late Events

Eventos podem chegar fora de ordem.

```text
E3 chegou
E1 chegou depois
E2 chegou por replay
```

A arquitetura deve preservar:

```text
occurred_at
received_at
source_sequence?
causation_id?
correlation_id
```

O motor não deve assumir que ordem de chegada é ordem do mundo.

---

# 13. Backfill e Replay

Empresas podem integrar anos de histórico.

Backfill precisa ser modo explícito:

```text
LIVE
BACKFILL
REPLAY
REPROCESS
SHADOW
```

Policies diferentes podem controlar:

- custo;
- velocidade;
- profundidade cognitiva;
- emissão de ações;
- learning eligibility;
- external AI use.

Backfill histórico não deve disparar ações externas como se fosse evento novo de produção.

---

# 14. Data Minimization

A Boundary deve reduzir exposição antes de chamar providers externos quando possível.

Exemplos:

```text
full payload
   ↓
extract required fields
   ↓
redact / tokenize / pseudonymize when policy allows
   ↓
external provider
```

Não enviar conteúdo completo por conveniência se o requisito usa apenas 3 campos.

---

# 15. Sensitive Data Classification

Classificação de sensibilidade precisa acompanhar o envelope.

Taxonomia inicial candidata:

```text
PUBLIC
INTERNAL
CONFIDENTIAL
RESTRICTED
HIGHLY_RESTRICTED
```

Categorias regulatórias específicas pertencem a policy/domain packs.

Essa classificação influencia:

- provider permitido;
- região;
- logging;
- retention;
- retrieval;
- human access;
- external AI.

---

# 16. Egress Boundary

Saída também precisa de membrana.

```text
COGNITIVE RESULT
      ↓
ACTION REQUEST / OUTPUT REQUEST
      ↓
POLICY
      ↓
DATA MINIMIZATION
      ↓
SCHEMA / DESTINATION MAPPING
      ↓
ADAPTER
      ↓
EXTERNAL SYSTEM
```

Nenhuma capability cognitiva deve chamar ERP/CRM diretamente como arquitetura padrão.

---

# 17. ActionRequest

Contrato conceitual:

```text
ActionRequest
├── action_id
├── action_type
├── target_system
├── target_ref
├── payload_ref
├── tenant_id
├── requested_by
├── evidence_refs[]
├── confidence?
├── risk_class
├── reversibility_class
├── policy_context
├── idempotency_key
└── trace_id
```

A autorização vem depois da intenção.

---

# 18. Human-in-the-loop

Humano pode ser:

```text
source
reviewer
approver
executor
escalation authority
feedback provider
```

Esses papéis devem ser distintos.

“Humano aprovou” precisa registrar:

```text
who
what
scope
when
policy
evidence shown
version
```

---

# 19. Integration Health

Cada adapter possui health próprio:

```text
availability
latency
error_rate
schema_mismatch_rate
replay_rate
duplicate_rate
late_event_rate
auth_failure_rate
cost
data_quality indicators
```

Uma integração tecnicamente online pode estar semanticamente degradada por schema drift.

---

# 20. Dead Letter / Quarantine

Eventos que não podem ser admitidos não devem desaparecer.

Destinos conceituais:

```text
REJECTED
QUARANTINED
DEAD_LETTER
RETRYABLE
MANUAL_REVIEW
```

Cada classe precisa de motivo auditável.

---

# 21. Rate Limits e Quotas

Uma origem comprometida ou mal configurada não pode consumir o organismo inteiro.

Limites por:

```text
tenant
source
adapter
event_type
capability path
cost budget
external AI budget
```

Integração participa de backpressure e circuit breakers.

---

# 22. Enterprise Integration Registry

Considerar registry lógico:

```text
IntegrationDescriptor
├── integration_id
├── tenant_id
├── source_system
├── adapter_version
├── supported_event_types[]
├── source_schemas[]
├── mapping_versions[]
├── allowed_scopes[]
├── auth_method
├── data_classes[]
├── ingestion_modes[]
├── egress_actions[]
├── health_probe_id
├── policy_tags[]
├── rate_limits
├── status
└── provenance
```

---

# 23. Enterprise Integration não vira microserviço obrigatório

Boundary é uma responsabilidade lógica.

A primeira implementação pode ser um pacote modular no mesmo deploy.

Separação física surge quando:

- escala justificar;
- segurança exigir;
- tenant isolation exigir;
- blast radius exigir;
- operação justificar.

---

# 24. Exemplo enterprise

```text
ERP: payment.failed
      │
      ▼
ERP ADAPTER
      │ authenticate + schema map
      ▼
INTEGRATION BOUNDARY
      │ tenant + scope + idempotency
      ▼
CANONICAL EVENT
      │
      ▼
COGNITIVE ENVELOPE
      │
      ▼
ORCHESTRATOR
      │
      ├── temporal
      ├── entity resolution
      ├── recurrence
      ├── context
      └── evidence
      │
      ▼
RESULT / HYPOTHESIS
      │
      ▼
possible ActionRequest
      │
      ▼
POLICY + APPROVAL
      │
      ▼
ERP ADAPTER
```

---

# 25. Invariantes v0.1

1. Sistema externo não acessa Cognitive Kernel diretamente.
2. Todo ingress enterprise resolve tenant/scope antes de admissão.
3. Adapter traduz transporte; Domain Pack traduz significado.
4. Modelo externo não contamina schema interno.
5. Schema mappings são versionados.
6. Reentrega precisa ser idempotente onde aplicável.
7. Ordem de chegada não é presumida como ordem temporal real.
8. Backfill/replay não executa ações de produção por padrão.
9. Source authentication não equivale a truth.
10. Ações externas passam por Egress Boundary + Policy.
11. Dados são minimizados antes de provider externo quando possível.
12. Eventos rejeitados/quarentenados possuem motivo rastreável.
13. Integration Health inclui schema/data quality, não só uptime.
14. Rate limits e quotas protegem o organismo por tenant/source.
15. Integrações são substituíveis sem alterar identidade do Core.

---

# 26. Questões em aberto

- primeiro protocolo de integração da v0 executável;
- auth model inicial;
- segredo/credential store;
- primeira taxonomia de sensibilidade;
- estratégia multi-tenant física;
- estratégia de CDC;
- fila/event bus inicial;
- DLQ física;
- schema registry implementation;
- data residency;
- retention por classe;
- integração com SIEM/auditoria;
- política de backfill;
- limites default por tenant;
- assinatura de webhooks;
- encryption key strategy.

---

# 27. Frases de fundação

> **A empresa não entra no Core. Ela atravessa uma membrana que traduz, limita, autentica e deixa rastro.**

> **Adapter conhece o sistema externo; Domain Pack conhece o domínio; o Kernel não precisa conhecer nenhum dos dois.**
