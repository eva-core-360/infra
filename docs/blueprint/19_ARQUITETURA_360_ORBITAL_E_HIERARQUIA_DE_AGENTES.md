# Eva Engine® — Arquitetura 360 Orbital e Hierarquia de Agentes

**Status:** base conceitual em validação  
**Função:** transformar a metáfora original do “360” em uma direção arquitetural testável para o Eva Engine®, sem expor mecânicas proprietárias ainda não documentadas.

---

# 1. O significado arquitetural de 360

A imagem de referência é:

```text
                     ┌───────────────────────────────┐
                     │       ÓRBITA 360              │
                     │ lentes · guards · agentes     │
                     │ evaluators · policies         │
                     │                               │
                     │        ↘   ↓   ↙              │
                     │      ┌───────────┐             │
                     │      │ EVA CORE  │             │
                     │      │  centro   │             │
                     │      └───────────┘             │
                     │        ↗   ↑   ↖              │
                     │                               │
                     └───────────────────────────────┘
```

O ponto central representa o **núcleo estável do motor**. A órbita representa um conjunto extensível de capacidades capazes de observar, filtrar, desafiar, enriquecer, validar e governar o que passa pelo Core.

O “360” não deve significar literalmente processamento infinito. A leitura técnica é **multifacetamento controlado**: um mesmo evento pode ser observado por várias lentes e mecanismos, desde que existam gatilhos, orçamento, limites e critérios de parada.

Princípio:

> **Um mesmo fato pode produzir múltiplas projeções; nenhuma projeção isolada deve ser confundida com a realidade inteira.**

---

# 2. A metáfora do espelho

A imagem do círculo espelhado é útil se traduzida com cuidado.

```text
                         LENTE A
                           /\
                          /  \
                         /    \
                        /      \
               LENTE B ◄──●──► LENTE C
                        \  CORE /
                         \     /
                          \   /
                           \ /
                         LENTE D
```

Um sinal que entra pode ser refletido em várias perspectivas:

```text
EVENTO ORIGINAL
      │
      ▼
REPRESENTAÇÃO CANÔNICA
      │
      ├──► lente temporal
      ├──► lente contextual
      ├──► lente semântica
      ├──► lente de privacidade
      ├──► lente de decisão
      └──► outras lentes ativadas
```

Essas projeções podem se cruzar e produzir novos sinais. Porém toda expansão deve manter:

- origem;
- versão;
- evidência;
- escopo;
- custo;
- confiança calibrada quando aplicável;
- profundidade;
- critério de parada.

A arquitetura busca **riqueza combinatória sem explosão combinatória**.

---

# 3. O motor não precisa usar a mesma lente para todo problema

**DECISÃO DE DIREÇÃO**

O Eva Engine® não deve possuir uma única forma de observar todos os fenômenos.

Ele deve poder selecionar conjuntos de lentes adequados ao contexto.

Exemplo:

```text
EVENTO
  │
  ▼
ORQUESTRADOR
  │
  ├── identifica contexto
  ├── consulta Capability Registry
  ├── consulta Lens Registry
  ├── consulta Policy
  ├── calcula orçamento
  └── monta plano de execução
          │
          ▼
      LENS STACK
```

Uma operação sensível pode ativar mais filtros e validação. Uma operação simples pode ser resolvida por uma função determinística barata.

Princípio:

> **Força não é executar tudo. Inteligência operacional também é saber o que não precisa acordar.**

---

# 4. Hierarquia de agentes

“Agente” é definido aqui como **unidade executora com responsabilidade limitada e contrato claro**. Não implica LLM, chamada externa ou custo de inferência.

Um agente pode ser:

- função pura;
- parser;
- regra;
- algoritmo estatístico;
- detector de anomalia;
- worker;
- modelo local;
- modelo externo opcional;
- processo de verificação;
- agente generativo, quando justificado.

Arquitetura conceitual:

```text
┌──────────────────────────────────────────────────────────────┐
│                     EVA ORCHESTRATOR                         │
│  plano · ordem · orçamento · dependências · cancelamento    │
└───────────────────────────┬──────────────────────────────────┘
                            │
            ┌───────────────┼────────────────┐
            ▼               ▼                ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│ INGRESS GUARDS  │ │ SPECIALISTS     │ │ CONTEXT AGENTS  │
│ schema          │ │ temporal        │ │ estado          │
│ origem          │ │ semântico       │ │ histórico       │
│ escopo          │ │ relação         │ │ dependências    │
│ privacidade     │ │ anomalia        │ │ memória         │
│ deduplicação    │ │ classificação   │ │ continuidade    │
└────────┬────────┘ └────────┬────────┘ └────────┬────────┘
         │                   │                   │
         └───────────────────┼───────────────────┘
                             ▼
                    ┌─────────────────┐
                    │ CROSSING LAYER  │
                    │ combina sinais │
                    └────────┬────────┘
                             ▼
                    ┌─────────────────┐
                    │ CHALLENGERS     │
                    │ refutam         │
                    │ testam          │
                    │ buscam conflito │
                    └────────┬────────┘
                             ▼
                    ┌─────────────────┐
                    │ EVALUATORS      │
                    │ qualidade       │
                    │ baseline        │
                    │ calibração      │
                    └────────┬────────┘
                             ▼
                    ┌─────────────────┐
                    │ OUTPUT GUARDS   │
                    │ policy          │
                    │ segurança       │
                    │ explicação      │
                    │ autorização     │
                    └────────┬────────┘
                             ▼
                    ┌─────────────────┐
                    │ RESULT / ACTION │
                    └─────────────────┘
```

---

# 5. Funções especiais na hierarquia

## 5.1 Orchestrator

Não é “o agente que sabe tudo”. É o componente responsável por montar e governar o plano de execução.

Deve poder responder:

- quais capacidades são necessárias;
- em qual ordem;
- quais podem executar em paralelo;
- quais dependem de outras;
- qual orçamento existe;
- quando parar;
- quando escalar para mecanismo mais caro;
- quando devolver silêncio/incerteza;
- quais políticas bloqueiam determinada rota.

## 5.2 Ingress Guards

Protegem a entrada antes da cognição:

```text
VALIDAR
NORMALIZAR
DEDUPLICAR
CLASSIFICAR ESCOPO
VERIFICAR ORIGEM
APLICAR PRIVACIDADE
REGISTRAR LINEAGE
```

## 5.3 Specialists

Produzem sinais especializados. Devem ser pequenos, substituíveis e avaliáveis de forma isolada.

## 5.4 Crossing Layer

Combina sinais de mecanismos diferentes. É uma das áreas com maior potencial de inteligência emergente e também maior risco de propagação de erro.

Toda composição precisa de teste específico; “duas boas heurísticas” não garantem uma boa composição.

## 5.5 Challenger / Critic

Tenta refutar hipóteses antes que sejam promovidas.

Pode executar testes como:

```text
remove duplicatas
compara grupo de controle
altera janela temporal
retira variável dominante
procura contradição
procura explicação alternativa
mede sensibilidade a threshold
```

Princípio:

> **Quanto maior a capacidade de encontrar padrões, maior deve ser a capacidade de desconfiar deles.**

## 5.6 Evaluator

Mede comportamento contra baseline e critérios definidos.

## 5.7 Output Guards

Protegem a saída:

- separação entre pista e conclusão;
- linguagem proporcional à confiança;
- autorização;
- privacidade;
- segurança;
- consistência epistemológica;
- explicabilidade mínima;
- política de ação.

---

# 6. Escalonamento por custo e necessidade

A hierarquia deve preferir o mecanismo mais barato que consiga responder adequadamente.

```text
NÍVEL 0  regra / lookup / cálculo
    │
    ▼ se insuficiente
NÍVEL 1  heurística / estatística local
    │
    ▼ se insuficiente
NÍVEL 2  busca semântica / modelo especializado local
    │
    ▼ se insuficiente e permitido
NÍVEL 3  agente/modelo mais pesado
    │
    ▼
NÍVEL 4  revisão humana / decisão externa
```

Os níveis acima são referência conceitual, não números finais aprovados.

Objetivo:

> **Escalar inteligência somente quando a incerteza e o valor do problema justificarem o custo.**

---

# 7. “Andar sobre ovos” como propriedade arquitetural

O motor não deve ser apenas potente. Deve conseguir modular sua força.

```text
CASO SIMPLES
→ poucas peças
→ baixa latência
→ baixo custo

CASO AMBÍGUO
→ mais lentes
→ mais verificação
→ linguagem cautelosa

CASO CRÍTICO
→ guards adicionais
→ challenger
→ evaluator
→ policy forte
→ possível revisão humana
```

Isso permite um motor que “empurra um caminhão” quando necessário e “anda sobre ovos” quando o risco exige delicadeza.

---

# 8. Hierarquia 32 → 12 → 8

Foi informado que o acervo privado de 32 lentes possui uma redução/agrupamento conceitual adicional, aproximadamente:

```text
32 LENTES
   │
   ▼
12 AGRUPAMENTOS / CAMADAS
   │
   ▼
8 NÚCLEOS / EIXOS
```

**Importante:** o pacote de 32 fichas analisado não contém de forma explícita e completa o mapa que determina quais lentes pertencem a cada grupo de 12 e de 8.

Há referências externas `N001`, `N002`, `N003`, `N004`, `N005` em algumas fichas, o que indica que o acervo original possuía camadas adicionais de organização, mas esse recorte não é suficiente para reconstruir o mapa sem risco de invenção.

Portanto:

- registrar a existência da hierarquia como pista legítima;
- não inventar o agrupamento;
- reconstruí-lo somente quando a fonte original estiver disponível ou a autora decidir explicitá-lo.

---

# 9. Contrato significa contrato técnico

Quando o Blueprint usa a palavra **contrato**, trata-se de contrato de software, não contrato jurídico.

Exemplo:

```text
AGENT CONTRACT

INPUT
- tipos aceitos
- schema
- contexto obrigatório

OUTPUT
- sinais produzidos
- estrutura
- possíveis erros

GUARANTEES
- determinismo quando aplicável
- idempotência quando aplicável
- lineage
- versionamento

LIMITS
- timeout
- orçamento
- escopo
- confiança mínima

POLICY
- permissões
- privacidade
- veto
```

O contrato técnico permite trocar a implementação interna sem quebrar o restante do motor.

---

# 10. Fundamentos matemáticos: precisão terminológica

O objetivo é basear cada mecanismo em fundamentos formais e testáveis — matemática, estatística, teoria de grafos, teoria da informação, otimização, teoria de filas, controle, álgebra, estruturas de dados e métodos experimentais quando apropriado.

Não se deve chamar algo de “lei física” apenas por analogia. Termos como órbita, gravidade e reflexão são metáforas arquiteturais enquanto não houver um modelo matemático explicitamente definido e validado.

Princípio:

> **Metáfora inspira a arquitetura. Fórmula, teste e evidência determinam o comportamento real.**

---

# 11. Diagramas como parte do Blueprint

**DECISÃO DE DOCUMENTAÇÃO**

A partir desta página, diagramas ASCII/caixa devem ser usados quando ajudarem a tornar arquitetura, fluxo, hierarquia ou dependências inequívocos.

Eles pertencem ao Markdown e podem ser lidos por:

- humanos;
- Cursor;
- agentes;
- GitHub;
- ferramentas de documentação.

Exemplo de notação:

```text
┌──────────┐     ┌──────────┐     ┌──────────┐
│  INPUT   │ ──► │ PROCESS  │ ──► │  OUTPUT  │
└──────────┘     └──────────┘     └──────────┘
```

Diagramas não substituem contratos formais, mas ajudam a impedir interpretações divergentes.

---

# 12. Questões abertas

- mapa exato 32 → 12 → 8;
- taxonomia final de tipos de agente;
- política de escalonamento entre mecanismos baratos e caros;
- formato do Execution Plan;
- formato do Agent Contract;
- mecanismo de cancelamento e timeout;
- política de paralelismo;
- orçamento cognitivo por evento;
- forma de votação/combinação de sinais;
- política de veto;
- quando o Challenger é obrigatório;
- relação final entre Lens Registry, Capability Registry e Agent Registry;
- conjunto mínimo de agentes para o primeiro Cognitive Kernel executável.

---

# 13. Frase-guia

> **O Core permanece no centro. As lentes observam. Os agentes executam. O Orchestrator coordena. O Challenger desconfia. Os Evaluators medem. As Policies limitam. A evidência decide o que merece sobreviver.**
