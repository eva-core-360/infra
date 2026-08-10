# Eva Engine® — Testes e Dataset

**Status:** especificação inicial

---

# 1. Princípio

O motor deve ser avaliado por evidência, não por impressão subjetiva.

> “Parece inteligente” não é critério de aceitação.

---

# 2. Dataset como patrimônio tecnológico

O dataset deve nascer junto com o motor e ser versionado.

Estrutura sugerida:

```text
datasets/
├── multilingual/
├── atomization/
├── relations/
├── continuity/
├── ambiguity/
├── profanity/
├── temporal/
├── corrections/
├── gravity/
└── regression/
```

---

# 3. Formato inicial

JSONL é candidato forte por ser simples, versionável e fácil de processar.

Exemplo:

```json
{"id":"atom_pt_001","input":"Decidi resolver isso amanhã.","language":"pt-BR","expected":{"atoms":["ATOM_DECISION","ATOM_TEMPORAL"]}}
```

Campos futuros:

```text
id
input
language
context
expected_atoms
expected_relations
expected_entities
expected_time
forbidden_outputs
notes
tags
```

---

# 4. Golden tests

Casos aprovados funcionam como contrato de comportamento.

Cada mudança de engine roda o conjunto novamente.

Objetivo:

- detectar regressão;
- permitir refatoração segura;
- comparar versões;
- medir evolução.

---

# 5. Tipos de teste

## Unit

Regra isolada.

Exemplo:

> “decidi” gera evidência para Decision quando não negado?

## Integration

Múltiplos módulos juntos.

Exemplo:

```text
content.created
→ language
→ atomizer
→ persistence
```

## Regression

Casos que quebraram no passado passam a fazer parte da suíte permanente.

## Multilingual equivalence

Frases equivalentes em idiomas diferentes devem produzir conceitos canônicos equivalentes quando semanticamente apropriado.

## Adversarial/ambiguity

Testar frases que parecem uma classe mas são outra.

Exemplo:

> “Não decidi mudar.”

Não pode virar Decision positiva automaticamente.

---

# 6. Dataset de profanidade

Precisa testar contexto, não só palavra proibida.

Casos:

```text
“Caralho, deu certo!”
```

Esperado:

- profanity flag possível;
- resultado positivo permitido;
- não inferir emoção negativa automaticamente.

Também testar uso ofensivo direcionado separadamente.

---

# 7. Dataset temporal

Exemplos:

```text
hoje
ontem
amanhã
semana passada
daqui a três dias
segunda-feira
às 14h
há seis meses
desde janeiro
por sete dias
```

Testar referência relativa usando clock controlado.

---

# 8. Dataset de continuidade

Estrutura deve conter sequências.

Exemplo:

```text
T0: “Vou testar dormir às 22h por uma semana.”
T1: “No terceiro dia dormi melhor.”
T2: “Terminei o teste e funcionou.”
```

Esperado:

- T1 relacionado ao experimento de T0;
- T2 como Result/continuidade;
- relações com confiança adequada.

---

# 9. Dataset de aprendizagem

Simular perfis separados.

Perfil A:

```text
“cérebro” + contexto Eva → Projects
```

Perfil B:

```text
“cérebro” → Health
```

Objetivo:

provar que personalização de A não contamina B ou conhecimento global.

---

# 10. Dataset de gravidade

Criar timeline sintética por 90 dias.

Avaliar:

- burst de atividade;
- continuidade longa;
- spam de notas curtas;
- retorno após semanas;
- área estável;
- área sem atividade recente.

Comparar fórmula com resultado intuitivo esperado.

---

# 11. Métricas

Candidatas:

```text
precision
recall
f1
classification_accuracy
relation_precision
correction_rate
false_relation_rate
processing_time
personalization_gain
regression_count
```

Nem todas precisam entrar na v0.

---

# 12. Critério de aceitação por módulo

Cada módulo deve definir sua própria barra de qualidade antes de produção.

Exemplo:

Atomizer v0:

- alta precisão em tipos suportados;
- nenhuma perda de RAW;
- source span correto;
- resultado determinístico para regras determinísticas;
- regressão zero nos golden tests aprovados.

---

# 13. Casos reais vs fictícios

Começar com casos fictícios cuidadosamente escritos.

Depois adicionar casos reais anonimizados/consentidos quando houver processo adequado.

Não colocar conteúdo pessoal sensível bruto no repositório público ou em dataset de engenharia sem política explícita.

---

# 14. Versionamento do dataset

Cada release relevante do motor deve registrar qual versão do dataset foi usada na validação.

Exemplo:

```text
engine = 0.3.0
dataset = 0.7.2
ontology = 0.4.0
```

Isso permite comparação histórica confiável.
