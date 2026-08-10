# Eva Engine® — Lentes Cognitivas e Orquestração

**Status:** base conceitual em validação  
**Origem:** análise de um acervo privado de 32 fichas neuro/cognitivas previamente criado pela autora do projeto. O acervo original não é reproduzido aqui; este documento registra apenas a leitura arquitetural extraída dele.

---

# 1. Conclusão principal

O acervo de 32 fichas possui valor para o Eva Engine®, mas **não deve ser incorporado ao Core como uma lista de 32 primitivas atômicas rígidas**.

A leitura mais promissora é tratá-lo como uma biblioteca de **Lentes Cognitivas**: perspectivas especializadas que podem ser ativadas, combinadas, ponderadas e supervisionadas conforme o contexto do problema.

Princípio:

> **Uma lente isolada descreve. O cruzamento de lentes pode produzir capacidade.**

Isso preserva a intenção original do material: os arquivos isolados são referências; o valor aparece quando múltiplas áreas se cruzam sobre um mesmo evento, contexto ou decisão.

---

# 2. Cuidado terminológico

As 32 fichas não pertencem todas à neurociência estrita. O conjunto mistura, de forma explícita e geralmente bem sinalizada:

- neurociência;
- ciência cognitiva;
- psicologia;
- HCI/UX;
- linguística;
- semiótica;
- arquitetura da informação;
- privacidade;
- engenharia de software;
- interação humano-computador;
- frameworks e heurísticas de produto.

Muitas fichas registram corretamente quando uma evidência é estabelecida, contestada, heurística, filosófica ou apenas prática de engenharia.

Por isso, para o Blueprint do motor, o termo preferido deve ser **Cognitive Lens / Lente Cognitiva**, e não “área neurocientífica” como afirmação científica universal.

Isso evita transformar uma biblioteca multidisciplinar útil em marketing de “neuro” impreciso.

---

# 3. Estrutura de rede encontrada no acervo

Considerando apenas as referências internas `neuro-XX` presentes nos campos `VIZINHOS`:

- 32 fichas analisadas;
- 64 ligações internas entre fichas;
- as 32 fichas formam uma única rede conectada;
- existem referências externas do tipo `N001`, `N002`, etc., não presentes neste pacote, portanto o grafo completo original provavelmente é ainda maior.

Hubs internos mais conectados no recorte analisado:

```text
neuro-18  Contexto                 grau 8
neuro-08  Semântica                grau 7
neuro-21  Retomada                 grau 7
neuro-14  Fluxo                    grau 6
neuro-24  Metadados                grau 6
```

Esse resultado é importante porque confirma estruturalmente a hipótese de cruzamento: o material não foi escrito como 32 ilhas independentes.

---

# 4. Quatro famílias emergentes

Uma análise do grafo interno sugere quatro agrupamentos úteis para arquitetura. Eles não são “verdades científicas”; são uma forma de organizar o acervo para testes.

## 4.1 Percepção, interação e carga

Exemplos de lentes:

- Design;
- Visual;
- UX;
- Cognição;
- Atenção;
- Emocional;
- Interação;
- Estética;
- Adaptação.

Função provável no Eva Engine®:

- avaliar como uma capacidade é apresentada;
- controlar carga cognitiva;
- proteger previsibilidade;
- reduzir atrito;
- modular feedback e interação.

Essa família tende a pertencer mais ao **Presentation/Product Plane** do que ao Cognitive Kernel.

## 4.2 Contexto, decisão e governança

Exemplos:

- Intuição;
- Consciência Contextual;
- Orquestração Cognitiva;
- Inteligência Expandida;
- Metadados;
- Presença;
- Privacidade;
- Decisão;
- Metacognição/Consciência.

Função provável:

- decidir quais mecanismos acordam;
- separar pista de conclusão;
- manter humano no circuito;
- proteger escopo e privacidade;
- explicar o que o motor sabe;
- governar inferências e ações.

Esta família é especialmente relevante para o Eva Engine® empresarial.

## 4.3 Continuidade, memória e ação

Exemplos:

- Temporal;
- Memória;
- Energia;
- Fluxo;
- Comportamento;
- Retomada;
- Produtividade.

Função provável:

- manter continuidade;
- reconstruir contexto;
- modelar passagem do tempo;
- reduzir custo de retomada;
- transformar intenção em próxima ação quando o domínio permitir.

## 4.4 Estrutura, semântica e representação

Exemplos:

- Arquitetura da Informação;
- Semântica;
- Associação;
- Percepção Espacial;
- Adaptabilidade Estrutural;
- Semiótica;
- Linguística.

Função provável:

- estruturar conhecimento;
- representar relações;
- organizar hierarquias extensíveis;
- construir pistas semânticas;
- permitir evolução sem reescrever o Core.

---

# 5. Lente não é agente, regra nem modelo

Uma **Lente Cognitiva** é uma especificação de perspectiva.

Ela pode ser implementada por diferentes mecanismos:

```text
regra determinística
heurística
estatística
algoritmo de busca
modelo local
modelo externo opcional
agente especializado
combinação de mecanismos
```

Portanto:

> **Lens = o que observar e quais limites respeitar.**

> **Mechanism = como produzir o sinal.**

> **Agent = unidade executora/orquestrada, quando essa forma de execução fizer sentido.**

Essa separação evita acoplar uma ideia cognitiva a uma tecnologia específica.

---

# 6. Cognitive Lens Registry

O Eva Engine® deve avaliar a criação de um **Cognitive Lens Registry** separado do Schema Registry e do Capability Registry.

Cada lente poderia possuir contrato semelhante a:

```text
lens_id
version
name
scope
purpose
triggers
required_inputs
required_context
evidence_requirements
produced_signals
confidence_policy
compatible_lenses
conflicting_lenses
privacy_class
cost_class
latency_class
activation_budget
veto_conditions
evaluator_id
provenance
```

Uma lente não precisa estar ativa o tempo todo.

---

# 7. Lens Stack

Para um evento específico, o Orchestrator pode montar uma pilha temporária de lentes.

Exemplo genérico:

```text
EVENTO
  ↓
Contexto
  ↓
LENS SELECTOR
  ↓
[Temporal]
[Metadados]
[Semântica]
[Associação]
[Decisão]
[Privacidade]
  ↓
SINAIS
  ↓
SÍNTESE CONTROLADA
```

Outro contexto pode ativar apenas:

```text
[Privacidade]
[Metadados]
[Temporal]
```

Princípio:

> **Não acordar 32 lentes para cada evento.**

A inteligência está também em escolher **quais lentes não usar**.

---

# 8. Regras de cruzamento

O cruzamento entre lentes deve ser explícito e testável.

Cada composição deve poder declarar:

```text
inputs
lenses_activated
order
parallelism
cross_signals
conflict_resolution
stop_conditions
output_type
required_evaluator
```

Exemplo conceitual:

```text
Contexto
 + Temporal
 + Metadados
 + Memória
 + Retomada
 = candidato a Capability de Continuidade
```

Outro:

```text
Semântica
 + Associação
 + Contexto
 + Intuição
 + Decisão
 = sugestão contextual com incerteza explícita
```

Outro:

```text
Orquestração
 + Privacidade
 + Inteligência Expandida
 + Metadados
 + Decisão
 = execução assistida com trilha de auditoria e veto
```

Essas composições são **hipóteses de engenharia**, não capacidades aprovadas até serem testadas.

---

# 9. Arquitetura de agentes sugerida

A ideia de agentes em diferentes pontos do fluxo é compatível com o Blueprint, desde que “agente” não seja sinônimo de LLM autônomo.

O termo pode representar um executor especializado, inclusive totalmente determinístico e local.

Estrutura candidata:

```text
INPUT
  ↓
INGRESS GUARD
  - schema
  - normalização
  - privacidade
  - deduplicação
  ↓
CONTEXT BUILDER
  ↓
LENS SELECTOR
  ↓
SPECIALIST AGENTS / PROCESSORS
  - temporal
  - semântico
  - relação
  - anomalia
  - domínio
  - determinísticos específicos
  ↓
CHALLENGER / CRITIC
  - tenta refutar
  - procura conflito
  - procura evidência insuficiente
  ↓
SYNTHESIZER
  ↓
EVIDENCE + POLICY GATE
  - confiança calibrada
  - proveniência
  - autorização
  - privacidade
  - custo
  ↓
OUTPUT
```

Em paralelo, fora do caminho crítico:

```text
EVALUATOR
LEARNING GOVERNOR
DRIFT MONITOR
PROMOTION PIPELINE
```

---

# 10. Agente “gratuito” e economia de runtime

Parte importante da visão é que muitos agentes podem ser baratos ou praticamente sem custo marginal de IA porque são:

- funções puras;
- regras;
- índices;
- comparadores;
- filtros;
- classificadores locais;
- validadores;
- estatística;
- cache;
- bancos/consultas;
- workers locais;
- modelos pequenos quando justificados.

Assim, o motor não precisa contratar raciocínio generativo caro para tarefas que uma mecânica previsível resolve melhor.

Princípio:

> **Use inteligência cara somente onde a mecânica barata não alcança qualidade suficiente e o ganho foi demonstrado por teste.**

---

# 11. O papel do Supervisor / Maestro

A ficha de Orquestração Cognitiva possui valor arquitetural especial.

O Supervisor não deve “pensar tudo”. Ele deve:

- receber o objetivo operacional;
- observar contexto disponível;
- ativar capacidades necessárias;
- respeitar orçamento de tempo/custo;
- controlar profundidade;
- resolver dependências;
- impedir loops;
- registrar decisão de roteamento;
- aplicar políticas;
- parar a cadeia quando evidência é insuficiente.

Ele pode ser determinístico na maior parte do tempo.

Casos ambíguos podem, futuramente, acionar mecanismos mais sofisticados sob política.

---

# 12. Entrada, meio e saída devem ter controles diferentes

## 12.1 Entrada

Objetivo: proteger o sistema de dado ruim antes de interpretação.

Possíveis guards:

- validade de schema;
- formato;
- normalização;
- idioma;
- duplicação;
- origem;
- permissões;
- sensibilidade;
- escopo de tenant;
- integridade temporal.

## 12.2 Meio

Objetivo: produzir sinais sem transformar hipótese em fato.

Possíveis controles:

- orçamento cognitivo;
- isolamento de contexto;
- provenance;
- limiar de confiança;
- candidatos máximos;
- anti-apofenia;
- conflito entre lentes;
- cross-check.

## 12.3 Saída

Objetivo: impedir que resultado frágil se apresente como certeza ou execute algo indevido.

Possíveis guards:

- evidence check;
- calibration;
- contradiction check;
- privacy/redaction;
- policy;
- permission;
- action scope;
- linguagem de incerteza;
- auditoria.

---

# 13. “Anti-apofenia” deve virar requisito

O material de Associação já reconhece explicitamente o risco de ver padrão onde não existe.

Essa ideia deve subir de uma ficha local para requisito do motor:

> **Quanto mais o Eva Engine® combinar sinais, maior deve ser sua capacidade de tentar refutar a relação criada.**

Isso sugere mecanismos como:

- challenger;
- negative controls;
- ablation tests;
- comparação com baseline;
- penalidade por relação genérica;
- minimum support;
- confidence calibration;
- detecção de duplicatas;
- avaliação fora da amostra.

---

# 14. O valor empresarial das lentes

Em ambiente empresarial, uma lente deixa de ser “como melhorar a experiência de notas” e pode virar um modo de observação operacional.

Exemplo abstrato:

```text
Temporal     → quando o fenômeno aparece?
Contexto     → em qual condição operacional?
Metadados    → origem, estado, versão, responsável?
Associação   → com que outros eventos coocorre?
Semântica    → quais eventos significam a mesma coisa com palavras diferentes?
Decisão      → existe evidência suficiente para recomendar ação?
Privacidade  → quais dados podem participar desta análise?
Orquestração → quais capacidades devem acordar agora?
```

O mesmo Lens Registry pode servir domínios diferentes, enquanto Domain Packs fornecem o vocabulário especializado.

---

# 15. O que NÃO deve acontecer

Evitar:

- transformar as 32 fichas em 32 microserviços;
- ligar todas as lentes em todos os eventos;
- afirmar que toda ficha é neurociência comprovada;
- acoplar uma lente a um fornecedor de IA;
- permitir que um agente auto-promova conclusão global;
- misturar contexto de tenants;
- tratar associação como causalidade;
- confundir “score” com “confidence”;
- esconder qual lente contribuiu para um resultado;
- expor mecânica proprietária em documentação que não precise dela.

---

# 16. Proteção de propriedade intelectual

A arquitetura deve separar:

```text
CONTRATO ARQUITETURAL
- o que entra
- o que sai
- invariantes
- segurança
- métricas
- interfaces

MECÂNICA PROPRIETÁRIA
- pesos
- regras específicas
- sequenciamento especial
- combinações internas
- thresholds
- fórmulas
- estratégias de ativação
```

O Blueprint pode documentar contratos e princípios sem revelar a implementação proprietária que produz vantagem competitiva.

---

# 17. Próximos testes sugeridos

Antes de incorporar Lenses como capacidade oficial do Core:

1. Criar 5 a 8 `Lens Stacks` experimentais.
2. Para cada stack, definir hipótese falsificável.
3. Criar baseline sem cruzamento.
4. Medir ganho do cruzamento.
5. Medir custo, latência e ruído.
6. Executar ablation: remover uma lente por vez.
7. Testar conflito entre lentes.
8. Testar comportamento com contexto insuficiente.
9. Testar entrada adversarial.
10. Medir se o Supervisor escolheu menos mecanismos sem perder qualidade.

Uma lente só entra no Capability Registry quando houver evidência de que sua ativação ou composição melhora algum objetivo mensurável.

---

# 18. Decisão de arquitetura proposta

**PROPOSTA PARA BASE VIGENTE:**

- preservar as 32 fichas como patrimônio conceitual privado;
- não incorporá-las literalmente como ontologia atômica universal;
- criar o conceito de **Cognitive Lens**;
- estudar um `Cognitive Lens Registry`;
- permitir composição por `Lens Stack`;
- usar Orchestrator/Supervisor para ativação seletiva;
- permitir agentes determinísticos, heurísticos ou baseados em modelos;
- manter agentes críticos/guards em entrada e saída;
- exigir evaluator para promover composição como capability;
- manter mecânica proprietária separada dos contratos arquiteturais.

Frase-guia:

> **O átomo descreve o que existe. A lente decide como observar. A capacidade nasce do cruzamento. O orquestrador decide quando acordar cada parte.**
