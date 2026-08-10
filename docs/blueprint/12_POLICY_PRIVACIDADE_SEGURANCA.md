# Eva Engine® — Policy, Privacidade e Segurança

**Status:** base arquitetural inicial

---

# 1. Objetivo

Separar claramente capacidade cognitiva de permissão operacional.

O motor pode compreender, inferir e sugerir. Isso não significa que está autorizado a executar qualquer ação externa.

---

# 2. Princípio de autorização

```text
Inference / Suggested Action
  ↓
Policy Evaluation
  ↓
Permission Check
  ↓
Adapter autorizado
  ↓
Execução externa
```

Sem política/permissão válida, nenhuma ação externa deve ocorrer.

---

# 3. Responsabilidades do Policy Engine

- autorização;
- escopo de dados;
- retenção;
- exclusão;
- compartilhamento;
- conteúdo sensível;
- execução de ações;
- isolamento entre usuários/tenants;
- limites de aprendizagem;
- limites de expansão cognitiva;
- providers externos permitidos.

---

# 4. Princípio de minimização

O motor deve processar apenas o necessário para a tarefa.

Exemplos:

- logs não precisam conter texto bruto completo;
- embeddings devem usar escopo correto;
- retrieval deve filtrar por usuário/tenant antes de similaridade ampla;
- adapters externos recebem apenas os dados necessários.

---

# 5. Conteúdo original

Preservar original não significa manter para sempre independentemente da vontade do usuário.

A política de retenção/exclusão será definida por produto e legislação aplicável.

O motor precisa permitir:

- localizar dados derivados por origem;
- invalidar/reprocessar derivados;
- excluir quando política exigir;
- evitar órfãos sem referência.

---

# 6. Isolamento

Desde o schema conceitual, preparar escopo:

```text
user_id
tenant_id
source_product
privacy_scope
```

Mesmo se a primeira versão for single-user, não criar atalhos que tornem isolamento futuro impossível.

---

# 7. Aprendizado individual

Perfil semântico individual é dado sensível do ponto de vista de privacidade porque revela padrões de linguagem/contexto.

Regras:

- não promover automaticamente para conhecimento global;
- não compartilhar entre usuários por conveniência;
- permitir reprocessamento/remoção;
- registrar proveniência;
- minimizar exposição em logs.

---

# 8. Embeddings/providers externos

Antes de enviar conteúdo a provider externo, avaliar:

- necessidade;
- consentimento/política;
- retenção do fornecedor;
- região;
- custo;
- dados sensíveis;
- possibilidade de execução local.

Arquitetura por provider deve permitir substituição.

---

# 9. Segredos

Nunca armazenar:

- tokens;
- API keys;
- passwords;
- service role keys

em código, dataset ou documentação versionada.

Usar secret store/variáveis de ambiente.

---

# 10. Logs

Logs técnicos devem preferir identificadores e métricas.

Exemplo:

```text
event_id
correlation_id
module
duration
atom_count
error_code
```

Texto bruto completo somente em ambiente controlado e quando realmente necessário para debug.

---

# 11. Profanidade e sensibilidade

Detectar não significa censurar.

Filtros podem produzir metadados usados pela política de produto.

O Policy Engine decide o que fazer com a classificação; a camada RAW permanece distinta.

---

# 12. Auditoria

Ações externas e mudanças importantes devem ser auditáveis.

Registrar:

```text
who
what
when
policy_decision
permission_source
adapter
result
```

---

# 13. Segurança por default

Princípios:

- deny by default para ações externas;
- menor privilégio;
- providers explicitamente configurados;
- validação de input;
- schemas versionados;
- idempotência em eventos;
- limites de custo e profundidade;
- proteção contra loops de automação.

---

# 14. Loops e autonomia

Nenhum evento interno deve gerar cadeia infinita.

A expansão cognitiva precisa de:

```text
max_depth
max_events
max_actions
time_budget
cost_budget
```

Ações externas podem exigir aprovação humana conforme produto/política.

---

# 15. Questões em aberto

- modelo de autorização;
- multi-tenant isolation físico;
- estratégia de encryption-at-rest adicional;
- retenção de event log;
- política de exclusão de embeddings;
- residência de dados;
- níveis de sensibilidade;
- auditoria administrativa;
- política de promoção de conhecimento global.
