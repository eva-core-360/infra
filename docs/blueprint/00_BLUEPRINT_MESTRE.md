# EVA ENGINE® — BLUEPRINT MESTRE

**Documento canônico de arquitetura e continuidade**  
**Versão do Blueprint:** 0.1-base  
**Status:** base vigente, em evolução  
**Objetivo:** permitir que o projeto seja retomado por qualquer novo chat, agente ou desenvolvedor sem depender do histórico de conversa.

---

## 0. COMO USAR ESTE DOCUMENTO

Este arquivo é a visão consolidada do projeto. Ele registra o que já foi decidido, o que está em hipótese e o que ainda precisa ser testado.

Convenções:

- **DECISÃO APROVADA**: base vigente da arquitetura.
- **HIPÓTESE DE PROJETO**: direção promissora que precisa de validação.
- **QUESTÃO EM ABERTO**: ainda não deve ser tratada como decisão.

Regra de manutenção:

> Toda mudança estrutural relevante deve atualizar este Blueprint e o Registro de Decisões. O código não é a fonte primária de verdade arquitetural; ele deve refletir o Blueprint vigente.

---

# 1. VISÃO

## 1.1 O que é o Eva Engine®

**DECISÃO APROVADA**

O Eva Engine® não nasce como um motor de notas.

Ele nasce como um **motor generalista de interpretação, memória, contexto, relações, aprendizagem e ativação cognitiva**, capaz de receber eventos e informações provenientes de diferentes produtos digitais, estruturar essa informação e aprender progressivamente com o uso.

O **Eva Memory®** será o primeiro produto consumidor do motor e o primeiro grande laboratório real da tecnologia.

Princípio central:

> **Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.**

Hoje:

```text
Eva Memory®
    ↓
Eva Engine®
```

Futuro possível:

```text
Eva Memory® ─────┐
Eva CRM ─────────┤
Eva Health ──────┤
Eva Projects ────┤──→ Eva Engine®
Educação ────────┤
Produtos terceiros┘
```

---

## 1.2 Missão do motor

Receber informação bruta e transformá-la progressivamente em informação:

```text
bruta
  ↓
preservada
  ↓
estruturada
  ↓
contextualizada
  ↓
relacionada
  ↓
aprendida
  ↓
reutilizável
```

O motor deve reduzir o esforço humano de classificação e organização sem apagar a autoria, o contexto ou a forma original de expressão do usuário.

---

## 1.3 Filosofia de experiência

O princípio de produto é:

> **Complexidade profunda nos bastidores. Simplicidade extrema na superfície.**

O motor pode executar dezenas de operações; o usuário não precisa assistir a nenhuma delas.

Exemplo desejado:

Usuário escreve:

> “De novo fiquei até três da manhã trabalhando e hoje acordei destruída.”

O motor pode detectar idioma, atomizar, localizar recorrência, recuperar memórias relacionadas, atualizar relações, recalcular pesos e aprender contexto.

A interface pode simplesmente mostrar:

> **Salvo. Relacionado a 3 registros anteriores sobre sono.**

---

# 2. PRINCÍPIOS E LEIS FUNDAMENTAIS

## P01 — Original preservado

**DECISÃO APROVADA**

O conteúdo original jamais é sobrescrito pela interpretação do motor.

Se a pessoa escreveu:

> “Essa porra desse fornecedor atrasou de novo.”

isso permanece exatamente como foi escrito.

A interpretação é armazenada em camadas derivadas e separadas.

---

## P02 — Fato não é inferência

**DECISÃO APROVADA**

O motor distingue ao menos quatro níveis:

```text
RAW       = o que foi realmente recebido
DERIVED   = o que foi extraído diretamente
INFERRED  = o que o motor considera provável
LEARNED   = o que foi aprendido ao longo do uso
```

Exemplo:

```text
RAW
“Ele atrasou novamente.”

DERIVED
recurrence_explicit = true

INFERRED
“ele” provavelmente = fornecedor X
confidence = 0.74

LEARNED
nesse contexto, o usuário costuma usar “ele” para se referir ao fornecedor X
```

A Eva não pode transformar inferência em fato silenciosamente.

---

## P03 — Toda inferência tem confiança

**DECISÃO APROVADA**

Exemplo:

```json
{
  "type": "decision",
  "confidence": 0.94
}
```

Baixa confiança deve resultar em sugestão, hipótese ou ausência de ação automática.

---

## P04 — Rastreabilidade

**DECISÃO APROVADA**

Toda classificação ou relação importante deve poder responder:

- qual regra/modelo produziu o resultado;
- qual versão do motor estava ativa;
- quais evidências contribuíram;
- qual confiança foi calculada.

Exemplo:

```text
classification = DECISION
confidence = 0.94
rule = PT_DECISION_004
engine_version = 0.3.2
ontology_version = 0.2
```

---

## P05 — Reversibilidade

**DECISÃO APROVADA**

Se o motor classifica algo como Saúde e o usuário corrige para Projeto, a correção não apaga o histórico.

```text
prediction = health
correction = project
```

Esse registro vira dado de aprendizagem.

---

## P06 — Aprendizado individual não altera automaticamente o global

**DECISÃO APROVADA**

A arquitetura separa:

```text
Conhecimento Global
      +
Perfil Semântico Individual
      +
Contexto Atual
```

Se para um usuário “cérebro” costuma significar arquitetura/backend do projeto, isso não redefine a palavra globalmente.

---

## P07 — Uso ensina

**DECISÃO APROVADA**

> **Usar a Eva é ensinar a Eva.**

O aprendizado deve ocorrer por:

- correções;
- confirmações;
- relações criadas;
- reclassificações;
- retomadas;
- buscas;
- continuidade;
- rejeições de sugestão;
- comportamento recorrente.

Sinais explícitos valem mais que sinais implícitos.

---

## P08 — Comportamento é evidência, não sentença

**DECISÃO APROVADA**

Não abrir uma memória por três meses não significa que ela deixou de ser importante.

O motor não deve psicologizar o usuário a partir de sinais fracos.

---

## P09 — A mecânica não precisa ser a interface

**DECISÃO APROVADA**

A Eva pode calcular relações, gravidade e proximidade internamente sem exibir um grafo visual.

Essa separação é essencial para mobile e para manter a interface simples.

---

## P10 — A Eva observa; não julga

**DECISÃO APROVADA**

Uma área com baixa atividade não deve ser apresentada como “fracasso”, “ruim” ou “negligência” automaticamente.

Preferir descrições observáveis:

```text
“baixa atividade recente”
“atividade crescente”
“retomado recentemente”
“sem continuidade há 32 dias”
```

---

# 3. UNIDADE UNIVERSAL DE ENTRADA: EVENTO

## 3.1 Por que evento e não nota

**DECISÃO APROVADA**

Nota é um tipo de entrada de produto. Evento é um conceito universal.

Exemplos:

```text
content.created
content.updated
customer.replied
payment.failed
workout.finished
deployment.failed
task.completed
```

Exemplo conceitual:

```json
{
  "event_type": "content.created",
  "source": "eva_memory",
  "actor": "user",
  "timestamp": "...",
  "payload": {
    "text": "Decidi trocar de fornecedor amanhã."
  }
}
```

O Core deve preferir uma API conceitual como:

```text
EvaEngine.process(event)
```

em vez de:

```text
EvaEngine.createNote(...)
```

---

# 4. PIPELINE LÓGICO DO MOTOR

**DECISÃO APROVADA COMO MAPA INICIAL**

```text
EVENTO
  ↓
01. INGESTION
  ↓
02. VALIDATION
  ↓
03. PRESERVATION
  ↓
04. LANGUAGE
  ↓
05. NORMALIZATION
  ↓
06. ATOMIZATION
  ↓
07. CLASSIFICATION
  ↓
08. CONTEXT
  ↓
09. RETRIEVAL
  ↓
10. RELATIONS
  ↓
11. INFERENCE
  ↓
12. LEARNING
  ↓
13. WEIGHT
  ↓
14. GRAVITY / ACTIVATION
  ↓
15. PERSISTENCE
  ↓
RESULTADO
```

Observação: esse pipeline descreve responsabilidades lógicas. Não significa que existirão 15 serviços separados.

---

# 5. ARQUITETURA DE MÓDULOS

## 5.1 eva-ingestion

Responsável por:

- receber eventos;
- validar envelope;
- gerar `event_id`;
- registrar origem;
- registrar ator;
- normalizar timestamp;
- encaminhar processamento.

---

## 5.2 eva-language

**DECISÃO APROVADA: o motor deve nascer multilíngue por arquitetura.**

O Core semântico não deve ser escrito “em português” para depois ser traduzido.

Estrutura conceitual:

```text
language/
├── pt-BR/
├── en/
├── es/
└── ...
```

Exemplo:

Português:

```text
“decidi”
“resolvi”
“ficou decidido”
```

Inglês:

```text
“I decided”
“I chose”
```

Ambos chegam ao Core como:

```text
ATOM_DECISION
```

A ontologia interna deve usar identificadores neutros de idioma.

---

## 5.3 eva-normalizer

Responsável por reconhecer e normalizar sinais sem alterar o original.

Pode detectar:

- idioma;
- datas;
- horários;
- URLs;
- e-mails;
- números;
- moedas;
- unidades;
- emojis;
- abreviações;
- pontuação;
- palavrões;
- expressões coloquiais.

### Regra de palavrões e linguagem vulgar

**DECISÃO APROVADA**

- preservar o original;
- não apagar;
- não censurar automaticamente;
- não inferir negatividade só porque existe palavrão;
- permitir classificar tecnicamente `contains_profanity` quando necessário;
- diferenciar linguagem vulgar de agressão contextual quando essa distinção for necessária;
- controles de ocultação/visualização pertencem à camada de produto/política, não à memória original.

Exemplo:

```text
“Caralho, deu certo!”
```

não deve ser interpretado como sentimento negativo apenas por conter palavrão.

---

## 5.4 eva-atomizer

O atomizador transforma entradas complexas em unidades menores e computáveis sem destruir a narrativa original.

Entrada:

> “Decidi trocar de fornecedor amanhã porque ele atrasou novamente.”

Possível saída:

```text
ATOM 01
Decision
“trocar fornecedor”

ATOM 02
Temporal
“amanhã”

ATOM 03
Observation
“fornecedor atrasou”

ATOM 04
Recurrence
“aconteceu anteriormente”
```

Relação candidata:

```text
ATRASO
   possible_reason_for
DECISÃO
```

---

# 6. ONTOLOGIA FUNDAMENTAL

**HIPÓTESE DE PROJETO EM FORMALIZAÇÃO**

O núcleo deve trabalhar com conceitos universais:

```text
Entity
Event
Atom
Relation
Context
State
Evidence
Action
Feedback
Inference
Time
```

Tipos iniciais de átomos candidatos:

```text
Observation
Fact
Idea
Question
Intention
Decision
Task
Hypothesis
Experiment
Event
Learning
Problem
Result
Continuity
```

A lista v0 será refinada no documento `04_ONTOLOGIA_V0.md`.

---

# 7. RELAÇÕES E CONTINUIDADE

Relações iniciais candidatas:

```text
continues
related_to
belongs_to
causes
possible_causes
depends_on
contradicts
supports
confirms
result_of
replaces
before
after
responds_to
```

Toda relação inferida deve carregar confiança.

Exemplo:

```text
A possible_causes B
confidence = 0.61
```

Continuidade é uma capacidade central: o motor deve ser capaz de detectar quando uma informação nova retoma, aprofunda ou responde a algo anterior.

---

# 8. MEMÓRIA DO MOTOR

**DECISÃO APROVADA COMO SEPARAÇÃO CONCEITUAL**

A arquitetura deve separar pelo menos:

```text
RAW MEMORY
conteúdo original

STRUCTURED MEMORY
átomos, entidades e relações

SEMANTIC MEMORY
representações semânticas e índices de recuperação

ADAPTIVE MEMORY
aprendizados individuais/contextuais

EPISODIC HISTORY
sequências e ocorrências ao longo do tempo
```

Essas camadas não precisam significar bancos físicos diferentes na v0.

---

# 9. CONTEXT ENGINE

O Context Engine procura responder:

- quem está envolvido?
- o que aconteceu?
- quando?
- em qual assunto?
- dentro de qual área/domínio?
- com o que isso se relaciona?
- o que estava acontecendo antes?
- qual produto originou o evento?
- qual contexto estava ativo?

Contexto é mais importante que “pasta”.

O objetivo é reduzir organização manual.

---

# 10. SEMÂNTICA, EMBEDDINGS E RECUPERAÇÃO

**HIPÓTESE DE IMPLEMENTAÇÃO**

Embeddings poderão ser usados para localizar memórias semanticamente próximas e detectar continuidade mesmo sem palavras idênticas.

Exemplo conceitual:

```text
sono
insônia
dormir
acordar durante a noite
descanso
```

podem ser semanticamente próximos.

A arquitetura não deve acoplar o Core a um fornecedor específico.

Interface sugerida:

```text
EmbeddingProvider
```

Implementações futuras possíveis:

```text
LocalEmbeddingProvider
CloudEmbeddingProvider
DeviceEmbeddingProvider
```

Busca vetorial inicial pode utilizar PostgreSQL + extensão vetorial, evitando um banco vetorial independente enquanto não houver necessidade real.

---

# 11. APRENDIZADO CONTÍNUO

## 11.1 Objetivo

A Eva não precisa aprender “a pensar como um ser humano”.

O objetivo é aprender progressivamente **como aquela pessoa ou organização estrutura significado e contexto**.

---

## 11.2 Sinais explícitos

Alta força de aprendizagem:

```text
user.confirmed
user.corrected
user.rejected
user.related
user.reclassified
```

---

## 11.3 Sinais implícitos

Força menor:

```text
opened
returned
continued
searched
ignored
archived
completed
```

Princípio:

> Correção explícita é evidência forte. Comportamento isolado é evidência fraca.

---

## 11.4 Aprendizado rápido e lento

### Fast learning

Atualiza perfil adaptativo após interações significativas.

```text
correção
  ↓
perfil adaptativo atualizado
```

### Slow learning

Analisa periodicamente:

- erros recorrentes;
- acertos recorrentes;
- termos pessoais;
- relações rejeitadas;
- associações recorrentes;
- mudanças consistentes de padrão.

Objetivo: evitar que um único clique altere demais o comportamento do sistema.

---

## 11.5 Pesos adaptativos com limites

**HIPÓTESE DE PROJETO**

Pesos podem se adaptar dentro de limites definidos.

Exemplo conceitual:

```text
continuidade:
min = 0.20
max = 0.40
```

Assim o sistema personaliza sem perder previsibilidade.

---

# 12. EXPANSÃO COGNITIVA CONTROLADA

Nome conceitual atual para a “explosão atômica”.

## 12.1 Ideia

Um evento pode gerar átomos; os átomos ativam memórias relacionadas; memórias revelam relações; relações podem produzir novas inferências.

```text
EVENTO
  ↓
ÁTOMOS
  ↓
ATIVAÇÃO DE MEMÓRIAS
  ↓
RELAÇÕES
  ↓
INFERÊNCIAS
  ↓
NOVAS ATIVAÇÕES POSSÍVEIS
```

## 12.2 Por que precisa ser controlada

Sem contenção, o sistema sofre explosão combinatória.

Exemplo perigoso:

```text
100.000 átomos × 100.000 átomos
```

Portanto a expansão precisa de limites:

```text
max_depth
max_atoms
max_candidates
max_related_memories
max_inferences
minimum_confidence
time_budget
cost_budget
privacy_scope
```

Princípio:

> Uma inteligência útil também precisa saber quando parar de procurar relações.

---

# 13. MOTOR ORIENTADO A EVENTOS

**DECISÃO APROVADA**

O motor não deve ficar “pensando” continuamente sem necessidade.

Ele deve acordar por eventos.

Eventos de produto:

```text
content.created
content.updated
content.deleted
content.reopened
content.continued
relation.created
relation.removed
classification.corrected
area.changed
search.performed
memory.archived
```

Eventos internos:

```text
atom.created
relation.discovered
context.changed
learning.updated
gravity.changed
```

Fluxo de exemplo:

```text
NOTE/CONTENT_CREATED
      ↓
detectar idioma
      ↓
normalizar
      ↓
atomizar
      ↓
classificar
      ↓
buscar continuidade
      ↓
avaliar relações
      ↓
atualizar pesos
      ↓
atualizar gravidade
      ↓
registrar aprendizagem necessária
```

Depois o motor volta a ficar ocioso.

---

# 14. TEMPO COMO FORÇA DO SISTEMA

Nem toda mudança depende de nova interação.

A passagem do tempo pode alterar pesos efetivos.

Exemplo:

```text
massa_base × função_temporal = massa_efetiva
```

A fórmula não está definida ainda.

**QUESTÃO EM ABERTO:** qual modelo de decaimento temporal produz um comportamento natural sem “punir” memórias antigas?

---

# 15. GRAVIDADE COGNITIVA

A gravidade é uma capacidade derivada do motor, não o próprio motor.

## 15.1 Objetivo

Representar matematicamente a atenção e atividade relativas de áreas, assuntos ou contextos.

Possíveis sinais:

```text
recência
frequência
continuidade
profundidade
relações
retorno
decisões associadas
ações associadas
persistência
```

Possíveis saídas:

```text
cognitive_mass
attention_score
trend
velocity
```

## 15.2 Regra de produto

A mecânica pode permanecer totalmente escondida.

No desktop ela pode eventualmente alimentar uma visualização espacial.

No mobile pode simplesmente definir:

- ordem das áreas;
- destaque;
- indicadores de movimento;
- “aproximando”, “estável”, “afastando”.

Não é necessário exibir grafo.

---

# 16. EVA MEMORY® — PRIMEIRO DOMÍNIO

## 16.1 Áreas de vida

**DECISÃO APROVADA COMO BASE ATUAL**

O Eva Memory® terá **13 áreas-base da vida**, com possibilidade de até **2 áreas personalizadas**, totalizando até 15 espaços quando necessário.

O “EU” não entra na contagem.

Base atual:

1. Saúde
2. Emocional
3. Família
4. Relacionamentos
5. Vida Social
6. Trabalho & Carreira
7. Finanças
8. Projetos & Criação
9. Estudos & Conhecimento
10. Casa & Ambiente
11. Lazer & Experiências
12. Propósito & Espiritualidade
13. Desenvolvimento Pessoal

Estrutura conceitual:

```text
EU
  ↓
ÁREA
  ↓
CONTEXTO / ASSUNTO
  ↓
MEMÓRIAS
  ↓
ÁTOMOS
```

A pessoa não deve ser obrigada a escolher uma área toda vez que escreve. O motor tenta classificar; o usuário pode corrigir; a correção ensina.

---

## 16.2 Interface sem grafo obrigatório

**DECISÃO APROVADA: o grafo não é requisito de interface.**

Direção mobile atual: Home Cognitiva / Ranking Vivo.

Exemplo:

```text
Saúde ↑
12 registros · atividade crescente

Projeto Eva ↑
9 registros · retomado recentemente

Finanças →
5 registros · estável

Família ↓
pouca atividade recente
```

Ao entrar em uma área:

```text
Continuar
Recentes
Assuntos
Linha do tempo
```

Princípio:

> A mecânica é o cérebro. A interface é a forma mais confortável de revelar apenas o necessário.

---

# 17. DOMAIN PACKS

**DECISÃO APROVADA**

Conhecimento específico não deve contaminar o Core.

Estrutura conceitual:

```text
domain-packs/
├── memory/
├── projects/
├── crm/
├── education/
├── finance/
└── health/
```

O primeiro será `memory`.

Um Domain Pack pode registrar tipos específicos no Schema Registry sem alterar o núcleo universal.

---

# 18. SCHEMA REGISTRY

O Schema Registry cataloga os conceitos que o motor conhece.

Core inicial:

```text
Entity
Event
Atom
Relation
Context
State
Evidence
Action
Feedback
Inference
```

Domínios podem estender.

Exemplo Saúde:

```text
Entity:
  Medication
  Examination

Event:
  MedicationTaken
  AppointmentCompleted
```

O Core não precisa ser reescrito para receber novos domínios.

---

# 19. POLICY ENGINE

**DECISÃO APROVADA COMO MÓDULO NECESSÁRIO**

Responsável por:

- privacidade;
- permissões;
- conteúdo sensível;
- retenção;
- escopo de aprendizagem;
- compartilhamento;
- execução de ações;
- limites por produto/tenant.

O motor pode sugerir uma ação, mas não deve necessariamente executá-la.

```text
Eva Engine
   ↓
Action Request
   ↓
Policy / Permission
   ↓
Adapter autorizado
   ↓
Serviço externo
```

Isso evita que o Core vire um conjunto de integrações acopladas.

---

# 20. ADAPTERS E EXECUÇÃO EXTERNA

Possíveis adaptadores futuros:

```text
Gmail
Calendar
GitHub
CRM
ERP
mensageria
IoT
aplicativos próprios
```

Princípio:

> O Core interpreta, relaciona, aprende e propõe. Adaptadores autorizados executam ações externas.

---

# 21. ARQUITETURA DE IMPLEMENTAÇÃO INICIAL

## 21.1 Modular Monolith

**DECISÃO APROVADA PARA COMEÇAR**

Não iniciar com dezenas de microserviços.

Estrutura conceitual:

```text
eva-engine/
│
├── apps/
│   ├── api/
│   └── worker/
│
├── packages/
│   ├── core/
│   ├── events/
│   ├── schemas/
│   ├── language/
│   ├── atomizer/
│   ├── context/
│   ├── semantic/
│   ├── relations/
│   ├── learning/
│   ├── policy/
│   └── gravity/
│
├── domain-packs/
│   └── memory/
│
├── datasets/
├── tests/
├── docs/
└── migrations/
```

Separação conceitual forte, implantação inicial simples.

---

# 22. STACK TECNOLÓGICA INICIAL

**DECISÃO / DIREÇÃO ATUAL**

- Programação assistida: **Cursor**
- Repositório e versionamento: **GitHub**
- Linguagem principal: **TypeScript**
- Runtime: **Node / edge compatível**
- Banco principal: **PostgreSQL**
- Plataforma de dados inicial: **Supabase/Postgres**
- Vetores: extensão vetorial no Postgres quando necessário
- API: HTTP/REST inicialmente
- Jobs: worker/background jobs
- CI/CD: GitHub Actions
- Documentação: Markdown versionado no próprio repositório
- Dataset: JSON/JSONL versionado
- Monitoramento: logs estruturados + métricas
- NLP/ML avançado: módulos/providers intercambiáveis
- Embeddings: provider intercambiável

Python não é obrigatório na v0. Se ML/NLP especializado justificar, poderá existir futuramente um `eva-ml-worker`.

---

# 23. PAPEL DO CURSOR

Cursor faz parte da fábrica do motor, não do runtime do produto.

Usos previstos:

- implementar especificações;
- criar testes;
- refatorar;
- documentar;
- gerar migrations;
- analisar dependências;
- detectar inconsistências.

Regra:

> O agente implementa a arquitetura vigente. Não deve inventar mudanças estruturais silenciosamente enquanto programa.

Por isso este repositório terá `AGENTS.md`.

---

# 24. API INICIAL

Hipótese simples:

```text
POST /v1/events
POST /v1/process
GET  /v1/memories/{id}
GET  /v1/relations/{id}
POST /v1/feedback
```

Futuramente:

```text
@eva/sdk
```

com uma interface equivalente a:

```text
eva.process(event)
```

---

# 25. PROCESSAMENTO SÍNCRONO E ASSÍNCRONO

**DECISÃO APROVADA COMO PRINCÍPIO DE UX**

Não bloquear a experiência do usuário esperando todo processamento profundo.

Imediato:

```text
salvar original
atomização básica
classificação básica
```

Background:

```text
relações profundas
recuperação extensa
reprocessamento
slow learning
expansão cognitiva
```

O usuário não deve esperar o motor “pensar” desnecessariamente para continuar usando o produto.

---

# 26. DATASET EVA

**DECISÃO APROVADA: dataset versionado desde o início.**

Estrutura proposta:

```text
datasets/
├── multilingual/
├── atomization/
├── relations/
├── continuity/
├── ambiguity/
├── profanity/
├── temporal/
└── corrections/
```

Exemplo:

```json
{
  "input": "Decidi resolver isso amanhã.",
  "language": "pt-BR",
  "expected": {
    "atoms": ["decision", "temporal"]
  }
}
```

Esse dataset é parte do patrimônio tecnológico do motor.

---

# 27. TESTES

Categorias mínimas:

## Unit tests

Uma regra isolada funciona?

## Language tests

Idiomas diferentes produzem o mesmo conceito semântico interno quando expressam a mesma intenção?

## Regression tests

O que funcionava na versão anterior continua funcionando?

## Golden tests

Casos versionados com:

```text
input
expected_atoms
expected_relations
expected_confidence
```

Esse conjunto funciona como laboratório cognitivo do motor.

---

# 28. OBSERVABILIDADE

Precisamos enxergar o motor trabalhando no ambiente técnico.

Exemplo:

```text
Evento recebido
↓
3 átomos
↓
12 candidatos
↓
2 relações aceitas
↓
1 relação rejeitada
↓
processamento = 143ms
```

Métricas candidatas:

```text
accuracy
correction_rate
false_relation_rate
processing_time
atoms_per_event
relations_per_event
learning_improvement
```

Objetivo: substituir “parece inteligente” por evidência mensurável.

---

# 29. VERSIONAMENTO COGNITIVO

Todo resultado relevante deve poder registrar:

```text
engine_version
language_pack_version
ontology_version
rule_version
embedding_model_version
```

Objetivo futuro:

```text
reprocessar memórias antigas com Eva Engine 2.x
```

sem perder o original nem o histórico de interpretações anteriores.

---

# 30. O QUE NÃO FAZER AGORA

**DECISÃO APROVADA COMO CONTROLE DE ESCOPO**

Na primeira fase, NÃO:

- treinar um modelo próprio;
- criar 20 microserviços;
- suportar dezenas de idiomas imediatamente;
- construir CRM, saúde e educação ao mesmo tempo;
- tentar criar a fórmula definitiva de gravidade antes dos testes;
- usar IA generativa para resolver tudo;
- tentar compreender qualquer frase humana possível;
- construir um grafo visual como requisito do motor;
- acoplar o Core a um fornecedor único de IA, embeddings ou nuvem.

---

# 31. PRIMEIRO OBJETIVO TÉCNICO REAL

A v0 deve conseguir:

> **receber uma informação, preservar o original, identificar idioma, gerar alguns átomos corretamente, registrar confiança, persistir resultados e manter rastreabilidade.**

Quando isso funcionar de forma testável, o coração do motor está batendo.

Depois:

```text
v0.1 atomização básica
   ↓
v0.2 relações e continuidade
   ↓
v0.3 perfil semântico individual
   ↓
v0.4 pesos adaptativos
   ↓
v0.5 gravidade/ativação
   ↓
v1.0 motor cognitivo inicial
```

A numeração ainda é provisória e será formalizada no Roadmap.

---

# 32. DOCUMENTOS DERIVADOS DO BLUEPRINT

A base deverá evoluir para documentos especializados:

```text
00_BLUEPRINT_MESTRE.md
01_REGISTRO_DECISOES.md
02_CONTEXTO_CONTINUIDADE.md
03_ROADMAP_IMPLEMENTACAO.md
04_ONTOLOGIA_V0.md
05_EVENTOS_V0.md
06_ATOMIZACAO.md
07_RELACOES_CONTINUIDADE.md
08_MEMORIA_CONTEXTO.md
09_APRENDIZADO.md
10_MULTILINGUE.md
11_POLICY_PRIVACIDADE.md
12_GRAVIDADE.md
13_SCHEMA_REGISTRY.md
14_DOMAIN_PACK_MEMORY.md
15_API_SDK.md
16_DADOS_PERSISTENCIA.md
17_TESTES_DATASET.md
18_OBSERVABILIDADE.md
19_SEGURANCA.md
20_OPERACAO_DEPLOY.md
```

Os nomes podem ser ajustados conforme o projeto evoluir.

---

# 33. QUESTÕES EM ABERTO

Ainda não tratar como decisão final:

1. Lista final de átomos v0.
2. Lista final de relações v0.
3. Modelo inicial de confidence scoring.
4. Fórmula de massa/gravidade cognitiva.
5. Função de decaimento temporal.
6. Primeiro provider de embeddings.
7. Estratégia exata de detecção de idioma.
8. Limites iniciais da expansão cognitiva.
9. Schema físico final do banco.
10. Estratégia de fila/background jobs.
11. Política de reprocessamento de memórias antigas.
12. Estratégia de isolamento multi-tenant.
13. Quais idiomas além de pt-BR entram na primeira versão executável.
14. Critério objetivo para promover uma heurística a regra estável.
15. Como medir aprendizado individual sem criar comportamento instável.

---

# 34. DEFINIÇÕES CURTAS DO PROJETO

## Eva Engine®

Motor generalista de interpretação, memória, contexto, relações, aprendizagem e ativação cognitiva.

## Eva Memory®

Primeiro produto consumidor do Eva Engine®, voltado à memória cognitiva pessoal.

## Átomo

Unidade semântica mínima útil extraída ou representada pelo motor.

## Atomização

Processo de transformar uma entrada complexa em unidades menores preservando o original.

## Expansão Cognitiva Controlada

Ativação em cadeia de átomos, memórias, relações e inferências com limites de profundidade, confiança, custo e escopo.

## Gravidade Cognitiva

Mecânica derivada que representa massa/atenção relativa a partir da atividade, continuidade e outros sinais.

## Perfil Semântico Individual

Memória adaptativa que registra significados, correções e padrões particulares de um usuário sem redefinir o conhecimento global.

## Domain Pack

Pacote de conhecimento específico de um domínio que estende o Core sem acoplá-lo ao produto.

---

# 35. FRASES-GUIA

Estas frases resumem decisões de projeto e devem permanecer como referência:

> **Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.**

> **Usar a Eva é ensinar a Eva.**

> **A Eva observa; não julga.**

> **A mecânica não precisa ser a interface.**

> **Complexidade profunda nos bastidores. Simplicidade extrema na superfície.**

> **A memória original pertence ao usuário; a interpretação pertence ao motor e deve ser rastreável e reversível.**

---

# 36. PRÓXIMO PASSO DO BLUEPRINT

A próxima etapa de especificação é formalizar a **Ontologia v0**:

- quais tipos de átomos existem;
- definição exata de cada um;
- exemplos positivos;
- exemplos negativos;
- ambiguidades;
- relações permitidas;
- campos mínimos;
- confiança;
- regras multilíngues iniciais.

Essa especificação deverá alimentar diretamente o primeiro dataset e a primeira implementação no Cursor.
