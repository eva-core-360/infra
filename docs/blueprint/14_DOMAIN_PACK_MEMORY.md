# Eva Engine® — Domain Pack: Memory v0

**Status:** base inicial  
**Produto consumidor:** Eva Memory®

---

# 1. Objetivo

Adicionar conhecimento específico de memória pessoal/notas sem alterar o Core generalista.

O Domain Pack `memory` traduz necessidades do Eva Memory® para contratos universais do Eva Engine®.

---

# 2. O que pertence ao Core

Exemplos:

```text
Event
Atom
Entity
Relation
Context
Inference
Feedback
Learning
Policy
```

---

# 3. O que pertence ao Memory Pack

Exemplos:

- áreas da vida;
- assuntos pessoais;
- captura de nota;
- retomada de memória;
- Home Cognitiva;
- continuidade de registros;
- formas de apresentação da gravidade para vida pessoal.

---

# 4. Áreas-base

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

“EU” não entra na contagem.

Até 2 áreas adicionais podem ser criadas pelo usuário.

---

# 5. Identificadores internos

Sugestão neutra:

```text
AREA_HEALTH
AREA_EMOTIONAL
AREA_FAMILY
AREA_RELATIONSHIPS
AREA_SOCIAL
AREA_WORK_CAREER
AREA_FINANCE
AREA_PROJECTS_CREATION
AREA_STUDY_KNOWLEDGE
AREA_HOME_ENVIRONMENT
AREA_LEISURE_EXPERIENCES
AREA_PURPOSE_SPIRITUALITY
AREA_PERSONAL_DEVELOPMENT
```

Labels são localizados por idioma.

---

# 6. Classificação de área

O usuário não deve ser obrigado a escolher área ao capturar conteúdo.

Fluxo:

```text
captura
  ↓
Core atomiza/contextualiza
  ↓
Memory Pack calcula candidatos de área
  ↓
confidence
  ↓
atribuição automática ou sugestão
  ↓
correção possível
  ↓
feedback para aprendizado
```

---

# 7. Assuntos

Áreas não devem funcionar como pastas rígidas.

Dentro de uma área, assuntos/contextos podem nascer dinamicamente.

Exemplo:

```text
Saúde
  ├── Sono
  ├── Alimentação
  ├── Exames
  └── Dor lombar
```

Um conteúdo pode se relacionar a mais de um assunto/área sem duplicar o original.

---

# 8. Home Cognitiva

Direção atual:

```text
Saúde ↑
atividade crescente

Projetos & Criação ↑
retomado recentemente

Finanças →
estável

Família ↓
baixa atividade recente
```

O ranking é uma visualização derivada da gravidade, não a fonte da verdade.

---

# 9. Experiência de captura

Meta:

> escrever primeiro, organizar depois — preferencialmente pelo motor.

Evitar exigir:

- pasta;
- tag;
- assunto;
- área;
- tipo de nota

a cada captura.

A fricção deve ser mínima.

---

# 10. Experiência de continuidade

Dentro de uma área/assunto, o produto pode apresentar:

```text
Continuar
Recentes
Assuntos
Linha do tempo
```

O motor deve ajudar a recuperar o ponto anterior sem exigir busca manual constante.

---

# 11. Gravidade no Memory Pack

O Core pode calcular sinais genéricos.

O Memory Pack decide como agregá-los/apresentá-los para áreas pessoais.

Exemplo:

```text
atom mass
  ↓
topic activation
  ↓
area activation
```

---

# 12. Não julgamento

O Memory Pack herda o princípio:

> A Eva observa; não julga.

Evitar linguagem moralizante sobre baixa atividade.

---

# 13. Primeiros eventos usados

```text
content.created
content.updated
content.reopened
content.continued
classification.corrected
relation.created
context.changed
memory.archived
```

---

# 14. Primeira prova de valor

O Memory Pack deve provar que:

1. a pessoa captura sem organizar manualmente;
2. o motor classifica parcialmente;
3. continuidade é encontrada;
4. correção ensina;
5. Home Cognitiva reflete o uso;
6. a experiência melhora com o tempo.

---

# 15. O que não deve entrar no Core

Evitar tipos como:

```text
NoteFolder
LifeAreaCard
EvernoteStyleNotebook
```

no núcleo universal.

São conceitos de produto/interface.
