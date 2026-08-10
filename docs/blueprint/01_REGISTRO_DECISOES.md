# Eva Engine® — Registro de Decisões

**Objetivo:** registrar decisões arquiteturais vigentes de forma curta e rastreável.

Este arquivo não substitui o Blueprint Mestre. Ele funciona como índice rápido das decisões aprovadas.

---

## D-001 — O Core é generalista
**Status:** aprovada  
**Decisão:** Eva Engine® não nasce como motor de notas. Eva Memory® é produto consumidor/laboratório; conceitos exclusivos de produto ficam fora do Core.

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
**Decisão:** classificações e relações importantes registram origem/versão/evidência; correções não apagam histórico necessário.

---

## D-007 — Aprendizado individual separado do global
**Status:** aprovada  
**Decisão:** o que a Eva aprende sobre um usuário/tenant não redefine automaticamente conhecimento global.

---

## D-008 — Uso é sinal de aprendizagem
**Status:** aprovada  
**Decisão:** correções, confirmações, relações, retomadas, buscas e outros sinais podem alimentar aprendizagem; sinais explícitos têm maior força.

---

## D-009 — Multilíngue por arquitetura
**Status:** aprovada  
**Decisão:** o Core semântico é independente do idioma; idiomas entram por Language Packs.

---

## D-010 — Profanidade não é censura automática
**Status:** aprovada  
**Decisão:** palavrões são preservados no original e podem ser classificados tecnicamente sem equivaler automaticamente a negatividade.

---

## D-011 — Motor orientado a eventos
**Status:** aprovada  
**Decisão:** o motor reage a eventos e volta ao estado ocioso; não mantém IA pensando permanentemente sem necessidade.

---

## D-012 — Expansão Cognitiva Controlada
**Status:** aprovada como princípio  
**Decisão:** relações em cadeia precisam de limites de profundidade, candidatos, confiança, tempo, custo, risco e escopo.

---

## D-013 — Mecânica não é interface
**Status:** aprovada  
**Decisão:** gravidade, relações e proximidade podem existir nos bastidores sem grafo visual obrigatório.

---

## D-014 — Home Cognitiva / Ranking Vivo
**Status:** hipótese forte de produto  
**Decisão atual:** direção de produto, não princípio do Core.

---

## D-015 — 13 áreas-base + até 2 personalizadas
**Status:** aprovada como base atual do Eva Memory®  
**Decisão:** pertence ao Domain Pack/produto, não ao Eva Core.

---

## D-016 — Domain Packs
**Status:** aprovada  
**Decisão:** conhecimento específico de domínio estende o Core sem contaminá-lo.

---

## D-017 — Schema Registry
**Status:** aprovada como capacidade necessária  
**Decisão:** tipos universais e extensões de domínio são registrados por schema e versão.

---

## D-018 — Policy Engine
**Status:** aprovada como capacidade necessária  
**Decisão:** ações externas, privacidade, permissões, retenção e limites passam por políticas explícitas.

---

## D-019 — Core interpreta; adapters executam
**Status:** aprovada  
**Decisão:** integrações externas não são incorporadas diretamente ao núcleo cognitivo.

---

## D-020 — Monólito modular primeiro
**Status:** aprovada  
**Decisão:** iniciar com separação modular forte e implantação simples; microserviços somente quando justificados.

---

## D-021 — TypeScript como linguagem principal inicial
**Status:** aprovada como direção atual  
**Decisão:** TypeScript no Core/API inicialmente; Python entra quando ML/NLP especializado justificar.

---

## D-022 — PostgreSQL/Supabase como persistência inicial
**Status:** aprovada como direção atual  
**Decisão:** usar PostgreSQL/Supabase inicialmente; vetores podem começar no próprio Postgres.

---

## D-023 — Providers intercambiáveis
**Status:** aprovada  
**Decisão:** embeddings, IA/NLP e serviços externos são abstraídos por interfaces quando houver risco de lock-in.

---

## D-024 — Dataset versionado desde o início
**Status:** aprovada  
**Decisão:** datasets de comportamento cognitivo fazem parte do produto tecnológico.

---

## D-025 — Testes antes de “parece inteligente”
**Status:** aprovada  
**Decisão:** comportamento cognitivo precisa ser mensurável por testes, regressão, holdout e golden datasets quando aplicável.

---

## D-026 — Versionamento cognitivo
**Status:** aprovada  
**Decisão:** resultados relevantes registram versões de engine, ontologia, schema, regras, capabilities e modelos quando aplicável.

---

## D-027 — Cursor implementa o Blueprint
**Status:** aprovada  
**Decisão:** Cursor/agentes são ferramentas de execução e aceleração; não são autoridade arquitetural silenciosa.

---

## D-028 — GitHub como fonte persistente de continuidade
**Status:** aprovada  
**Decisão:** documentação vigente permanece versionada neste repositório privado para continuidade entre chats e agentes.

---

## D-029 — Nascer pequeno na implementação, não na arquitetura
**Status:** aprovada  
**Decisão:** a primeira versão executável pode ser pequena; o espaço arquitetural deve nascer preparado para múltiplos domínios, produtos e capacidades.

---

## D-030 — Crescimento exponencial por composição
**Status:** aprovada  
**Decisão:** crescimento significa multiplicar capacidades por composição de módulos, schemas, registries, Domain Packs, idiomas, memória e aprendizagem; não crescimento descontrolado de custo.

---

## D-031 — Aprendizado contínuo supervisionado e governado
**Status:** aprovada  
**Decisão:** o motor pode aprender continuamente; promoção de mudanças duradouras é versionada, mensurável, rastreável e reversível.

---

## D-032 — Quatro níveis de aprendizagem
**Status:** aprovada como estrutura de referência  
**Decisão:** distinguir sessão/contexto, individual/tenant, domínio e global, com exigências crescentes de avaliação e supervisão.

---

## D-033 — Capability Registry
**Status:** aprovada  
**Decisão:** capacidades são descobertas por contrato e versão; produtos/orquestradores não presumem implementações silenciosamente.

---

## D-034 — Evaluators são parte da arquitetura
**Status:** aprovada  
**Decisão:** melhoria cognitiva precisa ser demonstrada contra baseline; evaluators fazem parte do ciclo de evolução.

---

## D-035 — Hierarquia interna extensível
**Status:** aprovada  
**Decisão:** o Core não impõe profundidade fixa de produto; suporta hierarquias extensíveis e relações transversais.

---

## D-036 — O motor não se auto-modifica sem governança
**Status:** aprovada  
**Decisão:** aprendizado contínuo não autoriza alteração silenciosa de código, ontologia global ou políticas críticas.

---

## D-037 — Foco vigente é o motor, não o produto de notas
**Status:** aprovada  
**Decisão:** protótipos de notas são laboratórios/evidência; o objeto do Blueprint é o Eva Engine® como infraestrutura cognitiva generalista.

---

## D-038 — Ambição empresarial sem alegação prematura
**Status:** aprovada como direção estratégica  
**Decisão:** o motor é arquitetado com horizonte B2B enterprise e alto impacto econômico; ROI/capacidade só são afirmados com prova apropriada.

---

## D-039 — Escada de evidência
**Status:** aprovada  
**Decisão:** distinguir E0 ideia, E1 prova de mecanismo, E2 bateria reproduzível, E3 escala sintética, E4 piloto de domínio, E5 prova operacional e E6 prova econômica.

---

## D-040 — Três escalas independentes
**Status:** aprovada  
**Decisão:** separar escala operacional, cognitiva e de domínio. Sucesso em uma não comprova as demais.

---

## D-041 — Fase privada de P&D
**Status:** aprovada para a fase atual  
**Decisão:** documentação, datasets, intenção experimental e resultados permanecem privados salvo decisão explícita de divulgação.

---

## D-042 — Hipóteses precisam de definição operacional
**Status:** aprovada  
**Decisão:** termos como inteligência, aprendizado, confiança, escala e economia exigem definição operacional, baseline e teste adequado.

---

## D-043 — Learning Quarantine isolado do Trusted Core
**Status:** aprovada  
**Decisão:** Learning Candidates, heurísticas candidatas e derivados experimentais não escrevem diretamente no Trusted Core; promoção ocorre por Promotion Gate rastreável, versionado e reversível.

---

## D-044 — Atomic/Cognitive Envelope obrigatório para artefatos relevantes
**Status:** aprovada como princípio  
**Decisão:** átomos e derivados relevantes circulam com identidade, provenance, scope, lineage, versões, trust/integrity state e policy suficiente para auditoria e recuperação.

---

## D-045 — Cognitive Kernel mínimo e neutro
**Status:** aprovada  
**Decisão:** o Kernel conhece identidade, escopo, envelopes, eventos, estados, lineage, policy gates, traces, budgets, versões, integridade e invocation contracts; detalhes de domínio, idioma, agente, lente, modelo e fornecedor permanecem fora.

---

## D-046 — Score não é Confidence
**Status:** aprovada  
**Decisão:** score de mecanismo não pode ser tratado como probabilidade/confiança calibrada sem método apropriado. Signal, Evidence, Claim/Hypothesis, Score, Confidence e Decision permanecem separados.

---

## D-047 — Evidência recursiva não ganha independência por repetição
**Status:** aprovada  
**Decisão:** novos derivados da mesma ancestralidade não contam automaticamente como novas evidências independentes. Lineage e grupos de independência protegem contra Evidence Echo.

---

## D-048 — Health é técnico, cognitivo e econômico
**Status:** aprovada como estrutura de referência  
**Decisão:** Health Registry deve permitir distinguir disponibilidade técnica, qualidade cognitiva e saúde econômica/custo de uma capability.

---

## D-049 — Capability é contrato; agente é executor
**Status:** aprovada  
**Decisão:** uma capability pode possuir múltiplas implementações; agentes/modelos/funções executam capabilities e não definem o contrato universal.

---

## D-050 — Orquestração separa Control Plane e Execution Plane
**Status:** aprovada  
**Decisão:** planejamento, seleção, autorização, budget, replanejamento e parada ficam logicamente separados da execução das capabilities.

---

## D-051 — Recursão só continua por admissão explícita
**Status:** aprovada  
**Decisão:** capabilities podem propor `NextStepCandidate`, mas não criar trabalho/recursão ilimitada diretamente. Toda nova onda passa por Admission Control, policy e budget.

---

## D-052 — Toda onda possui orçamento e condição de parada
**Status:** aprovada  
**Decisão:** Explosão Atômica Recursiva exige limites explícitos de fan-out, profundidade, waves, custo, tempo, risco, novidade/ganho de informação e stop reason.

---

## D-053 — Orquestração hierárquica com autoridade limitada
**Status:** aprovada como direção arquitetural  
**Decisão:** Root Orchestrator pode delegar subplans com scope, budget, risk limit, fan-out e deadline próprios; delegar trabalho não delega autoridade ilimitada.

---

## D-054 — Hard constraints antes do ranking
**Status:** aprovada  
**Decisão:** schema, policy, scope, health e risco filtram capabilities inelegíveis antes de qualquer ranking por custo/latência/qualidade.

---

## D-055 — IA supervisora é escalonamento, não padrão obrigatório
**Status:** aprovada  
**Decisão:** IA potente pode ser acionada quando risco, ambiguidade, conflito, novidade ou ganho esperado justificarem; sua saída continua sendo Artifact/Evidence Candidate sujeito a avaliação e policy.

---

## D-056 — Falha conhecida é preferível a improvisação silenciosa
**Status:** aprovada  
**Decisão:** ausência/degradação de capability crítica gera fallback explícito, escalonamento ou fail-closed; o motor não mascara falta de capacidade usando peça inadequada.

---

# Decisões ainda não fechadas

- ontologia v0 final;
- relações v0 finais;
- Atomic/Cognitive Envelope final;
- fórmula final de confidence/calibração;
- fórmula de gravidade e decaimento temporal;
- provider inicial de embeddings;
- isolamento multi-tenant físico;
- idiomas da primeira versão executável além de pt-BR;
- limites numéricos iniciais de fan-out, waves e profundidade;
- formato físico dos registries;
- formato físico do Work Graph / OrchestrationPlan;
- algoritmo inicial de ranking de capabilities;
- política inicial de budget allocation e reserve budget;
- definição operacional de `expected_information_gain`;
- scheduler / queue / worker implementation;
- circuit breaker e backpressure thresholds;
- retry matrix por mechanism class;
- persistência dos plans/traces;
- critérios objetivos de escalonamento para Supervisory AI e Human Authority;
- critérios mínimos para capability `VALIDATED` / `ACTIVE`;
- baseline e métricas dos primeiros evaluators;
- política de orçamento cognitivo;
- primeiro problema empresarial para piloto E4;
- requisitos mínimos para mover uma capacidade de E2 para E3/E4.
