# Eva Engine® — Evidence Model v0.1

**Status:** base arquitetural para refinamento e testes  
**Função:** definir como o Eva Engine® transforma sinais em evidência, evidência em hipóteses/inferências e inferências em decisões sem confundir força matemática, confiança, causalidade ou certeza.

---

# 1. Por que o Evidence Model é obrigatório

Um motor que cruza milhares ou milhões de sinais corre um risco fundamental:

> **quanto mais relações encontra, mais fácil fica construir uma história convincente em torno de algo falso.**

Portanto, o Eva Engine® não pode possuir apenas:

```text
SIGNAL
  ↓
INFERENCE
```

Ele precisa de uma camada explícita:

```text
SIGNAL
  ↓
EVIDENCE
  ↓
CLAIM / HYPOTHESIS
  ↓
CHALLENGE
  ↓
CONFIDENCE / UNCERTAINTY
  ↓
DECISION
```

O Evidence Model existe para impedir que coincidência, repetição, correlação, duplicação ou saída de um agente seja tratada como prova suficiente.

---

# 2. Seis conceitos que nunca devem ser confundidos

## 2.1 Signal

Um **sinal** é uma observação computacional relevante.

Exemplos:

```text
termo apareceu
frequência aumentou
entidade mudou de estado
latência subiu
mesmos IDs aparecem juntos
sequência se repetiu
similaridade semântica alta
valor saiu do intervalo esperado
```

Sinal não é evidência automaticamente.

---

## 2.2 Evidence

**Evidência** é um sinal ou conjunto de sinais que possui relação explícita com uma claim/hypothesis e cuja origem pode ser auditada.

Exemplo:

```text
SIGNAL
“82% dos incidentes do grupo X ocorreram após mudança Y”

EVIDENCE
esse padrão suporta HYPOTHESIS H17
com método M3
sobre população P2
na janela temporal T5
```

---

## 2.3 Claim

Uma **Claim** é uma afirmação verificável que o sistema está avaliando.

Exemplo:

```text
CLAIM C17
“A versão Z está associada a aumento de falhas no processo P.”
```

Claim não significa verdade.

---

## 2.4 Hypothesis

Uma **Hypothesis** é uma claim ainda em investigação, normalmente usada para organizar busca de evidência e contraprova.

```text
HYPOTHESIS H17
“combinação fornecedor X + turno Y + versão Z contribui para atraso”
```

---

## 2.5 Score

Um **Score** é uma medida produzida por um mecanismo.

Exemplos:

```text
similarity_score = 0.82
anomaly_score = 4.7
association_score = 12.4
keyword_density = 0.61
```

Score não deve ser exibido ou tratado como probabilidade sem calibração apropriada.

---

## 2.6 Confidence

**Confidence** representa o grau calibrado de suporte que o sistema atribui a uma inferência/claim em determinado contexto.

Princípio:

> **Confidence não é sinônimo de score.**

Se não houver método de calibração justificável, usar nomes como:

```text
strength
score
support_index
ranking_score
```

em vez de `confidence`.

---

# 3. Modelo conceitual

```text
RAW / EVENT
    │
    ▼
SIGNALS
    │
    ├─────────────┐
    ▼             ▼
EVIDENCE       COUNTER-EVIDENCE
    │             │
    └──────┬──────┘
           ▼
       CLAIM / HYPOTHESIS
           │
           ▼
       CHALLENGER
           │
           ▼
    EVIDENCE AGGREGATION
           │
           ▼
   CONFIDENCE / UNCERTAINTY
           │
           ▼
      POLICY / RISK
           │
           ▼
        DECISION
```

---

# 4. Evidence Item

Contrato conceitual inicial:

```text
EvidenceItem
├── evidence_id
├── claim_id
├── direction              # supports / contradicts / neutral
├── source_ref
├── source_type
├── method_id
├── method_version
├── observed_at
├── valid_from?
├── valid_until?
├── scope_id
├── population_ref?
├── sample_size?
├── strength_score?
├── calibrated_confidence?
├── uncertainty?
├── independence_group?
├── provenance
├── epistemic_level
├── trust_state
├── integrity_state
├── version_vector
└── trace_id
```

O modelo físico final pode mudar, mas esses conceitos devem permanecer distinguíveis.

---

# 5. Evidence Direction

Toda evidência precisa declarar sua relação com a claim.

```text
SUPPORTS
CONTRADICTS
NEUTRAL
INCONCLUSIVE
```

Isso permite que o motor procure ativamente por evidência contrária em vez de acumular somente sinais favoráveis.

---

# 6. Challenger como parte do Evidence Model

O Challenger não é um “agente pessimista”.

Ele executa uma função epistemológica:

> **tentar encontrar condições sob as quais a conclusão atual deixa de se sustentar.**

Exemplos de perguntas mecanizáveis:

```text
- o padrão sobrevive sem duplicatas?
- o padrão existe no grupo de controle?
- o efeito permanece em outra janela temporal?
- existe uma variável confundidora?
- a relação aparece apenas depois de um filtro?
- a associação é explicada por volume/base rate?
- fontes independentes confirmam?
- o resultado muda com outro método?
- existe evidência que contradiz a hipótese?
```

O Challenger produz **counter-evidence**, não apenas uma opinião textual.

---

# 7. Independência de evidência

Um dos riscos mais importantes é contar a mesma origem várias vezes.

Exemplo errado:

```text
notícia original A
  ↓
site B copia A
  ↓
site C resume B
  ↓
LLM D cita C

motor conta: 4 evidências independentes
```

Na realidade pode existir apenas **uma origem primária**.

Por isso cada Evidence Item pode carregar:

```text
independence_group
source_lineage
primary_source_ref
```

Princípio:

> **Repetição não cria independência.**

---

# 8. Duplicação e efeito de eco

O Eva Engine® deve tentar detectar:

```text
duplicata exata
quase duplicata
mesma fonte republicada
mesmo evento contado várias vezes
mesma hipótese retornando como “nova evidência”
derivados recursivos que apontam para o mesmo ancestral
```

Sem essa proteção, a Explosão Atômica poderia amplificar artificialmente confiança.

Nome do risco:

**Evidence Echo / Echo Amplification**.

---

# 9. Causalidade não nasce de correlação

**DECISÃO APROVADA COMO PRINCÍPIO**

O motor deve distinguir pelo menos:

```text
CO-OCCURRENCE
ASSOCIATION
TEMPORAL PRECEDENCE
PREDICTIVE RELATION
POSSIBLE_CAUSE
CAUSAL_EVIDENCE
CONFIRMED_CAUSE
```

A transição entre esses níveis exige evidência crescente.

Exemplo:

```text
X e Y aparecem juntos
      ≠
X causa Y
```

Mesmo quando X precede Y:

```text
X acontece antes de Y
      ≠
X causa Y
```

O motor pode sugerir investigação causal sem promover causalidade prematuramente.

---

# 10. Base rate

Um padrão pode parecer forte apenas porque algo já é muito frequente.

Exemplo:

```text
80% das falhas usam sistema X
```

isso parece importante até descobrir:

```text
95% de todas as operações usam sistema X
```

Portanto, sempre que aplicável, o Evidence Model deve buscar uma **base rate / taxa de base**.

Possíveis comparações:

```text
incidência no grupo afetado
versus
incidência no grupo geral
```

---

# 11. Confounders

Uma **confounding variable** / variável confundidora pode produzir associação aparente entre A e B.

Exemplo:

```text
A = turno noturno
B = falha alta
C = hardware antigo
```

Talvez o turno noturno utilize mais hardware antigo.

O motor não precisa resolver causalidade universal na v0, mas deve conseguir representar:

```text
potential_confounder
```

como artefato/evidência candidata.

---

# 12. Evidência temporal

Toda evidência tem contexto temporal.

Uma relação válida em 2025 pode não ser válida em 2027.

Por isso o Evidence Model deve suportar:

```text
observed_at
valid_from
valid_until
time_window
recency
staleness
```

Princípio:

> **Evidência antiga não desaparece, mas pode perder aplicabilidade atual.**

---

# 13. Evidence Decay não deve ser universal

Não existe uma fórmula única de decaimento para toda evidência.

Exemplos:

```text
lei contratual assinada
pode continuar válida por anos

latência de serviço
pode ficar obsoleta em minutos

preferência de usuário
pode mudar gradualmente
```

O decaimento deve ser policy/domain aware.

---

# 14. Tipos de incerteza

O sistema deve poder registrar por que existe incerteza.

Categorias iniciais:

```text
DATA_INSUFFICIENCY
SOURCE_UNRELIABILITY
MODEL_UNCERTAINTY
CONFLICTING_EVIDENCE
OUT_OF_DISTRIBUTION
AMBIGUOUS_CONTEXT
TEMPORAL_STALENESS
MISSING_COUNTERFACTUAL
UNKNOWN_CONFOUNDER
```

Isso é melhor do que reduzir toda incerteza a um único número.

---

# 15. Evidence Aggregation

O agregador de evidência deve considerar mais do que soma simples.

Ele pode precisar ponderar:

```text
qualidade da fonte
independência
quantidade
recência
método
integridade
escopo
contradições
base rate
risco
calibração histórica
```

Forma conceitual:

```text
ClaimSupport = f(
  evidence_strength,
  independence,
  source_quality,
  contradictions,
  temporal_validity,
  calibration,
  scope
)
```

**QUESTÃO EM ABERTO:** fórmula final.

Nenhuma fórmula deve ser escolhida apenas por parecer elegante.

---

# 16. Confidence Calibration

Um sistema está calibrado quando, ao longo de muitos casos comparáveis, afirmações com determinada confiança acertam aproximadamente naquela proporção.

Exemplo conceitual:

```text
100 inferências marcadas como 0.80
≈
80 corretas
```

Isso exige ground truth ou feedback confiável.

Métricas candidatas futuras:

```text
Brier Score
Expected Calibration Error (ECE)
reliability diagrams
log loss
```

Essas métricas são candidatas; o conjunto final dependerá do tipo de saída.

---

# 17. Confidence nunca substitui Policy

Mesmo alta confiança não autoriza automaticamente ação de alto risco.

Exemplo:

```text
confidence = 0.98
risk = critical
```

Policy pode exigir:

```text
human_approval = true
```

Portanto:

```text
Confidence
     +
Risk
     +
Reversibility
     +
Policy
     =
Action Authority
```

---

# 18. Risk-weighted Evidence Thresholds

O nível de evidência necessário deve aumentar com o risco.

```text
LOW RISK
pista pode ser suficiente

MEDIUM RISK
múltiplas evidências + challenger

HIGH RISK
forte evidência + independência + evaluator

CRITICAL
strong evidence + policy + supervisory/human authority
```

Exemplo:

```text
“talvez esse relatório esteja relacionado”
```

pode tolerar incerteza maior que:

```text
“bloquear pagamento de R$ 10 milhões”
```

---

# 19. Claim Lifecycle

```text
PROPOSED
   │
   ▼
UNDER_EVALUATION
   │
   ├────────────► INCONCLUSIVE
   │
   ├────────────► REJECTED
   │
   ▼
SUPPORTED
   │
   ├────────────► CHALLENGED
   │
   ├────────────► SUPERSEDED
   │
   └────────────► REVOKED
   │
   ▼
PROMOTED
```

Nem toda claim precisa chegar a `PROMOTED`.

Algumas permanecem hipóteses úteis.

---

# 20. Evidence Ledger

O sistema deve considerar um **Evidence Ledger** lógico: histórico append-oriented das evidências usadas para claims relevantes.

Objetivos:

- auditoria;
- replay;
- comparação entre versões;
- detectar mudança de evidência;
- invalidar claims quando fonte é revogada;
- calcular blast radius;
- explicar decisão.

Não significa necessariamente blockchain ou tecnologia específica.

---

# 21. Relação com Learning Quarantine

Uma nova regra pode parecer excelente porque aprendeu em evidência contaminada.

Portanto todo Learning Candidate deve registrar:

```text
training_evidence_refs[]
evaluation_evidence_refs[]
holdout_refs[]
known_counterevidence[]
```

Se uma fonte importante for revogada, o sistema consegue localizar quais candidatos/modelos dependiam dela.

---

# 22. Relação com Explosão Atômica

A recursão deve distinguir:

```text
novo derivado
≠
nova evidência independente
```

Exemplo:

```text
Evento E1
  ↓
Derivado D1
  ↓
Derivado D2
  ↓
Hipótese H1
```

D1 e D2 podem trazer novas representações, mas não necessariamente duas evidências independentes para H1.

Esse princípio é obrigatório para evitar auto-reforço.

---

# 23. Relação com agentes e IA

Saída de agente é tratada como **Artifact**, não como verdade.

```text
AGENT OUTPUT
    │
    ▼
Cognitive Artifact
    │
    ▼
Evidence eligibility check
    │
    ├──► rejected / quarantined
    │
    └──► Evidence Item
```

Um LLM pode gerar hipótese, sumarizar evidência, procurar contradição ou sugerir relação.

Ele não ganha autoridade epistemológica especial por ser um LLM.

---

# 24. Evidence Quality

Cada Evidence Item pode receber dimensões separadas de qualidade.

Candidatas:

```text
source_reliability
method_reliability
independence
sample_adequacy
recency
scope_match
integrity
reproducibility
```

Evitar colapsar tudo cedo demais em um único número.

---

# 25. Explicabilidade mínima

Uma claim relevante deve poder responder:

```text
O QUE afirmamos?
POR QUE afirmamos?
QUAL evidência suporta?
QUAL contradiz?
DE ONDE veio?
QUANDO foi observada?
QUAL método produziu?
QUAL versão estava ativa?
QUAL incerteza permanece?
QUAL risco foi considerado?
```

---

# 26. Exemplo enterprise

Hipótese:

```text
H42
“Atualização Z aumenta falhas no fluxo de pagamentos.”
```

Fluxo:

```text
2.300 falhas observadas
        │
        ▼
SIGNAL A
falhas cresceram após update Z
        │
        ▼
SIGNAL B
crescimento concentrado em região R
        │
        ▼
EVIDENCE 1
associação temporal
        │
        ▼
CHALLENGER
compara regiões sem Z
        │
        ▼
COUNTER-EVIDENCE
região R também recebeu mudança de rede
        │
        ▼
HYPOTHESIS REFINED
Z sozinha não explica o efeito
        │
        ▼
NOVA INVESTIGAÇÃO
Z + network_change
```

O sistema melhorou a hipótese em vez de aumentar artificialmente a confiança da primeira história.

---

# 27. Testes mínimos do Evidence Model v0

O laboratório precisa verificar pelo menos:

1. duplicatas não multiplicam evidência como independentes;
2. derivados do mesmo ancestral não contam como novas fontes independentes;
3. score não é rotulado automaticamente como confidence;
4. evidence contraditória reduz suporte ou aumenta incerteza;
5. claim de causalidade exige nível de evidência superior a associação;
6. base rate pode derrubar padrões aparentes;
7. evidência expirada/obsoleta perde aplicabilidade conforme policy;
8. fonte revogada propaga impacto para claims dependentes;
9. LLM output não entra como verdade por default;
10. ação de alto risco exige threshold/policy superior;
11. lineage permite reconstruir todos os Evidence Items de uma claim;
12. calibration metrics podem ser executadas quando houver ground truth.

---

# 28. Invariantes do Evidence Model v0.1

```text
E01 — Signal não é Evidence automaticamente.
E02 — Evidence sempre aponta para origem e claim/hypothesis.
E03 — Score não é Confidence sem calibração.
E04 — Repetição não cria independência.
E05 — Derivação recursiva não cria evidência independente por default.
E06 — Correlation/association não vira causality silenciosamente.
E07 — Counter-evidence precisa ser representável.
E08 — Confidence não substitui Policy.
E09 — Evidence tem contexto temporal e de escopo.
E10 — Source revocation precisa poder propagar impacto.
E11 — Agent/LLM output é Artifact antes de poder ser Evidence.
E12 — Alto risco exige evidência e autoridade proporcionais.
E13 — Uma claim pode permanecer inconclusiva sem ser forçada para true/false.
E14 — Evidence relevante precisa ser auditável e versionada.
```

---

# 29. Questões em aberto

- modelo final de Evidence Item;
- fórmula de evidence aggregation;
- critérios de independência;
- calibração por tipo de capability;
- níveis formais de causalidade;
- decay temporal por domínio;
- thresholds por risk tier;
- modelo de source reliability;
- estratégia de Evidence Ledger;
- métricas obrigatórias por tipo de saída;
- tratamento de evidência privada/confidencial entre tenants;
- counterfactual testing em domínios que permitam;
- propagação de revogação em grafos muito grandes.

---

# 30. Frase-guia

> **A Eva não deve perguntar apenas “o que encontrei?”. Deve perguntar “o que sustenta isso, o que pode derrubar isso e quanta autoridade essa evidência realmente merece?”.**
