# Eva Engine® — Stack e Ferramentas

**Status:** direção inicial, sujeita a validação técnica

---

# 1. Objetivo

Escolher ferramentas que permitam construir rápido agora sem comprometer a possibilidade de evolução do motor.

Princípios:

- poucas dependências;
- modularidade;
- baixo lock-in;
- observabilidade;
- bom suporte a testes;
- compatibilidade com Cursor;
- facilidade de deploy;
- custo inicial controlado.

---

# 2. Linguagem principal

## TypeScript

Direção inicial aprovada.

Motivos:

- tipagem forte suficiente para schemas/eventos;
- excelente ecossistema para APIs;
- bom compartilhamento de tipos entre SDK/backend;
- boa experiência com Cursor/agentes;
- ampla compatibilidade com Node e runtimes edge;
- facilita manter o primeiro sistema em uma única stack.

Python não é obrigatório na v0.

Se surgir necessidade real de NLP/ML especializado, criar serviço isolado:

```text
eva-ml-worker
```

---

# 3. Arquitetura de código

## Monólito modular

Começar com módulos bem separados no mesmo repositório/runtime.

Estrutura sugerida:

```text
apps/
  api/
  worker/

packages/
  core/
  schemas/
  events/
  language/
  atomizer/
  context/
  semantic/
  relations/
  learning/
  policy/
  gravity/

domain-packs/
  memory/
```

Microserviços entram apenas quando escala, isolamento ou tecnologia específica justificar.

---

# 4. Persistência

## PostgreSQL

Banco principal inicial.

## Supabase

Plataforma candidata/preferida na fase inicial por já oferecer PostgreSQL gerenciado e recursos úteis ao ecossistema do produto.

Evitar usar recursos proprietários no Core sem abstração quando isso dificultar portabilidade futura.

---

# 5. Vetores

Começar com extensão vetorial no PostgreSQL quando embeddings entrarem.

Vantagens:

- uma infraestrutura a menos;
- joins com metadata/contexto;
- backup único;
- operação mais simples.

Banco vetorial separado somente se métricas reais mostrarem necessidade.

---

# 6. API

Primeiro contrato externo: HTTP/REST.

Possíveis endpoints:

```text
POST /v1/events
POST /v1/process
POST /v1/feedback
GET  /v1/memories/:id
GET  /v1/relations/:id
```

A API deve delegar para serviços do Core, não conter regras cognitivas diretamente nos controllers.

---

# 7. SDK

Futuro:

```text
@eva/sdk
```

Objetivo:

```text
eva.process(event)
eva.feedback(...)
```

Sem expor detalhes internos do pipeline.

---

# 8. Background jobs

Separar trabalho síncrono e assíncrono.

Síncrono:

- persistência RAW;
- validação;
- atomização/classificação leve;
- resposta rápida ao produto.

Assíncrono:

- relações profundas;
- embeddings em lote;
- expansão cognitiva;
- slow learning;
- reprocessamento;
- recalibração.

Interface abstrata sugerida:

```text
JobQueue
```

Provider concreto fica para decisão posterior.

---

# 9. Cloudflare

Pode ser utilizado para API/edge/workers/filas se fizer sentido operacional.

Regra:

- não espalhar dependências específicas do fornecedor dentro do Core;
- encapsular integração em adapters/providers.

---

# 10. GitHub

Fonte de verdade para:

- Blueprint;
- código;
- issues;
- pull requests;
- CI/CD;
- releases;
- histórico de decisões.

Branch principal atual: `main`.

Estratégia de branches pode evoluir conforme equipe/automação crescer.

---

# 11. Cursor

Cursor é ferramenta de construção assistida.

Deve ler:

- `AGENTS.md`;
- Blueprint Mestre;
- documento do módulo;
- testes existentes.

Fluxo ideal:

```text
spec
→ tests
→ implementation
→ review
```

Evitar prompts genéricos como “crie um motor inteligente”.

Preferir tarefas pequenas e verificáveis.

---

# 12. Schemas

Usar schemas tipados e versionados.

Opções a avaliar na implementação:

- TypeScript types/interfaces;
- biblioteca de validação runtime;
- JSON Schema para contratos externos.

Critério: evitar duplicação desnecessária de definição.

---

# 13. Testes

Runner TypeScript será escolhido na criação do código.

Necessidades:

- unit;
- integration;
- golden dataset;
- regression;
- property-based quando útil;
- performance para expansão/retrieval.

---

# 14. Logs e observabilidade

Logs estruturados em JSON desde o início.

Campos candidatos:

```text
correlation_id
event_id
module
engine_version
duration_ms
result_count
confidence_summary
error_code
```

Nunca logar conteúdo pessoal completo por padrão.

---

# 15. Segurança de segredos

Segredos nunca entram no repositório.

Usar variáveis de ambiente/secret stores.

Criar `.env.example` apenas com nomes de variáveis e exemplos não sensíveis.

---

# 16. CI/CD

GitHub Actions candidata para:

```text
lint
format
typecheck
tests
golden tests
build
migration validation
```

Deploy automático somente após a primeira estrutura estável.

---

# 17. Dependências externas

Toda dependência cognitiva importante deve responder:

1. o Core consegue funcionar sem ela?
2. existe interface para substituição?
3. quais dados saem do ambiente?
4. qual custo por volume?
5. qual impacto de latência?
6. qual política de retenção do fornecedor?

---

# 18. Ferramentas ainda a escolher

- framework HTTP;
- biblioteca runtime schema validation;
- provider de fila;
- provider inicial de embeddings;
- tracing/metrics platform;
- migration tool se não for a solução padrão escolhida;
- estratégia de secrets em produção.

Não decidir por moda; decidir na hora em que o requisito estiver claro.
