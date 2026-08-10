# Eva Engine® — Registro de Decisões

**Objetivo:** registrar decisões arquiteturais vigentes de forma curta e rastreável.

Este arquivo não substitui o Blueprint Mestre. Ele funciona como índice rápido das decisões aprovadas.

---

## D-001 — O Core é generalista

**Status:** aprovada  
**Decisão:** Eva Engine® não nasce como motor de notas. Eva Memory® é o primeiro produto consumidor.

**Consequência:** conceitos exclusivos de notas devem ficar no Domain Pack `memory` ou no produto.

---

## D-002 — Evento é a unidade universal de entrada

**Status:** aprovada  
**Decisão:** o Core recebe eventos, não “notas” como abstração fundamental.

---

## D-003 — Original é preservado

**Status:** aprovada  
**Decisão:** conteúdo original nunca é sobrescrito pelo motor.

---

## D-004 — Separação epistemológica

**Status:** aprovada  
**Decisão:** distinguir RAW, DERIVED, INFERRED e LEARNED.

---

## D-005 — Inferências possuem confiança

**Status:** aprovada  
**Decisão:** resultado inferido não deve ser tratado como certeza silenciosa.

---

## D-006 — Rastreabilidade e reversibilidade

**Status:** aprovada  
**Decisão:** classificações e relações importantes devem registrar origem/versão/evidência; correções não apagam histórico.

---

## D-007 — Aprendizado individual separado do global

**Status:** aprovada  
**Decisão:** o que a Eva aprende sobre um usuário não redefine automaticamente o conhecimento geral do motor.

---

## D-008 — Uso é sinal de aprendizagem

**Status:** aprovada  
**Decisão:** correções, confirmações, relações, retomadas, buscas e outros sinais alimentam aprendizagem; sinais explícitos têm maior força.

---

## D-009 — Multilíngue por arquitetura

**Status:** aprovada  
**Decisão:** o Core semântico deve ser independente do idioma; idiomas entram por Language Packs.

---

## D-010 — Profanidade não é censura automática

**Status:** aprovada  
**Decisão:** palavrões são preservados no original e podem ser classificados tecnicamente, sem equivaler automaticamente a negatividade.

---

## D-011 — Motor orientado a eventos

**Status:** aprovada  
**Decisão:** o motor deve reagir a eventos e voltar ao estado ocioso; não manter “IA pensando” permanentemente sem necessidade.

---

## D-012 — Expansão Cognitiva Controlada

**Status:** aprovada como princípio  
**Decisão:** relações em cadeia precisam de limites de profundidade, candidatos, confiança, tempo, custo e escopo.

---

## D-013 — Mecânica não é interface

**Status:** aprovada  
**Decisão:** gravidade, relações e proximidade podem existir nos bastidores sem grafo visual.

---

## D-014 — Home Cognitiva / Ranking Vivo como direção mobile

**Status:** hipótese forte de produto  
**Decisão atual:** priorizar lista dinâmica de áreas e indicadores de movimento em vez de grafo obrigatório.

---

## D-015 — 13 áreas-base + até 2 personalizadas

**Status:** aprovada como base atual do Eva Memory®  
**Decisão:** 13 áreas universais, “EU” fora da contagem, com até duas áreas personalizadas.

---

## D-016 — Domain Packs

**Status:** aprovada  
**Decisão:** conhecimento específico de domínio estende o Core sem contaminá-lo.

---

## D-017 — Schema Registry

**Status:** aprovada como capacidade necessária  
**Decisão:** tipos universais e extensões de domínio devem ser registrados por schema.

---

## D-018 — Policy Engine

**Status:** aprovada como capacidade necessária  
**Decisão:** ações externas, privacidade, permissões, retenção e limites passam por políticas explícitas.

---

## D-019 — Core interpreta; adapters executam

**Status:** aprovada  
**Decisão:** integrações externas não devem ser incorporadas diretamente ao núcleo cognitivo.

---

## D-020 — Monólito modular primeiro

**Status:** aprovada  
**Decisão:** iniciar com separação modular forte e implantação simples; microserviços somente quando justificados.

---

## D-021 — TypeScript como linguagem principal inicial

**Status:** aprovada como direção atual  
**Decisão:** TypeScript no Core/API inicialmente; Python entra apenas se ML/NLP especializado justificar.

---

## D-022 — PostgreSQL/Supabase como persistência inicial

**Status:** aprovada como direção atual  
**Decisão:** usar PostgreSQL e aproveitar Supabase; vetores podem começar no próprio Postgres.

---

## D-023 — Providers intercambiáveis

**Status:** aprovada  
**Decisão:** embeddings, IA/NLP e serviços externos devem ser abstraídos por interfaces quando houver risco de lock-in.

---

## D-024 — Dataset versionado desde o início

**Status:** aprovada  
**Decisão:** dataset de atomização, relações, ambiguidades, idiomas, profanidade e correções faz parte do produto tecnológico.

---

## D-025 — Testes antes de “parece inteligente”

**Status:** aprovada  
**Decisão:** comportamento cognitivo deve ser mensurável por testes unitários, linguísticos, regressão e golden tests.

---

## D-026 — Versionamento cognitivo

**Status:** aprovada  
**Decisão:** resultados relevantes devem registrar versões de engine, ontologia, language pack, regras e modelo semântico quando aplicável.

---

## D-027 — Cursor implementa o Blueprint

**Status:** aprovada  
**Decisão:** Cursor/agentes são ferramentas de execução e aceleração; não são autoridade arquitetural silenciosa.

---

## D-028 — GitHub como fonte persistente de continuidade

**Status:** aprovada  
**Decisão:** documentação vigente do Blueprint deve permanecer versionada neste repositório para permitir continuidade entre chats e agentes.

---

# Decisões ainda não fechadas

- ontologia v0 final;
- relações v0 finais;
- fórmula de confiança;
- fórmula de gravidade;
- decaimento temporal;
- provider inicial de embeddings;
- fila/background job implementation;
- isolamento multi-tenant;
- idiomas da primeira versão executável além de pt-BR;
- limites numéricos iniciais da expansão cognitiva.
