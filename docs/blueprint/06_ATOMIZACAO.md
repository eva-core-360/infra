# Eva Engine® — Motor de Atomização

**Status:** especificação inicial  
**Objetivo:** definir como entradas complexas se transformam em unidades semânticas úteis sem perder o original.

---

# 1. Princípio central

Atomizar não é resumir e não é reescrever.

Atomização significa:

> preservar a fonte e criar representações menores, rastreáveis e reutilizáveis a partir dela.

O original permanece intacto.

---

# 2. Entrada e saída

Entrada:

```text
Evento + conteúdo bruto + contexto disponível
```

Saída:

```text
zero ou mais átomos
+ spans de origem
+ evidências
+ confiança
+ qualificadores
```

Exemplo:

> “Decidi trocar de fornecedor amanhã porque ele atrasou novamente.”

Saída possível:

```text
Decision: trocar fornecedor
Temporal: amanhã
Observation: fornecedor atrasou
Recurrence marker: novamente
```

---

# 3. Etapas propostas

```text
RAW
 ↓
segmentação
 ↓
detecção de idioma
 ↓
normalização não destrutiva
 ↓
extração de sinais
 ↓
geração de candidatos
 ↓
classificação
 ↓
resolução de sobreposição
 ↓
source spans
 ↓
confidence
 ↓
persistência
```

---

# 4. Normalização não destrutiva

A normalização serve ao processamento, não à edição do usuário.

Pode criar versões técnicas para:

- lowercase quando necessário;
- expansão de abreviações;
- normalização de espaços;
- datas;
- números;
- moedas;
- emojis;
- pontuação;
- gírias;
- profanidade.

Nunca substituir RAW pela versão normalizada.

---

# 5. Source spans

Todo átomo extraído de texto deve, quando possível, apontar para o trecho que o originou.

Exemplo conceitual:

```json
{
  "atom_type": "ATOM_DECISION",
  "content": "trocar de fornecedor",
  "source_span": {
    "start": 0,
    "end": 28
  }
}
```

Benefícios:

- auditoria;
- explicabilidade;
- debug;
- realce na UI;
- reprocessamento.

---

# 6. Três camadas de interpretação

## Determinística

Usada quando existe sinal explícito e regra confiável.

Exemplos:

- datas bem formatadas;
- URLs;
- pontuação interrogativa;
- padrões linguísticos explícitos.

## Heurística

Usada quando existem sinais, mas não certeza absoluta.

Exemplos:

- intenção vs tarefa;
- observação vs fato;
- hipótese causal.

## Preditiva

Não deve ser necessária para a atomização básica v0. Entra futuramente para priorização e contexto provável usando histórico.

---

# 7. Atomização múltipla

Uma frase pode gerar vários átomos.

Não forçar classificação única de uma sentença inteira.

Exemplo:

> “Estou cansada e decidi dormir cedo amanhã.”

Pode gerar:

- Observation: estou cansada;
- Decision: dormir cedo;
- Temporal: amanhã.

---

# 8. Sobreposição e conflitos

Quando dois candidatos ocupam o mesmo trecho:

1. comparar especificidade;
2. comparar evidência;
3. comparar confiança;
4. verificar se são semanticamente compatíveis;
5. manter ambos se representam dimensões diferentes;
6. evitar duplicata semântica.

---

# 9. Profanidade

Profanidade é sinal lexical/contextual, não tipo de átomo cognitivo por padrão.

Exemplo:

> “Caralho, finalmente funcionou.”

Pode produzir:

- Result: funcionou;
- atributo técnico: contains_profanity = true;

Não produzir automaticamente:

- emoção negativa;
- agressão;
- conteúdo inválido.

---

# 10. Atomização e idioma

O atomizador consome evidências do Language Pack e produz conceitos neutros.

```text
pt-BR: “decidi”
        ↓
ATOM_DECISION

EN: “I decided”
        ↓
ATOM_DECISION
```

O mesmo tipo canônico deve funcionar em qualquer idioma suportado.

---

# 11. Reprocessamento

Cada átomo registra versão da engine/ontologia/regras.

Quando o motor melhorar, memórias antigas podem ser reprocessadas sem apagar resultados históricos imediatamente.

Estratégia final de substituição/supersedência ainda será definida.

---

# 12. Métricas do atomizador

Candidatas:

```text
atom_precision
atom_recall
classification_accuracy
false_positive_rate
false_negative_rate
atoms_per_input
correction_rate
```

No início, priorizar precisão sobre quantidade: é melhor gerar poucos átomos úteis do que atomizar tudo de forma barulhenta.

---

# 13. Critério de v0

A v0 não precisa entender qualquer texto humano.

Precisa entender muito bem um conjunto pequeno de situações com golden tests claros.

Meta conceitual:

> pequeno, previsível, rastreável e evolutivo.
