# Eva Engine® — Modelo de Dados Conceitual v0

**Status:** base conceitual; não é ainda migration final

---

# 1. Objetivo

Definir entidades de persistência suficientes para implementar o primeiro motor sem acoplar o schema ao Eva Memory®.

---

# 2. Tabelas/coleções conceituais

## `events`

Representa eventos recebidos ou gerados pelo motor.

Campos candidatos:

```text
id
schema_version
event_type
source
actor_type
actor_id
tenant_id
occurred_at
correlation_id
causation_id
payload
status
engine_version
created_at
```

---

## `raw_objects`

Preserva conteúdo original ou referência a ele.

Campos candidatos:

```text
id
source_event_id
content_type
raw_text
raw_uri
content_hash
language_hint
privacy_scope
created_at
```

Regra: interpretações não sobrescrevem esta camada.

---

## `atoms`

```text
id
atom_type
source_event_id
raw_object_id
content
source_start
source_end
classification_confidence
statement_certainty
status
engine_version
ontology_version
language_pack_version
created_at
```

`statement_certainty` ainda é hipótese de schema.

---

## `entities`

```text
id
entity_type
canonical_label
scope_id
metadata
created_at
updated_at
```

Aliases podem ficar em tabela própria.

---

## `entity_aliases`

```text
id
entity_id
alias
language
context_id
confidence
source
created_at
```

Útil para personalização semântica.

---

## `relations`

```text
id
relation_type
source_object_type
source_object_id
target_object_type
target_object_id
confidence
status
created_by
engine_version
created_at
```

---

## `relation_evidence`

```text
id
relation_id
evidence_type
source_reference
weight
metadata
```

---

## `contexts`

```text
id
context_type
parent_context_id
scope_id
label
metadata
created_at
```

Permite hierarquia de contexto sem obrigar pasta física.

---

## `feedback_events`

```text
id
target_type
target_id
feedback_type
predicted_value
corrected_value
actor_id
context_snapshot
engine_version
created_at
```

---

## `learning_profile_rules`

```text
id
scope_id
rule_type
pattern
context_selector
target
support_count
reject_count
weight
confidence
last_seen_at
created_at
updated_at
```

---

## `inferences`

```text
id
inference_type
claim
confidence
status
scope_id
engine_version
created_at
```

---

## `inference_evidence`

```text
id
inference_id
evidence_type
object_type
object_id
weight
```

---

## `semantic_vectors`

Quando embeddings entrarem:

```text
id
object_type
object_id
provider
model_version
vector
scope_id
created_at
```

---

## `cognitive_scores`

Quando gravidade entrar:

```text
id
object_type
object_id
score_type
score
trend
velocity
formula_version
calculated_at
```

---

# 3. Proveniência

Todo objeto derivado deve apontar para sua origem direta ou evidências suficientes para reconstruir a cadeia.

Exemplo:

```text
raw_object
  ↓
atom
  ↓
relation
  ↓
inference
```

Proveniência é requisito, não detalhe opcional.

---

# 4. Status e supersedência

Objetos derivados podem precisar de estados:

```text
active
rejected
superseded
invalidated
```

Ao reprocessar, preferir supersedência/versionamento a apagar imediatamente interpretação anterior, quando auditoria justificar.

---

# 5. IDs

Usar IDs opacos e globalmente únicos.

Formato final ainda será escolhido.

Possíveis prefixos para debug:

```text
evt_
raw_
atm_
ent_
rel_
ctx_
inf_
fbk_
```

Prefixos são conveniência, não requisito fechado.

---

# 6. Multi-tenant readiness

Mesmo na v0, schemas centrais devem aceitar escopo.

Evitar queries sem filtro de escopo em retrieval semântico.

Índices e RLS serão definidos quando schema físico for implementado.

---

# 7. JSON vs colunas

Regra sugerida:

- dados consultados/filtrados frequentemente → colunas tipadas;
- metadata experimental/extensível → JSON;
- não esconder todo o schema em JSON por conveniência.

---

# 8. Event log vs state tables

Não adotar Event Sourcing completo automaticamente.

Manter eventos suficientes para rastreabilidade e aprendizagem, enquanto estado atual pode viver em tabelas próprias.

Se event sourcing integral se tornar necessário, decidir por requisito real.

---

# 9. Exclusão e cascata

A política final deve impedir derivados órfãos.

Quando RAW é removido por política, derivados associados precisam ser:

- excluídos;
- anonimizados;
- invalidados;

conforme regra definida.

Não definir cascade destrutivo final antes do Policy Engine físico.

---

# 10. Próximo passo

Transformar este modelo conceitual em:

- schemas TypeScript;
- validação runtime;
- migrations PostgreSQL;
- índices;
- RLS/políticas;
- fixtures de teste.

Somente após Ontologia v0 e Eventos v0 estabilizarem o suficiente.
