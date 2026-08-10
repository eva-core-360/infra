# Eva Engine® — Explosão Atômica Recursiva e Escalonamento de IA

**Status:** base conceitual vigente, em evolução  
**Função:** formalizar a ideia de que o processamento do Eva Engine® não termina na primeira resposta. Cada ciclo pode produzir novos derivados, metadados, hipóteses e candidatos de aprendizagem que retornam ao motor como novas ondas de processamento, sob limites explícitos e supervisão.

---

# 1. A mudança essencial

Até aqui, a Expansão Cognitiva Controlada podia ser interpretada como:

```text
entrada
  ↓
atomização
  ↓
relações
  ↓
inferência
  ↓
resultado
```

A visão vigente acrescenta uma etapa decisiva:

> **O resultado não é necessariamente o fim. Ele pode produzir novos derivados que retornam ao motor como uma nova onda cognitiva.**

Portanto, o modelo passa a ser recursivo:

```text
ENTRADA ORIGINAL
      │
      ▼
┌───────────────┐
│ PROCESSAMENTO │
└───────┬───────┘
        │
        ▼
     RESULTADO
        │
        ├──────────────► saída consumível
        │
        └──────────────► DERIVADOS COGNITIVOS
                              │
                              ▼
                      nova fragmentação
                              │
                              ▼
                       nova onda/evento
                              │
                              └──────────────┐
                                             ▼
                                      PROCESSAMENTO
```

Essa realimentação controlada é a interpretação técnica atual de **Explosão Atômica**.

---

# 2. Explosão Atômica não é explosão combinatória

**DECISÃO APROVADA COMO PRINCÍPIO**

Explosão Atômica significa expansão recursiva de capacidade e informação útil, não criação ilimitada de nós, relações ou processamento.

Toda nova onda deve justificar sua existência por valor marginal.

A arquitetura deve possuir limites como:

```text
max_depth
max_waves
max_branches
max_new_atoms
max_new_relations
minimum_confidence
minimum_novelty
minimum_information_gain
time_budget
compute_budget
cost_budget
privacy_scope
risk_budget
stop_condition
```

Princípio:

> **A Eva pode continuar pensando mecanicamente enquanto cada nova onda produz informação nova suficiente para justificar o custo e o risco.**

---

# 3. Três saídas de cada ciclo

Cada ciclo cognitivo deve ser conceitualmente capaz de produzir três categorias separadas.

## 3.1 Resultado externo

O que será devolvido ao produto, processo ou consumidor.

Exemplos:

- resposta;
- sugestão;
- classificação;
- alerta;
- relação encontrada;
- estado atualizado;
- ação candidata.

## 3.2 Derivados cognitivos

Novas estruturas produzidas durante o processamento e que podem alimentar ondas futuras.

Exemplos:

```text
novo átomo
nova relação
novo contexto
novo estado
novo metadado
nova evidência
novo padrão candidato
nova contradição
nova anomalia
nova hipótese
novo alias
novo vínculo temporal
novo agrupamento
```

## 3.3 Candidatos de aprendizagem

Algo observado durante o ciclo pode sugerir mudança futura de comportamento.

Isso NÃO significa promover uma nova heurística automaticamente.

Exemplos:

```text
weight_adjustment_candidate
rule_candidate
association_candidate
threshold_candidate
lens_activation_candidate
routing_candidate
personal_semantic_candidate
```

Esses candidatos entram no Learning Plane e precisam obedecer à governança adequada ao seu alcance.

---

# 4. A palavra correta para o que “volta”

A expressão informal “volta com uma nova heurística” descreve bem a intuição, mas arquiteturalmente precisamos distinguir:

```text
DERIVED SIGNAL
  algo novo extraído neste ciclo

COGNITIVE DERIVATIVE
  estrutura nova criada pelo processamento

LEARNING CANDIDATE
  proposta de alteração futura de comportamento

LEARNED STATE
  alteração já avaliada e promovida
```

Portanto, uma resposta não deve automaticamente criar uma nova regra global.

Ela pode criar **candidatos de aprendizagem e derivados cognitivos** que serão avaliados posteriormente.

---

# 5. Ondas cognitivas

A recursão será modelada em **ondas** ou **gerações**.

```text
WAVE 0
entrada original
    │
    ▼
WAVE 1
derivados primários
    │
    ▼
WAVE 2
relações e hipóteses secundárias
    │
    ▼
WAVE 3
contraprovas, padrões e contexto ampliado
    │
    ▼
STOP
quando o ganho marginal não justificar continuar
```

Cada onda deve carregar lineage explícito.

Campos conceituais:

```text
root_event_id
wave_id
wave_depth
parent_derivation_id
origin_module
origin_lens
origin_agent
created_at
engine_version
ontology_version
confidence
novelty_score
information_gain
risk_score
cost_so_far
stop_reason
```

Isso permite reconstruir exatamente como uma conclusão emergiu.

---

# 6. Diagrama 360 da Explosão Atômica

```text
                         ┌─────────────────────┐
                         │    EVENTO RAIZ      │
                         └──────────┬──────────┘
                                    │
                                    ▼
                          ┌──────────────────┐
                          │     EVA CORE     │
                          └────────┬─────────┘
                                   │
                    ┌──────────────┼──────────────┐
                    ▼              ▼              ▼
                 LENTE A        LENTE B        LENTE C
                    │              │              │
                    └───────┬──────┴──────┬───────┘
                            ▼             ▼
                         SINAIS       CONTEXTO
                            └──────┬──────┘
                                   ▼
                              CROSSING
                                   │
                   ┌───────────────┼────────────────┐
                   ▼               ▼                ▼
                ÁTOMO           RELAÇÃO          HIPÓTESE
                   │               │                │
                   └───────────────┼────────────────┘
                                   ▼
                              CHALLENGER
                                   │
                                   ▼
                              EVALUATION
                                   │
                    ┌──────────────┴──────────────┐
                    ▼                             ▼
               RESULTADO                    DERIVADOS
                                                  │
                                      fragmentação / metadados
                                                  │
                                                  ▼
                                             NOVA ONDA
                                                  │
                                                  └──────► EVA CORE
```

Esse loop pode repetir até uma condição de parada.

---

# 7. O que pode gerar uma nova onda

Uma nova onda não precisa vir apenas de texto ou de um novo usuário.

Ela pode nascer de:

```text
novo átomo
relação descoberta
mudança de confiança
contradição detectada
novo contexto
feedback recebido
resultado de ação
mudança temporal
anomalia
quebra de padrão
nova evidência
resposta de agente
veto de policy
falha de verificação
```

Portanto, o próprio motor produz eventos internos capazes de acordar partes diferentes de si.

---

# 8. Critério de continuação

A explosão deve continuar apenas quando houver justificativa mensurável.

Modelo conceitual inicial:

```text
CONTINUE if

novelty_score        >= threshold
AND information_gain >= threshold
AND confidence       >= minimum
AND risk             <= budget
AND cost             <= budget
AND depth            <= max_depth
AND privacy_scope    permits
```

A fórmula real ainda precisa de experimento.

O ponto arquitetural é que a Eva deve conhecer duas capacidades igualmente importantes:

> **como expandir**

> **quando parar de expandir**

---

# 9. IA não é eliminada; é escalada

**DECISÃO APROVADA COMO DIREÇÃO**

O objetivo não é eliminar 100% da IA/modelos externos.

O objetivo é resolver o máximo possível com mecanismos:

- determinísticos;
- matemáticos;
- estatísticos;
- algoritmos clássicos;
- modelos locais quando fizer sentido;
- agentes sem custo variável de API quando possível;

antes de escalar para inteligência externa mais cara ou menos previsível.

“Gratuito” deve ser entendido tecnicamente como **sem custo variável de chamada externa**, não como custo computacional literalmente zero.

---

# 10. Escada de escalonamento cognitivo

Direção conceitual:

```text
L0 — PURE MECHANICS
│    regras, validação, parsing, cálculo, índices
│
▼
L1 — LOCAL HEURISTICS / STATISTICS
│    ranking, frequência, anomalia, coocorrência controlada
│
▼
L2 — LOCAL SPECIALISTS
│    algoritmos especializados, modelos pequenos/locais quando justificáveis
│
▼
L3 — AGENT ENSEMBLE
│    especialistas coordenados, challenger, verificadores
│
▼
L4 — SUPERVISORY AI
│    um ou mais agentes/modelos de IA de maior custo/capacidade
│    acionados apenas quando risco, ambiguidade ou valor justificarem
│
▼
L5 — HUMAN AUTHORITY
     revisão/aprovação quando política, risco ou impacto exigirem
```

Essa hierarquia não é rígida; um domínio pode pular níveis ou bloquear níveis conforme Policy.

---

# 11. Supervisory AI Plane

A IA de maior capacidade não deve necessariamente ficar no caminho quente de toda operação.

Uma arquitetura possível é colocá-la acima da malha mecânica:

```text
                 ┌──────────────────────────┐
                 │  SUPERVISORY AI PLANE    │
                 │                          │
                 │  review · arbitrate      │
                 │  challenge · synthesize  │
                 │  investigate · escalate  │
                 └─────────────┬────────────┘
                               │
                        somente quando
                         necessário
                               │
                               ▼
┌─────────────────────────────────────────────────────┐
│             EVA MECHANICAL COGNITIVE FABRIC         │
│                                                     │
│ guards → lenses → specialists → crossing → critic  │
│       → evaluators → policies → derivatives         │
└─────────────────────────────────────────────────────┘
```

Benefícios esperados:

- reduzir custo variável;
- reduzir dependência de fornecedor;
- aumentar previsibilidade;
- preservar privacidade quando possível;
- reservar IA pesada para casos em que realmente agrega valor;
- permitir comparação entre resultado mecânico e supervisão inteligente.

---

# 12. Agentes de entrada e saída

A sugestão de agentes/filtros nas extremidades deve ser preservada.

## Ingress Agents / Guards

Podem verificar:

```text
schema
origem
integridade
permissão
escopo
PII/sensibilidade
normalização
duplicidade
inconsistência
input adversarial
```

## Egress Agents / Guards

Podem verificar:

```text
assertividade indevida
contradição
insuficiência de evidência
vazamento de informação
política
risco
linguagem
explicabilidade
necessidade de revisão humana
```

O motor pode ser excelente e ainda assim precisar dessas barreiras.

---

# 13. Meta-orquestração

Se existirem muitos agentes, alguém precisa administrar os próprios administradores.

Portanto, o Blueprint deve prever **meta-orquestração**.

Responsabilidades possíveis:

```text
selecionar agentes
resolver conflito entre agentes
controlar concorrência
aplicar orçamento
impedir loops
medir qualidade por agente
rebaixar agentes ruidosos
promover rotas mais eficientes
escalar para IA supervisora
encerrar processamento
```

Isso não implica um único “superagente”. Pode ser uma combinação de regras, políticas e módulos de coordenação.

---

# 14. Explosão Atômica como criação de informação derivada

A ideia central pode ser resumida assim:

```text
1 observação
   ↓
N projeções
   ↓
M cruzamentos úteis
   ↓
novos derivados
   ↓
novas ondas
   ↓
novas relações / hipóteses / evidências
```

Mas toda nova informação precisa manter vínculo com sua origem.

Regra:

> **Nenhum átomo derivado deve perder a trilha que permite voltar ao evento ou evidência que o originou.**

---

# 15. O ciclo completo

```text
OBSERVAR
  ↓
PRESERVAR
  ↓
ATOMIZAR
  ↓
CONTEXTUALIZAR
  ↓
SELECIONAR LENTES
  ↓
EXECUTAR ESPECIALISTAS
  ↓
CRUZAR SINAIS
  ↓
INFERIR
  ↓
DESAFIAR
  ↓
AVALIAR
  ↓
POLICY
  ↓
RESPONDER
  ↓
GERAR DERIVADOS
  ↓
FRAGMENTAR DERIVADOS
  ↓
REENTRAR COMO NOVA ONDA
  ↓
APRENDER / CANDIDATAR APRENDIZAGEM
  ↓
PARAR QUANDO O GANHO MARGINAL TERMINAR
```

---

# 16. Novas perguntas de pesquisa

**QUESTÕES EM ABERTO**

1. Qual métrica representa melhor `information_gain` entre ondas?
2. Como distinguir novidade real de reformulação do mesmo conteúdo?
3. Quantas ondas produzem ganho antes de começar a gerar ruído?
4. Quais tipos de derivados podem reentrar automaticamente?
5. Quais exigem Challenger antes de reentrada?
6. Quais exigem supervisão de IA?
7. Como medir contribuição marginal de cada lente/agente?
8. Quando um learning candidate pode virar learned state?
9. Como impedir loops auto-reforçados de inferências erradas?
10. Como comparar custo marginal de mais mecânica versus escalada para IA?

Essas perguntas devem virar experimentos reproduzíveis no Evaluation Plane.

---

# 17. Frase de arquitetura

> **A Explosão Atômica não termina na resposta. A resposta deixa resíduos cognitivos rastreáveis; esses resíduos podem se fragmentar em novos átomos, relações, evidências e candidatos de aprendizagem, formando novas ondas até que o ganho marginal deixe de justificar continuar.**

E, em paralelo:

> **A Eva deve usar IA onde IA agrega valor — não onde uma mecânica mais barata, previsível e comprovável já resolve o problema.**
