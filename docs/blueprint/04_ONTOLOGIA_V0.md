# Eva Engine® — Ontologia v0

**Status:** base inicial para validação  
**Objetivo:** definir os primeiros conceitos semânticos do motor com precisão suficiente para criar dataset e implementação.

---

# 1. Princípio

A ontologia deve ser:

- pequena no início;
- neutra de idioma;
- extensível;
- testável;
- independente do Eva Memory®;
- capaz de receber extensões por Domain Packs.

Identificadores canônicos internos usam inglês técnico para neutralidade entre idiomas.

---

# 2. Tipos fundamentais

## 2.1 Entity

Algo identificável sobre o qual eventos, estados ou relações podem existir.

Exemplos:

- pessoa;
- organização;
- projeto;
- documento;
- produto;
- lugar;
- conceito.

Campos mínimos sugeridos:

```text
entity_id
entity_type
canonical_label
aliases[]
source_scope
created_at
```

---

## 2.2 Event

Algo que aconteceu, foi observado ou foi emitido por um produto/sistema.

Campos mínimos sugeridos:

```text
event_id
event_type
source
actor
timestamp
payload
raw_reference
```

---

## 2.3 Atom

Unidade semântica mínima útil derivada ou representada pelo motor.

Campos mínimos sugeridos:

```text
atom_id
atom_type
content
source_event_id
source_span
confidence
certainty_level
created_by
engine_version
created_at
```

`source_span` é importante para rastrear qual trecho do original sustenta o átomo quando aplicável.

---

## 2.4 Relation

Ligação entre dois objetos semânticos.

Campos mínimos sugeridos:

```text
relation_id
relation_type
source_id
target_id
confidence
evidence[]
created_by
engine_version
created_at
```

---

## 2.5 Context

Conjunto de condições que ajuda a interpretar informação.

Pode incluir:

- usuário;
- produto;
- área;
- assunto;
- projeto;
- janela temporal;
- entidade ativa;
- sequência anterior.

---

## 2.6 Evidence

Evidência usada para sustentar classificação ou inferência.

Exemplos:

- palavra explícita;
- padrão linguístico;
- correção anterior;
- similaridade semântica;
- relação temporal;
- regra determinística.

---

## 2.7 Inference

Conclusão probabilística que não deve ser tratada como fato original.

Campos mínimos sugeridos:

```text
inference_id
inference_type
claim
confidence
evidence[]
status
engine_version
```

Status possível:

```text
proposed
accepted
rejected
superseded
```

---

## 2.8 Feedback

Sinal explícito ou implícito vindo do uso.

Exemplos:

```text
confirmed
corrected
rejected
reclassified
related
ignored
returned
continued
```

---

# 3. Átomos v0 candidatos

A v0 começa propositalmente pequena.

---

## A01 — OBSERVATION

**ID canônico:** `ATOM_OBSERVATION`

### Definição

Registro de algo percebido, experienciado ou observado pelo emissor.

### Exemplos positivos

- “Hoje acordei cansada.”
- “O cliente pareceu confuso durante a reunião.”
- “O sistema ficou lento depois da atualização.”

### Não confundir com

- decisão;
- tarefa;
- hipótese causal;
- fato externo verificado.

### Observação

Nem toda observação é objetivamente verdadeira. Ela registra a percepção expressa.

---

## A02 — FACT

**ID canônico:** `ATOM_FACT`

### Definição

Afirmação apresentada como fato objetivo ou dado observável diretamente estruturável.

### Exemplos

- “A reunião começou às 14h.”
- “O arquivo tem 12 páginas.”
- “A pressão registrada foi 130/85.”

### Cuidado

O motor não deve promover qualquer frase declarativa a “verdade universal”. `FACT` significa que a informação foi apresentada/registrada como factual dentro da fonte, não que o motor verificou o mundo externo.

---

## A03 — QUESTION

**ID canônico:** `ATOM_QUESTION`

### Definição

Questão aberta explícita ou linguisticamente clara.

### Exemplos

- “Como podemos reduzir o tempo de resposta?”
- “Será que isso está relacionado ao sono?”
- “Qual fornecedor devo escolher?”

### Sinais iniciais pt-BR

- `?`
- “como”
- “qual”
- “por que”
- “será que”

Sinais precisam ser avaliados em contexto; palavras interrogativas também aparecem em frases não interrogativas.

---

## A04 — INTENTION

**ID canônico:** `ATOM_INTENTION`

### Definição

Desejo, propósito ou plano ainda não consolidado como decisão/compromisso executável.

### Exemplos

- “Quero estudar isso amanhã.”
- “Pretendo viajar em setembro.”
- “Estou pensando em mudar o layout.”

### Não confundir com

- `TASK`: ação explicitamente executável/pendente;
- `DECISION`: escolha já assumida;
- `HYPOTHESIS`: explicação possível.

---

## A05 — DECISION

**ID canônico:** `ATOM_DECISION`

### Definição

Escolha assumida entre possibilidades ou posição explicitamente definida.

### Exemplos

- “Decidi usar a versão mobile primeiro.”
- “Escolhi o fornecedor B.”
- “Ficou definido que vamos usar PostgreSQL.”

### Sinais iniciais pt-BR

- “decidi”
- “escolhi”
- “resolvi”
- “ficou definido”

### Exemplo negativo

> “Talvez eu use PostgreSQL.”

Isso é intenção/possibilidade, não decisão.

---

## A06 — TASK

**ID canônico:** `ATOM_TASK`

### Definição

Ação concreta que pode ser executada ou concluída.

### Exemplos

- “Preciso marcar dentista amanhã.”
- “Enviar contrato para João.”
- “Tenho que revisar o domínio.”

### Campos derivados possíveis

```text
action
object
due_time
assignee
status
```

Não são todos obrigatórios na v0.

---

## A07 — HYPOTHESIS

**ID canônico:** `ATOM_HYPOTHESIS`

### Definição

Explicação, relação ou possibilidade ainda não confirmada.

### Exemplos

- “Talvez o café esteja atrapalhando meu sono.”
- “Acho que o atraso ocorreu por causa da API.”
- “Pode ser que o erro esteja no cache.”

### Sinais iniciais

- talvez;
- acho que;
- pode ser que;
- provavelmente;
- possível.

A confiança da classificação do átomo pode ser alta mesmo que a hipótese interna expressa pelo usuário seja incerta. São duas coisas diferentes.

---

## A08 — EXPERIMENT

**ID canônico:** `ATOM_EXPERIMENT`

### Definição

Teste deliberado criado para observar um resultado.

### Exemplos

- “Vou ficar sete dias sem café para ver se durmo melhor.”
- “Vamos testar duas versões do onboarding.”

### Estrutura candidata

```text
intervention
expected_observation
duration
start_time
end_time
status
```

---

## A09 — RESULT

**ID canônico:** `ATOM_RESULT`

### Definição

Resultado observado associado a uma ação, hipótese ou experimento anterior.

### Exemplos

- “Testei dormir às 22h e funcionou.”
- “Depois da alteração, o tempo caiu para 200ms.”

O valor deste átomo aumenta quando existe relação com experimento/ação anterior.

---

## A10 — LEARNING

**ID canônico:** `ATOM_LEARNING`

### Definição

Conclusão explicitamente apresentada como aprendizado obtido de experiência ou análise.

### Exemplos

- “Percebi que trabalho melhor pela manhã.”
- “Aprendi que esse fornecedor demora mais às segundas.”

Não confundir com inferência automática do motor. `ATOM_LEARNING` representa algo expresso na entrada.

---

## A11 — PROBLEM

**ID canônico:** `ATOM_PROBLEM`

### Definição

Estado ou situação apresentada como obstáculo, falha ou problema a resolver.

### Exemplos

- “O login está quebrado.”
- “Estou sem conseguir dormir.”
- “O cliente não recebeu o e-mail.”

---

## A12 — TEMPORAL

**ID canônico:** `ATOM_TEMPORAL`

### Definição

Expressão temporal relevante para outro átomo ou evento.

### Exemplos

- hoje;
- amanhã;
- semana passada;
- às 14h;
- desde janeiro;
- por sete dias.

### Observação

Pode futuramente ser representado mais como dimensão/qualificador do que como átomo independente. Mantido na v0 para facilitar testes de parsing. **Questão em aberto.**

---

# 4. Atom types que ainda não entram automaticamente na v0

Candidatos futuros:

```text
Emotion
Preference
Goal
Constraint
Reference
Reminder
Belief
Value
Commitment
Request
Warning
```

Motivo para esperar: evitar ontologia grande demais antes de entender sobreposição semântica.

---

# 5. Regras de ambiguidade

## Regra O-AMB-01

Um trecho pode produzir mais de um átomo quando contém significados independentes.

Exemplo:

> “Decidi trocar de fornecedor amanhã porque ele atrasou novamente.”

Pode produzir:

- Decision;
- Temporal;
- Observation;
- possível Recurrence marker.

## Regra O-AMB-02

O motor não deve forçar uma classe única quando a entrada contém múltiplos atos semânticos.

## Regra O-AMB-03

Se duas classes forem plausíveis para o mesmo trecho, registrar candidatos/confiança ou manter classificação mais genérica até haver evidência suficiente.

## Regra O-AMB-04

O usuário pode corrigir; a correção alimenta aprendizagem individual.

---

# 6. Linguagem neutra e Language Packs

A ontologia canônica não guarda sinônimos específicos de cada idioma.

Exemplo:

```text
ATOM_DECISION
```

é universal.

O Language Pack pt-BR pode mapear sinais como:

```text
decidi
escolhi
resolvi
ficou definido
```

O Language Pack en pode mapear:

```text
I decided
I chose
we agreed
```

Os packs produzem evidências para o mesmo conceito.

---

# 7. Confidence vs semantic certainty

Duas incertezas diferentes devem ser separadas.

Exemplo:

> “Talvez o cache esteja causando o problema.”

O motor pode ter:

```text
classification_confidence = 0.98
```

porque está muito seguro de que aquilo é uma hipótese.

Mas o conteúdo da hipótese expressa baixa certeza sobre a causa.

Portanto, futuramente pode existir:

```text
classification_confidence
statement_certainty
```

**Hipótese de schema a validar.**

---

# 8. Critério de promoção da Ontologia v0

Antes de chamar essa ontologia de estável para implementação ampla:

- criar no mínimo 10 exemplos positivos por tipo;
- criar exemplos negativos próximos;
- testar ambiguidade;
- testar pt-BR e ao menos um segundo idioma;
- validar conflitos entre Intention, Decision e Task;
- validar Observation vs Fact;
- validar Hypothesis vs Question;
- definir campos mínimos finais de Atom.

---

# 9. Próximo documento relacionado

Criar posteriormente:

`06_ATOMIZACAO.md`

com regras operacionais de segmentação, source spans, normalização e geração de átomos.
