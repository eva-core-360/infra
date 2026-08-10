# Eva Engine® — Roadmap de Implementação

**Objetivo:** transformar o Blueprint em software real sem tentar construir a plataforma inteira de uma vez.

---

# Estratégia geral

A implementação deve seguir ciclos curtos:

```text
especificar
  ↓
criar casos de teste
  ↓
implementar
  ↓
medir
  ↓
ajustar
```

A primeira versão deve ser pequena, observável e testável.

---

# Fase 0 — Fundação do repositório

## Entregáveis

- Blueprint Mestre
- Registro de Decisões
- Contexto de Continuidade
- Ontologia v0
- Catálogo de Eventos v0
- `AGENTS.md`
- estrutura inicial de código
- CI básica

## Critério de conclusão

Novo chat/agente consegue entender o projeto sem depender da conversa original.

---

# Fase 1 — Eva Engine v0.1: coração mínimo

## Objetivo

Receber uma entrada textual simples e produzir resultado estruturado rastreável.

## Capacidades

1. receber evento `content.created`;
2. gerar `event_id`;
3. preservar RAW;
4. detectar idioma inicial;
5. normalizar sinais básicos;
6. atomizar um conjunto pequeno de tipos;
7. classificar com confiança;
8. persistir resultado;
9. registrar versões;
10. expor saída de debug.

## Átomos sugeridos para primeira implementação

- Observation
- Question
- Intention
- Decision
- Task
- Hypothesis
- Temporal

A lista pode mudar após formalização da Ontologia v0.

## Critério de conclusão

Um conjunto de golden tests multilíngues passa de forma reproduzível.

---

# Fase 2 — v0.2: relações e continuidade

## Objetivo

Fazer o motor reconhecer que uma entrada pode continuar ou se relacionar com memórias anteriores.

## Capacidades

- geração de candidatos;
- relações simples;
- `continues`;
- `related_to`;
- relações temporais;
- confidence scoring para relações;
- persistência de links;
- rejeição/correção pelo usuário.

## Critério de conclusão

Casos conhecidos de continuidade são detectados sem comparar tudo com tudo.

---

# Fase 3 — v0.3: memória semântica

## Objetivo

Encontrar memórias semanticamente próximas mesmo com vocabulário diferente.

## Capacidades

- interface `EmbeddingProvider`;
- geração de embedding;
- armazenamento vetorial;
- busca top-k;
- filtros por usuário/tenant/contexto;
- limiar mínimo de similaridade;
- logs de candidatos.

## Critério de conclusão

O motor recupera memórias semanticamente próximas em dataset controlado com boa precisão.

---

# Fase 4 — v0.4: perfil adaptativo

## Objetivo

Aprender significados e correções particulares do usuário.

## Capacidades

- eventos de feedback;
- perfil semântico individual;
- pesos de sinais;
- fast learning;
- histórico de correções;
- explicabilidade de ajuste.

## Critério de conclusão

Após uma sequência de correções controladas, previsões futuras melhoram no dataset daquele perfil sem alterar o comportamento global.

---

# Fase 5 — v0.5: expansão cognitiva controlada

## Objetivo

Permitir ativação em cadeia sem explosão combinatória.

## Capacidades

- `max_depth`;
- `max_candidates`;
- `minimum_confidence`;
- `time_budget`;
- `cost_budget`;
- rastreio de árvore de ativação;
- cancelamento/stop conditions.

## Critério de conclusão

O motor consegue revelar relações de segunda ordem dentro de limites determinísticos de custo e tempo.

---

# Fase 6 — v0.6: gravidade cognitiva

## Objetivo

Transformar atividade e continuidade em sinais de massa/atenção.

## Capacidades

- massa por átomo;
- agregação por assunto;
- agregação por área;
- tendência;
- velocidade;
- função temporal;
- explicação técnica do score.

## Critério de conclusão

O mesmo histórico produz o mesmo score com a mesma versão/configuração e mudanças de comportamento produzem movimentos esperados nos testes.

---

# Fase 7 — Eva Memory alpha

## Objetivo

Consumir o motor em uma experiência real de notas/memória.

## Interface inicial sugerida

- captura rápida;
- Home Cognitiva;
- 13 áreas-base;
- até 2 áreas personalizadas;
- assuntos/contextos;
- “continuar de onde parou”;
- indicador de atividade/tendência;
- correção simples de classificação.

## Critério de conclusão

Usuário consegue escrever sem organizar manualmente cada registro, corrigir quando necessário e perceber melhora progressiva do sistema.

---

# Fase 8 — Generalização por Domain Packs

Somente depois do primeiro domínio funcionar.

Possíveis provas:

- Projects Pack;
- CRM Pack;
- Education Pack.

Objetivo: demonstrar que o Core é realmente reutilizável e identificar acoplamentos escondidos com o Eva Memory®.

---

# Regra de prioridade

Sempre priorizar, nesta ordem:

1. preservação e integridade;
2. contratos e rastreabilidade;
3. testes;
4. atomização útil;
5. continuidade;
6. aprendizagem;
7. expansão;
8. gravidade;
9. sofisticação visual.

---

# O que significa “motor inteligente” neste roadmap

Não é quantidade de IA generativa.

É capacidade crescente de:

- interpretar corretamente;
- lembrar contexto;
- encontrar continuidade;
- aprender com correções;
- reduzir organização manual;
- explicar tecnicamente o que fez;
- continuar previsível e reversível.
