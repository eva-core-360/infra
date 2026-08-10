# Eva Engine® — Atomic / Cognitive Envelope v1.0

**Status:** base arquitetural vigente para refinamento e testes  
**Função:** definir o contrato universal de circulação dos objetos cognitivos do Eva Engine®: identidade, escopo, lineage, provenance, integridade, confiança operacional, política, versionamento e rastreabilidade sem acoplar o envelope a produto, domínio, idioma ou mecanismo específico.

---

# 1. Definição

O **Atomic / Cognitive Envelope** é o invólucro operacional que acompanha eventos, átomos, sinais, evidências, relações, hipóteses, inferências, resultados, derivados e candidatos de aprendizagem enquanto circulam pelo organismo.

Ele não representa o conteúdo em si.

Ele representa **as condições sob as quais aquele conteúdo pode existir, circular, ser utilizado, derivado, promovido, revogado ou reprocessado**.

Princípio:

> **Nenhum artefato cognitivo relevante circula sem identidade, escopo, origem e lineage suficientes para ser auditado.**

---

# 2. O problema que o Envelope resolve

Sem um envelope universal, cada capability tende a inventar seus próprios metadados:

```text
módulo A usa source_id
módulo B usa parent
módulo C usa origin
módulo D esquece tenant
módulo E não registra versão
módulo F não registra evidência
```

Isso destrói auditabilidade e torna correção em cascata quase impossível.

O Envelope cria um contrato transversal:

```text
WHO AM I?
WHERE DID I COME FROM?
WHO PRODUCED ME?
WHICH SCOPE DO I BELONG TO?
WHAT VERSION PRODUCED ME?
WHAT IS MY EPISTEMIC LEVEL?
WHAT IS MY TRUST STATE?
WHAT IS MY INTEGRITY STATE?
WHICH POLICIES APPLY?
WHO DESCENDS FROM ME?
CAN I BE USED HERE?
```

---

# 3. Envelope não é Payload

**DECISÃO APROVADA COMO PRINCÍPIO**

Separar estritamente:

```text
ENVELOPE
controle, identidade, governança, lineage

PAYLOAD
conteúdo semântico ou referência para conteúdo
```

Diagrama:

```text
┌───────────────────────────────────────────────┐
│              COGNITIVE ENVELOPE               │
│                                               │
│ identity · scope · lineage · trust · policy   │
│ integrity · version · trace · timestamps      │
│                                               │
│    ┌─────────────────────────────────────┐    │
│    │              PAYLOAD                │    │
│    │                                     │    │
│    │ atom / evidence / relation / claim  │    │
│    │ event / signal / result / etc.      │    │
│    └─────────────────────────────────────┘    │
└───────────────────────────────────────────────┘
```

O Kernel deve conseguir validar e rotear o Envelope sem precisar compreender semanticamente todo o Payload.

---

# 4. Duas camadas para não engordar o organismo

Em escala enterprise, não é aceitável duplicar dezenas de metadados pesados em bilhões de artefatos.

O Envelope será concebido em duas camadas lógicas:

```text
CORE ENVELOPE
metadados mínimos de circulação
sempre presentes quando exigidos pelo schema

EXTENDED METADATA
provenance detalhada
trace completo
evidence ledger
policy decisions
cost metrics
model diagnostics
security attestations
armazenados por referência quando apropriado
```

Princípio:

> **Rastreabilidade não exige duplicação indiscriminada. O Envelope carrega identidade e ponteiros suficientes para reconstruir o contexto completo.**

---

# 5. Core Envelope v1

Contrato conceitual inicial:

```text
CognitiveEnvelopeV1
├── object_id
├── object_type
├── schema_id
├── schema_version
│
├── root_event_id
├── parent_id?
├── correlation_id
├── causation_id?
├── trace_id
│
├── tenant_id
├── scope_id
├── domain_scope?
│
├── created_at
├── observed_at?
├── valid_from?
├── valid_until?
│
├── provenance_ref
├── produced_by
├── version_vector_ref
│
├── epistemic_level
├── trust_state
├── integrity_state
│
├── policy_context_ref
├── data_classification
├── retention_class?
│
├── content_hash?
├── idempotency_key?
│
├── evidence_refs[]?
├── lineage_refs[]?
│
└── payload_ref | payload
```

O schema final poderá compactar ou especializar campos, mas essas responsabilidades precisam permanecer representáveis.

---

# 6. Identidade

Todo objeto relevante precisa de identidade estável.

```text
object_id
object_type
schema_id
schema_version
```

Regras:

1. `object_id` identifica a instância, não o significado abstrato.
2. `object_type` é extensível via Schema Registry.
3. `schema_id + schema_version` define a forma interpretável daquele objeto.
4. Identidade não deve depender de label de UI ou nome de produto.

Exemplo:

```text
object_id   = art_01J...
object_type = EVIDENCE_ITEM
schema_id   = eva.evidence.item
version     = 1
```

---

# 7. Root, Parent, Correlation e Causation

Esses conceitos não devem ser fundidos.

```text
root_event_id
origem operacional da árvore cognitiva

parent_id
pai estrutural/derivacional imediato quando houver

correlation_id
agrupa objetos pertencentes à mesma operação ou investigação

causation_id
objeto/evento cuja ocorrência disparou diretamente este novo objeto
```

Exemplo:

```text
EVENT E1
  ↓
ATOM A1
  ↓
RELATION R1
  ↓
HYPOTHESIS H1
```

Todos podem compartilhar:

```text
root_event_id = E1
correlation_id = C77
```

mas cada um possui `parent_id` / `causation_id` próprios.

Isso evita usar um único campo `parent` para representar relações diferentes.

---

# 8. Scope e isolamento

**DECISÃO APROVADA COMO INVARIANTE ENTERPRISE**

O Envelope deve carregar escopo suficiente para impedir mistura silenciosa entre tenants, organizações, usuários, domínios ou contextos protegidos.

Campos conceituais:

```text
tenant_id
scope_id
domain_scope?
policy_context_ref
```

Regra:

> **Nenhuma capability pode retirar um artefato do seu escopo autorizado apenas porque semanticamente ele parece relevante.**

Cross-scope ou cross-tenant access exige autorização explícita e rastreável.

---

# 9. Provenance

**Provenance** responde de onde a informação veio e quais transformações relevantes participaram de sua existência.

O Envelope não precisa carregar todo o histórico inline.

Pode carregar:

```text
provenance_ref
produced_by
lineage_refs[]
```

Registro de provenance estendido pode conter:

```text
source_system
source_record_id
source_uri?
ingestion_method
actor?
capability_id
capability_version
implementation_id
model_id?
model_version?
lens_id?
agent_id?
transformation_chain[]
received_at
```

Princípio:

> **Origem não é apenas “qual banco”. É a cadeia necessária para explicar como aquele artefato chegou ao estado atual.**

---

# 10. `produced_by` é obrigatório para derivados

Todo objeto DERIVED, INFERRED ou LEARNED precisa declarar quem o produziu.

`produced_by` deve apontar para mecanismo identificável, por exemplo:

```text
CAP_TEMPORAL_PARSE@1.3.0
CAP_RELATION_DISCOVERY@2.1.4
AGENT_CHALLENGER@0.8
HUMAN_REVIEW@policy-17
```

Saída de IA externa não recebe autoridade especial.

Ela continua sendo resultado de uma capability versionada.

---

# 11. Três eixos ortogonais

O Envelope preserva os três eixos definidos no Cognitive Kernel.

## 11.1 Epistemic Level

```text
RAW
DERIVED
INFERRED
LEARNED
```

Responde:

> qual é a natureza epistemológica deste objeto?

## 11.2 Trust State

```text
UNVERIFIED
CANDIDATE
PROMOTED
SUPERSEDED
REVOKED
```

Responde:

> qual autoridade operacional este objeto conquistou?

## 11.3 Integrity State

```text
CLEAN
SUSPECT
QUARANTINED
TAINTED
INVALIDATED
REQUIRES_RECOMPUTE
```

Responde:

> há problema conhecido na integridade deste objeto ou em sua ancestralidade?

Exemplo válido:

```text
Epistemic = INFERRED
Trust     = PROMOTED
Integrity = CLEAN
```

Outro:

```text
Epistemic = LEARNED
Trust     = CANDIDATE
Integrity = QUARANTINED
```

Os três eixos nunca devem ser comprimidos em um único campo `status`.

---

# 12. Imutabilidade de origem e evolução de estado

O conteúdo original e a identidade histórica não devem ser silenciosamente reescritos.

Quando algo muda:

```text
SUPERSEDE
REVOKE
INVALIDATE
RECOMPUTE
PROMOTE
```

preferir eventos/records de transição ou uma nova versão logicamente vinculada ao objeto anterior.

Princípio:

> **Corrigir não é apagar a história; é registrar uma nova verdade operacional sobre ela.**

---

# 13. Integridade e tamper evidence

Quando aplicável, o Envelope pode carregar:

```text
content_hash
payload_hash
signature_ref?
checksum?
```

Objetivos:

- detectar corrupção;
- verificar que o payload referenciado não mudou silenciosamente;
- apoiar auditoria;
- permitir comparação/replay.

Assinatura criptográfica não é obrigatória para todo objeto na v1.

Ela pode ser exigida por policy em domínios ou fronteiras de maior risco.

---

# 14. Idempotência

Ingestão enterprise frequentemente recebe retries e eventos duplicados.

O Envelope deve permitir:

```text
idempotency_key
source_event_id
content_hash
```

para que uma capability possa distinguir:

```text
retry legítimo
duplicata exata
novo evento semanticamente parecido
```

Princípio:

> **Repetir transporte não deve criar realidade nova automaticamente.**

---

# 15. Temporalidade

O sistema precisa separar:

```text
created_at
quando o objeto foi criado no Eva Engine®

observed_at
quando o fenômeno foi observado

valid_from / valid_until
intervalo em que a informação é considerada aplicável
```

Exemplo:

Um contrato pode ser ingerido hoje, ter sido assinado ontem e entrar em vigor no mês que vem.

Um único `timestamp` não representa corretamente esses três tempos.

---

# 16. Data Classification e Privacy

O Envelope deve carregar classificação mínima de dados quando aplicável.

Taxonomia final é questão em aberto, mas precisa representar algo como:

```text
PUBLIC
INTERNAL
CONFIDENTIAL
RESTRICTED
SENSITIVE
```

Pode existir classificação adicional por domínio/regulação.

O ponto principal é arquitetural:

> **Privacy e data handling precisam viajar com o artefato; não podem depender apenas da memória de quem o está processando.**

`data_classification` e `policy_context_ref` ajudam o Orchestrator a eliminar capabilities incompatíveis antes da execução.

---

# 17. Evitar vazamento por metadados

Metadados também podem conter informação sensível.

Portanto:

- não copiar PII para labels de trace sem necessidade;
- não usar conteúdo bruto em IDs;
- não incluir segredos em `policy_tags`;
- não duplicar payload sensível dentro de logs;
- preferir referências opacas quando possível;
- aplicar retenção também a traces e provenance.

Princípio:

> **Envelope seguro não significa apenas proteger o Payload.**

---

# 18. Evidence References

Nem todo artefato precisa possuir evidência.

Quando possuir:

```text
evidence_refs[]
```

aponta para Evidence Items registrados.

Uma inferência pode dizer:

```text
artifact H17
  ↓ evidence_refs
E01
E04
E09
```

Sem copiar toda a evidência dentro da inferência.

Isso permite revogação e blast radius:

```text
E04 revoked
   ↓
find dependent artifacts
   ↓
H17 becomes challenged / requires_recompute
```

---

# 19. Lineage References

`lineage_refs[]` representa relações de derivação e ancestralidade, não relações semânticas genéricas.

Exemplos:

```text
DERIVED_FROM
INFERRED_FROM
GENERATED_BY
SUPPORTED_BY
INVALIDATES
SUPERSEDES
REQUIRES_RECOMPUTE
```

Relações semânticas como `RELATED_TO` ou `CAUSES` pertencem ao modelo cognitivo, não necessariamente ao lineage estrutural.

Essa separação evita confundir:

```text
"foi produzido a partir de"
```

com:

```text
"tem relação semântica com"
```

---

# 20. Version Vector

O Envelope não deve repetir dezenas de versões inline se isso for caro.

Pode carregar:

```text
version_vector_ref
```

apontando para:

```text
engine_version
kernel_version
schema_version
ontology_version
policy_version
capability_versions{}
model_versions{}
language_pack_versions{}
domain_pack_versions{}
```

Objetivo:

> **nenhum resultado relevante deve existir sem possibilidade de saber qual configuração tecnológica o produziu.**

---

# 21. Trace e Observability

Todo processamento relevante deve possuir:

```text
trace_id
```

Opcionalmente:

```text
span_id
parent_span_id
```

quando a implementação de observabilidade exigir granularidade distribuída.

O Envelope aponta para o trace; o trace não precisa ser duplicado no objeto.

O trace pode registrar:

```text
capabilities chamadas
latência
retries
fallbacks
escalations
cost
warnings
policies
health snapshots
```

---

# 22. Budget Context

Budget pertence primariamente ao Processing Context / Orchestrator, não a cada artefato.

Porém o Envelope deve permitir correlação com a execução que o produziu por `trace_id`, `causation_id` e referências de contexto.

Evitar copiar continuamente:

```text
cost_budget
compute_budget
max_depth
max_waves
```

em cada derivado se eles puderem ser recuperados pelo contexto da execução.

Princípio:

> **O Envelope deve ser suficiente para reconstrução, não uma cópia integral do mundo.**

---

# 23. Envelope por tipo de objeto

Nem todos os campos são obrigatórios em todo artefato.

O Schema Registry define perfis.

Exemplo:

```text
EVENT_ENVELOPE_PROFILE
required:
  object_id
  object_type
  tenant_id
  scope_id
  schema
  provenance_ref
  created_at
  trace_id
  payload

INFERENCE_ENVELOPE_PROFILE
required:
  object_id
  root_event_id
  tenant_id
  scope_id
  produced_by
  epistemic_level=INFERRED
  trust_state
  integrity_state
  evidence_refs
  lineage_refs
  version_vector_ref
  trace_id

LEARNING_CANDIDATE_PROFILE
required:
  ...
  trust_state=CANDIDATE
  integrity_state
  lineage_refs
  training_evidence_refs
  evaluation_refs
```

Isso evita um único schema gigantesco e cheio de campos vazios.

---

# 24. Envelope e Explosão Atômica

A Explosão Atômica depende do Envelope para não perder ancestralidade.

```text
WAVE 0
EVENT E1
  │
  ▼
WAVE 1
A1 · A2 · A3
  │
  ▼
WAVE 2
R1 · R2 · H1
  │
  ▼
WAVE 3
EVIDENCE · COUNTER-EVIDENCE
```

Todos preservam:

```text
root_event_id = E1
correlation_id = C1
trace_id = T1
```

mas possuem identidades e pais distintos.

Assim a expansão é grande sem virar amnésia estrutural.

---

# 25. Envelope e Learning Quarantine

Learning Candidate precisa circular com marcação inequívoca.

```text
Epistemic = LEARNED
Trust     = CANDIDATE
Integrity = CLEAN | SUSPECT | QUARANTINED
```

Ele não pode alterar estado promovido apenas mudando o próprio campo `trust_state`.

A promoção exige um evento/artefato autorizado pelo **Promotion Gate**.

Fluxo:

```text
LEARNING CANDIDATE
       │
       ▼
QUARANTINE
       │
       ▼
EVALUATION
       │
       ▼
PROMOTION DECISION
       │
       ▼
NEW PROMOTED ARTIFACT / STATE
```

---

# 26. Envelope e Integrity Propagation

Quando um ancestral muda para:

```text
TAINTED
INVALIDATED
REVOKED
```

o sistema precisa conseguir localizar descendentes.

```text
ANCESTOR X
  ↓
LINEAGE INDEX
  ↓
D1
D2
D3
  ↓
mark / assess
  ↓
SUSPECT / TAINTED / REQUIRES_RECOMPUTE
```

A propagação exata depende de policy e relação de lineage.

Nem todo descendente precisa ser automaticamente invalidado.

Mas nenhum descendente crítico deve ignorar silenciosamente a revogação de sua base.

---

# 27. Envelope e Orchestration

O Orchestrator usa o Envelope para Admission Control.

```text
ARTIFACT ARRIVES
      │
      ▼
SCHEMA VALID?
      │
SCOPE ALLOWED?
      │
INTEGRITY ACCEPTABLE?
      │
TRUST SUFFICIENT?
      │
POLICY ALLOWS?
      │
      ▼
ELIGIBLE FOR PLAN
```

A capability recebe apenas artefatos compatíveis com seu contrato e policy.

---

# 28. Envelope e external AI

Antes de enviar qualquer payload para um modelo externo, o Orchestrator/Policy deve poder inspecionar:

```text
data_classification
privacy_scope
policy_context_ref
tenant_id
purpose
```

Fluxo:

```text
ARTIFACT
   │
   ▼
EXTERNAL_AI_REQUEST
   │
   ▼
POLICY CHECK
   │
   ├── DENY
   ├── REDACT / MINIMIZE
   ├── REQUIRE APPROVAL
   └── ALLOW
```

A decisão precisa ficar no trace.

---

# 29. Envelope e Human Authority

Revisão humana também precisa ser rastreável.

Se um humano:

```text
confirma
corrige
rejeita
promove
revoga
```

isso gera evento/artefato com:

```text
actor_ref
policy_context
trace_id
reason?
created_at
```

Autoridade humana não deve aparecer no sistema como mutação invisível de banco.

---

# 30. Compatibilidade e evolução

O Envelope v1 precisa evoluir sem quebrar o organismo.

Princípios:

1. campos novos preferencialmente opcionais até migração controlada;
2. breaking changes exigem nova major version;
3. Schema Registry declara compatibilidade;
4. consumidores não devem interpretar campos desconhecidos como erro fatal quando policy/schema permitir forward compatibility;
5. artefatos históricos preservam schema/version usados na época;
6. migração não reescreve silenciosamente o original.

---

# 31. Performance e envelope budget

O próprio Envelope precisa de orçamento.

Métricas futuras:

```text
avg_envelope_bytes
p95_envelope_bytes
metadata_to_payload_ratio
lineage_lookup_latency
provenance_lookup_latency
trace_lookup_latency
index_write_cost
```

Objetivo:

> **Rastreabilidade enterprise sem imposto cognitivo e financeiro descontrolado.**

Se um metadado pesado puder ser referenciado com segurança, preferir referência a duplicação.

---

# 32. Invariantes v1.0

**DECISÃO APROVADA COMO BASE PARA TESTE**

1. Todo artefato relevante possui identidade estável e schema versionado.
2. Todo artefato pertence a um tenant/scope explícito quando operando em ambiente multi-tenant.
3. Todo derivado declara `produced_by` e ancestralidade mínima.
4. `epistemic_level`, `trust_state` e `integrity_state` são dimensões separadas.
5. Payload e Envelope são responsabilidades distintas.
6. O original não é sobrescrito para “corrigir” uma interpretação.
7. Cross-scope access exige autorização explícita.
8. Learning Candidate não pode se promover alterando metadado localmente.
9. Revogação de ancestral crítico precisa ser propagável via lineage.
10. Score não deve ser colocado em `confidence` sem calibração válida.
11. Repetição de transporte não deve criar novo fato quando idempotência indicar retry.
12. Provenance e versionamento precisam ser recuperáveis mesmo quando armazenados por referência.
13. O Envelope não deve duplicar indiscriminadamente trace, evidence ou provenance pesados.
14. Metadados também obedecem privacy, retenção e classificação.
15. Toda saída externa de alto risco precisa manter correlação suficiente com a decisão de policy que a autorizou.
16. O Envelope deve permanecer neutro de produto, domínio, idioma e fornecedor.

---

# 33. Testes mínimos do Envelope

Antes de considerá-lo executável, testar:

```text
T01 — rejeitar schema incompatível
T02 — impedir cross-tenant involuntário
T03 — reconstruir árvore de lineage
T04 — calcular descendentes de artefato revogado
T05 — detectar retry por idempotency key
T06 — preservar original após correção
T07 — diferenciar RAW / INFERRED / LEARNED
T08 — diferenciar CANDIDATE / PROMOTED
T09 — diferenciar CLEAN / TAINTED
T10 — recuperar Version Vector
T11 — recuperar Provenance completa por referência
T12 — policy negar external AI para classificação incompatível
T13 — reprocessar derivado sem perder root_event_id
T14 — suportar bilhões de IDs sem colisão prática no mecanismo escolhido
T15 — medir overhead médio/p95 do Envelope
T16 — garantir que metadata/logging não replique payload sensível indevidamente
```

A implementação concreta de IDs, hashing, assinatura e storage será escolhida posteriormente.

---

# 34. O que ainda NÃO está decidido

- formato físico final (`JSON`, protobuf, MessagePack ou combinação);
- mecanismo de geração de IDs;
- algoritmo de hash padrão;
- uso e escopo de assinaturas digitais;
- taxonomia final de `data_classification`;
- política de retenção por classe;
- storage/index do lineage;
- storage/index de provenance;
- forma física do Version Vector;
- compatibilidade com tracing distribuído específico;
- compressão/compactação de envelopes;
- envelope mínimo para hot path de altíssimo volume;
- estratégia de archival para artefatos frios;
- política final de causalidade `parent_id` versus `causation_id` por tipo de objeto.

Nenhuma dessas questões deve ser fechada apenas por preferência tecnológica.

---

# 35. Frase de fundação

> **No Eva Engine®, inteligência pode se fragmentar bilhões de vezes; identidade, origem e responsabilidade não podem se perder uma única vez.**

E uma segunda regra operacional:

> **O Envelope não carrega o mundo. Ele carrega o suficiente para provar onde o mundo daquele artefato pode ser reconstruído.**
