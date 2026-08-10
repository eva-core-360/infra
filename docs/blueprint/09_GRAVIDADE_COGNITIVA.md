# Eva Engine® — Gravidade Cognitiva

**Status:** hipótese arquitetural forte; fórmula ainda não fechada

---

# 1. Objetivo

Criar uma métrica dinâmica que represente quanto um assunto, contexto ou área está ativo na vida ou operação do usuário sem reduzir tudo a contagem de registros.

A gravidade é uma capacidade derivada do motor.

Ela não define a ontologia e não é requisito para todos os produtos consumidores.

---

# 2. Conceitos

## Massa cognitiva

Quantidade ponderada de atividade/significado acumulado por um objeto semântico.

## Ativação

Força atual de presença daquele objeto no contexto recente.

## Tendência

Direção da mudança:

```text
rising
stable
falling
```

## Velocidade

Taxa de mudança da ativação ao longo do tempo.

---

# 3. Sinais candidatos

```text
recency
frequency
continuity
return_rate
relation_density
decision_weight
action_weight
result_weight
persistence
explicit_priority
```

Não assumir pesos finais sem experimento.

---

# 4. Regra contra contagem burra

Dez notas superficiais não devem necessariamente pesar mais que uma sequência longa de decisão + continuidade + resultado.

Exemplo conceitual:

```text
Nota A
“ok”

Nota B
“Decidi testar X por sete dias...”
  ↓
Experiment
  ↓
Result
  ↓
Learning
```

A segunda sequência pode produzir mais massa significativa.

---

# 5. Agregação

```text
Atom
  ↓
Topic / Context
  ↓
Area
  ↓
Product-level representation
```

Exemplo no Eva Memory®:

```text
Projetos & Criação        0.91 ↑
  Eva Memory              0.96 ↑
  Marca de roupas         0.42 →
  Projeto Casa            0.18 ↓
```

---

# 6. Tempo

A massa efetiva pode considerar tempo.

Modelo genérico:

```text
base_mass × temporal_factor = effective_mass
```

A função temporal deve evitar duas falhas:

1. fazer tudo antigo parecer irrelevante;
2. manter atividade antiga eternamente dominante.

Possíveis modelos a testar:

- exponencial;
- meia-vida por tipo de átomo;
- decaimento por janelas;
- decaimento adaptado por recorrência.

Nenhum está aprovado ainda.

---

# 7. Gravidade não é moralidade

Uma área que caiu não significa abandono moral.

Interface deve preferir:

```text
atividade menor
menos continuidade recente
estável
retomando
```

Evitar:

```text
você negligenciou
você falhou
área ruim
```

salvo se algum produto específico tiver contexto e consentimento para linguagem diferente.

---

# 8. Mobile

A gravidade pode alimentar um ranking vertical simples.

```text
Saúde ↑
atividade crescente

Projetos →
estável

Finanças ↓
menor atividade recente
```

O usuário não precisa ver números brutos.

---

# 9. Desktop

O mesmo score pode alimentar:

- ranking;
- heatmap;
- timeline;
- visualização espacial opcional;
- comparação entre períodos.

O grafo não é requisito.

---

# 10. Explicabilidade técnica

Todo score precisa poder ser decomposto internamente.

Exemplo:

```text
score = 0.82

recency        +0.21
continuity     +0.25
frequency      +0.14
returns        +0.09
relations      +0.08
other          +0.05
```

A interface final pode não exibir tudo, mas desenvolvimento e auditoria precisam conseguir explicar.

---

# 11. Métricas de validação

- estabilidade de ranking;
- sensibilidade a nova atividade;
- resistência a spam de notas curtas;
- efeito de continuidade;
- efeito de retorno;
- comportamento temporal;
- correlação com percepção do usuário.

---

# 12. Próximo experimento

Criar histórico sintético de 90 dias com 13 áreas e testar diferentes fórmulas.

Critério desejado:

- atividade real recente sobe;
- spam não domina;
- continuidade pesa;
- áreas antigas não desaparecem abruptamente;
- resultado é intuitivo ao observar a sequência.
