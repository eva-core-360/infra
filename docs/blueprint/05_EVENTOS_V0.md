# Eva Engine® — Catálogo de Eventos v0

**Status:** base inicial para validação  
**Objetivo:** definir o que “acorda” o motor e padronizar o envelope mínimo dos eventos.

---

# 1. Princípio

O Eva Engine® é orientado a eventos.

Evento significa:

> algo aconteceu e o motor recebeu informação suficiente para decidir quais módulos precisam processar essa mudança.

O motor não deve ficar executando raciocínio contínuo sem necessidade.

---

# 2. Envelope canônico de evento

Proposta v0:

```json
{
  "event_id": "evt_...",
  "event_type": "content.created",
  "schema_version": "1.0",
  "source": "eva_memory",
  "actor": {
    "type": "user",
    "id": "usr_..."
  },
  "tenant_id": "tnt_...",
  "timestamp": "2026-08-10T00:00:00Z",
  "correlation_id": "cor_...",
  "causation_id": null,
  "payload": {}
}
```

Campos:

- `event_id`: identificador único;
- `event_type`: tipo do evento;
- `schema_version`: versão do contrato;
- `source`: produto/adapter que emitiu;
- `actor`: quem/que originou;
- `tenant_id`: escopo de isolamento quando aplicável;
- `timestamp`: quando ocorreu;
- `correlation_id`: agrupa eventos do mesmo fluxo;
- `causation_id`: evento que causou este evento, quando houver;
- `payload`: conteúdo específico.

**Questão em aberto:** quais campos serão obrigatórios na primeira implementação single-user e quais entram apenas quando multi-tenant for ativado.

---

# 3. Eventos externos v0

## E01 — `content.created`

Novo conteúdo textual ou multimodal foi criado por um produto consumidor.

Payload inicial possível:

```json
{
  "content_id": "cnt_...",
  "content_type": "text",
  "text": "Decidi trocar de fornecedor amanhã."
}
```

Pipeline provável:

```text
preserve raw
→ language
→ normalize
→ atomize
→ classify
→ context
→ retrieve
→ relate
→ persist
```

---

## E02 — `content.updated`

Conteúdo existente foi alterado.

Requisitos:

- preservar histórico de versão;
- não apagar silenciosamente interpretações anteriores;
- avaliar quais átomos/relações ficaram obsoletos;
- gerar nova versão derivada.

---

## E03 — `content.deleted`

Produto consumidor removeu/solicitou remoção do conteúdo.

**Questão em aberto:** política exata entre exclusão lógica, retenção e exclusão física. Deve passar pelo Policy Engine.

---

## E04 — `content.reopened`

Usuário voltou a abrir conteúdo anterior.

Natureza do sinal:

- implícito;
- peso baixo isoladamente;
- pode reforçar atividade quando recorrente.

---

## E05 — `content.continued`

Produto ou usuário declarou continuidade explícita de conteúdo anterior.

Esse é um sinal forte para `REL_CONTINUES`.

---

## E06 — `classification.corrected`

Usuário corrigiu uma classificação feita pelo motor.

Payload conceitual:

```json
{
  "target_id": "atm_...",
  "predicted": "ATOM_INTENTION",
  "corrected_to": "ATOM_TASK"
}
```

Peso de aprendizado: alto.

---

## E07 — `classification.confirmed`

Usuário confirmou classificação sugerida.

Peso de aprendizado: alto, porém possivelmente menor que correção explícita dependendo da UX.

---

## E08 — `relation.created`

Usuário/produto criou relação explícita entre objetos.

Pode ser sinal forte de aprendizagem contextual.

---

## E09 — `relation.removed`

Usuário removeu/rejeitou relação existente.

Se a relação foi inferida pelo motor, isso é importante sinal negativo.

---

## E10 — `context.changed`

Usuário/produto mudou área, assunto, projeto ou outro contexto de uma memória.

Pode alimentar perfil semântico individual.

---

## E11 — `search.performed`

Busca foi realizada.

Sinal implícito. Não interpretar uma busca isolada como importância forte.

---

## E12 — `memory.archived`

Memória/conteúdo foi arquivado no produto.

Isso altera estado do produto; não significa automaticamente “sem importância”.

---

## E13 — `task.completed`

Evento generalista de conclusão de ação.

Mostra por que o Core não pode depender de notas.

Pode vir de Eva Memory®, projetos ou outro produto.

---

# 4. Eventos internos v0

Eventos internos são emitidos pelo próprio motor para desacoplar módulos e permitir observabilidade.

## I01 — `atom.created`

Novo átomo foi produzido.

## I02 — `atom.updated`

Átomo foi reprocessado/ajustado.

## I03 — `relation.discovered`

Motor encontrou relação candidata/aceita.

## I04 — `relation.rejected`

Relação candidata não atingiu critério ou foi rejeitada.

## I05 — `inference.created`

Nova inferência foi registrada.

## I06 — `learning.updated`

Perfil adaptativo recebeu atualização relevante.

## I07 — `gravity.changed`

Score de ativação/massa sofreu mudança suficiente para gerar evento.

## I08 — `processing.completed`

Pipeline terminou.

Pode carregar métricas:

```text
duration_ms
atoms_created
relations_evaluated
relations_accepted
inferences_created
```

## I09 — `processing.failed`

Falha de processamento técnico.

Deve conter referência de erro sem vazar conteúdo sensível desnecessariamente nos logs.

---

# 5. Eventos temporais/sistêmicos

Nem tudo depende de ação imediata do usuário.

Candidatos:

```text
time.window_elapsed
learning.recalibration_requested
memory.reprocessing_requested
policy.retention_due
```

Esses eventos ainda serão formalizados depois da v0.

---

# 6. Idempotência

**Decisão recomendada para implementação:** processamento de eventos deve suportar idempotência.

Se `event_id` já foi processado com sucesso, reentrega não deve duplicar átomos e relações.

Isso será importante para filas e retries.

---

# 7. Correlation e causation

Para rastrear a expansão cognitiva:

```text
content.created (evt_1)
  ↓ causa
atom.created (evt_2)
  ↓ causa
relation.discovered (evt_3)
```

Todos podem compartilhar:

```text
correlation_id = cor_A
```

E cada filho registra:

```text
causation_id = evento_pai
```

Isso permitirá reconstruir por que o motor chegou a determinada conclusão.

---

# 8. Prioridade de processamento

Hipótese inicial:

## Alta prioridade / usuário esperando

```text
content.created
classification.corrected
content.updated
```

## Background

```text
relation discovery profundo
expansão cognitiva
slow learning
reprocessamento
recalibração de gravidade ampla
```

---

# 9. Regra de emissão

Não transformar qualquer alteração interna trivial em evento persistido se isso gerar ruído ou custo sem valor.

Critério futuro:

- evento de domínio importante → persistir;
- telemetria técnica → log/metric quando suficiente;
- mudança irrelevante de score → não emitir `gravity.changed`.

---

# 10. Próximos passos

Formalizar em documentos futuros:

- schema JSON/TypeScript dos envelopes;
- tabela de quais módulos escutam quais eventos;
- política de retry;
- Dead Letter Queue quando houver fila;
- versionamento de schema de eventos;
- segurança de payload;
- retenção de event log.
