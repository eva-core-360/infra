# Eva Engine® — Contexto de Continuidade

**Função deste documento:** permitir que um novo chat, agente ou desenvolvedor retome o projeto sem reconstruir a conversa original e sem reduzir o Eva Engine® ao primeiro produto que inspirou seus mecanismos.

---

# 1. Estado atual do projeto

O projeto está na fase de **Blueprint arquitetural detalhado**, antes da implementação principal do novo Core.

A intenção é construir uma especificação suficientemente clara para que Cursor/agentes possam programar por módulos com testes, sem inventar arquitetura durante a implementação.

O repositório `eva-core-360/infra` é a fonte persistente de verdade do Blueprint.

**Foco vigente:** Eva Engine® como infraestrutura cognitiva generalista, extensível, mensurável, supervisionada e potencialmente utilizável em produtos e operações empresariais de grande escala.

---

# 2. Origem conceitual — importante, mas não limitante

A discussão começou a partir de mecanismos de um produto de anotações e memória pessoal.

Foram exploradas ideias como:

- pessoa no centro (“EU”);
- áreas da vida;
- continuidade;
- retomada;
- associação;
- gravidade/proximidade cognitiva;
- funcionamento principalmente determinístico e heurístico sem IA generativa ativa permanente.

Esses mecanismos serviram como primeiro laboratório para testar se regras pequenas, combinadas, poderiam produzir comportamento útil e percebido como inteligente.

**A origem em notas não define o novo Core.**

O protótipo de notas deve ser tratado como:

```text
LABORATORIO
+
EVIDENCIA HISTORICA
+
FONTE DE CASOS DE TESTE
```

não como arquitetura-alvo universal.

---

# 3. Virada fundamental

A arquitetura deixou de ser pensada como “motor de notas”.

A decisão central passou a ser:

> **Eva Engine® = Core generalista.**

> **Produtos = consumidores do motor.**

Princípio:

> **Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.**

Essa continua sendo uma das decisões arquiteturais mais importantes do projeto.

---

# 4. Nova ampliação de foco: motor empresarial

A ambição foi explicitamente elevada.

O Blueprint deve ser grande o suficiente para permitir que o Eva Engine® futuramente:

- sirva múltiplos produtos;
- opere em múltiplos domínios;
- receba eventos de sistemas diferentes;
- mantenha memória e contexto;
- relacione informação;
- aprenda continuamente sob supervisão;
- seja testável e auditável;
- seja implantável em cenários empresariais sérios;
- possa gerar impacto econômico quando isso for demonstrado em pilotos reais.

O projeto **não afirma hoje** que já atende grandes empresas ou economiza milhões. Essa é direção estratégica e hipótese de valor, a ser conquistada por evidência.

Regra:

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**

---

# 5. Três naturezas lógicas do motor

Desde o início foram escolhidas três naturezas de raciocínio que podem coexistir:

## Determinístico

Usado quando regras, parsing, validação, contexto conhecido ou cálculo explícito podem produzir comportamento previsível.

## Heurístico

Usa sinais e aproximações quando não existe certeza absoluta. Deve trabalhar com limites, evidência e incerteza.

## Preditivo

Usa histórico e padrões para estimar tendência futura sem transformar previsão em verdade.

A bateria anterior reforçou que mecanismos determinísticos podem produzir muito valor e que heurísticas precisam ser cuidadosamente calibradas e avaliadas.

---

# 6. Bateria experimental anterior

Foi realizado um laboratório com 508 cenários sobre mecanismos locais de um protótipo anterior.

Os resultados detalhados estão registrados em:

`16_LICOES_DO_LABORATORIO_INTELIGENCIA_LOCAL.md`

Lições principais:

- continuidade/retomada e busca local mostraram sinais fortes;
- mecanismos simples podem compor valor real;
- heurísticas de associação/classificação podem errar com confiança indevida;
- algumas abordagens degradaram com escala;
- recalcular estatística não é aprendizado contínuo real;
- explicabilidade e silêncio importam;
- teste pequeno positivo é justificativa para investigar, não prova empresarial.

Esse laboratório é evidência, não destino.

---

# 7. Aprendizado contínuo — definição vigente

Princípio:

> **Usar a Eva pode ensinar a Eva, mas promover o que foi aprendido exige governança.**

A arquitetura distingue pelo menos:

```text
L1 — aprendizado de sessão/contexto
L2 — aprendizado individual/tenant/organização
L3 — aprendizado de domínio
L4 — aprendizado global
```

Quanto maior o alcance, maior a necessidade de:

- evidência;
- evaluator;
- baseline;
- versionamento;
- aprovação;
- monitoramento;
- rollback.

Aprendizado não significa simplesmente que os dados mudaram. Deve existir alteração mensurável de comportamento ou parâmetros em função de evidência/feedback.

---

# 8. Crescimento exponencial — significado técnico

“Crescimento exponencial” não significa custo ou processamento descontrolado.

Significa **crescimento por composição**:

```text
novo idioma
+
Core existente
+
ontologia
+
contexto
+
aprendizado
=
mais capacidades em vários produtos
```

ou:

```text
novo Domain Pack
+
Event Engine
+
Memory Engine
+
Relation Engine
=
novo domínio sem reconstruir o Core
```

Documentação central: `15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`.

---

# 9. Três escalas que não devem ser confundidas

## Escala operacional

Volume de eventos, dados, tenants, concorrência, memória e processamento.

## Escala cognitiva

Quantidade/complexidade de contextos, relações, hipóteses, padrões e aprendizagem.

## Escala de domínio

Quantidade/diversidade de setores, produtos, ontologias e políticas especializadas.

Sucesso em uma dimensão não comprova as outras.

---

# 10. Engenharia em camadas — direção vigente

O Blueprint passa a investigar o motor como uma cadeia de responsabilidades:

```text
EVENTOS / DADOS
      ↓
SUBSTRATO DETERMINISTICO
      ↓
SINAIS
      ↓
REPRESENTACAO ESTRUTURADA
      ↓
CONTEXTO
      ↓
RECUPERACAO / MEMORIA
      ↓
RELACOES
      ↓
INFERENCIA
      ↓
APRENDIZADO
      ↓
EVALUATION PLANE
      ↓
ORQUESTRACAO / ORCAMENTO
      ↓
GOVERNANCA
      ↓
CAPABILITIES / INTEGRACOES
```

Cada camada deve poder ser testada isoladamente e em composição.

Documento principal desta mudança: `17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md`.

---

# 11. Ontologia universal

O Core não deve conhecer antecipadamente todas as áreas humanas ou empresariais.

Ele deve conhecer abstrações universais e meios de extensão:

```text
Event
Entity
Atom
Relation
Context
State
Time
Evidence
Inference
Feedback
Memory
Policy
Capability
Schema
```

Áreas da vida, categorias empresariais, especialidades médicas, departamentos ou tipos de contrato pertencem a Domain Packs/Schemas quando específicos.

---

# 12. “Infinita por dentro”

A visão não é manter uma lista infinita de categorias no Core.

É permitir hierarquias e relações extensíveis:

```text
DOMAIN
  └── CONTEXT
       └── SUBCONTEXT
            └── SUBJECT
                 └── ENTITY / EVENT / ATOM
                      └── RELATIONS
```

Essa profundidade não é rígida e pode variar por domínio.

---

# 13. Multilíngue desde a arquitetura

O Core não deve nascer em português para depois ser traduzido.

Language Packs convertem expressões de diferentes idiomas para conceitos internos neutros, por exemplo:

```text
ATOM_DECISION
ATOM_INTENTION
REL_CONTINUES
```

Adicionar idioma não deve exigir reconstruir a ontologia central.

---

# 14. Expansão Cognitiva Controlada

A ideia antiga de “explosão atômica” evoluiu para Expansão Cognitiva Controlada.

Um evento pode gerar átomos, ativar contexto, recuperar memória, criar relações candidatas e produzir inferências.

Mas todo ciclo precisa de orçamento:

- profundidade;
- candidatos;
- átomos;
- relações;
- confiança mínima;
- tempo;
- custo;
- memória;
- prioridade;
- escopo de privacidade.

O motor deve aprender também quando **não** expandir.

---

# 15. Evaluation Plane

Evaluators são parte da arquitetura.

Nenhuma mudança é “melhoria” apenas porque parece mais inteligente.

Capacidades devem ser comparadas contra baseline com métricas adequadas, como:

- precision;
- recall;
- F1;
- calibration;
- false positive/negative rate;
- top-k;
- cobertura;
- qualidade de silêncio;
- latência;
- custo;
- estabilidade;
- regressão;
- drift;
- impacto operacional/econômico quando houver piloto real.

---

# 16. Escada de evidência

O projeto agora distingue:

```text
E0 — ideia
E1 — prova de mecanismo
E2 — bateria reproduzível
E3 — escala sintética
E4 — piloto de domínio
E5 — prova operacional
E6 — prova econômica
```

A arquitetura pode nascer com ambição E6; nenhuma capacidade ganha esse status sem conquistar os degraus.

---

# 17. Fase privada de P&D

Na fase atual:

- documentação técnica permanece no repositório privado autorizado;
- datasets e resultados de teste permanecem privados salvo decisão explícita;
- intenção de teste não é publicada automaticamente;
- protótipos de produto não precisam ser expostos para especificar o Core;
- resultados internos não devem virar alegações públicas sem revisão.

---

# 18. Stack atual

Direção inicial:

- Cursor para programação assistida;
- GitHub para fonte de verdade e versionamento;
- TypeScript como linguagem principal;
- monólito modular;
- PostgreSQL/Supabase;
- vetores no Postgres quando necessário;
- API HTTP/REST primeiro;
- background workers para processamento profundo;
- providers intercambiáveis para embeddings/IA;
- dataset JSON/JSONL versionado;
- testes unitários, multilíngues, regressão, golden tests, red team, holdout e escala sintética.

Essas são direções iniciais, não dogmas eternos.

---

# 19. Como continuar em um novo chat

Um novo chat NÃO deve reconstruir o projeto do zero e NÃO deve voltar automaticamente para o produto de notas.

Fluxo recomendado:

1. Ler `00_BLUEPRINT_MESTRE.md`.
2. Ler `01_REGISTRO_DECISOES.md`.
3. Ler este arquivo.
4. Ler `15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`.
5. Ler `17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md`.
6. Ler `AGENTS.md`.
7. Identificar a frente arquitetural vigente.
8. Continuar do estado atual.
9. Atualizar documentação quando decisão estrutural mudar.

Evitar pedir novamente explicação do projeto se ela estiver no repositório.

---

# 20. Próxima frente de trabalho

A próxima frente prioritária é definir **Cognitive Kernel + Evidence Model + Evaluation Plane** de forma coordenada.

Questões centrais:

- quais estruturas são realmente irredutíveis no Core;
- como representar evidência;
- como separar score de confidence;
- como modelar incerteza;
- como compor sinais sem amplificar erro;
- como medir melhoria;
- como aprender sem contaminar escopos maiores;
- como promover e reverter comportamento aprendido.

---

# 21. Princípio de trabalho

O Blueprint é vivo.

Preferir:

- base vigente;
- decisão aprovada;
- versão atual;
- hipótese em validação;
- pronto para testar.

A arquitetura pode evoluir, desde que a mudança seja explícita, documentada e testável.

Frase-guia desta fase:

> **Não estamos construindo um bloco de notas que ficou grande. Estamos construindo um motor que começou pequeno o suficiente para ser testado.**
