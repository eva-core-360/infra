# Eva Engine® — Infra & Blueprint

Este repositório é a fonte de verdade arquitetural do **Eva Engine®**, núcleo cognitivo generalista que dará origem a produtos próprios e poderá futuramente servir como infraestrutura e serviço para organizações de grande escala.

## Regra de continuidade

Antes de propor arquitetura, código ou decisões estruturais, qualquer pessoa ou agente deve ler, nesta ordem:

1. `docs/blueprint/00_BLUEPRINT_MESTRE.md`
2. `docs/blueprint/01_REGISTRO_DECISOES.md`
3. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
4. `docs/blueprint/15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`
5. `docs/blueprint/17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md`
6. `docs/blueprint/18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md`
7. `docs/blueprint/19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md`
8. `AGENTS.md`

Depois, consultar os documentos específicos da área em que irá trabalhar.

## Princípio central

> Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.

O Eva Memory® e protótipos anteriores são laboratórios e consumidores do motor; **não definem o teto conceitual do Core**.

## Princípio de escala

> **Nascer pequeno na implementação não significa nascer pequeno na arquitetura.**

O Eva Engine® deve crescer por composição: novos idiomas, schemas, Domain Packs, capabilities, providers, relações e mecanismos de aprendizagem devem ampliar o sistema sem exigir reconstrução do núcleo.

Aprendizado contínuo é desejado, porém sua promoção deve ser supervisionada, versionada, mensurável e reversível.

## Princípio de evidência

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**

O projeto distingue ideia, prova de mecanismo, bateria reproduzível, escala sintética, piloto de domínio, prova operacional e prova econômica. A arquitetura pode nascer com ambição empresarial alta; cada capacidade precisa conquistar os degraus de evidência.

## Blueprint atual

```text
infra/
├── README.md
├── AGENTS.md
└── docs/
    └── blueprint/
        ├── 00_BLUEPRINT_MESTRE.md
        ├── 01_REGISTRO_DECISOES.md
        ├── 02_CONTEXTO_CONTINUIDADE.md
        ├── 03_ROADMAP_IMPLEMENTACAO.md
        ├── 04_ONTOLOGIA_V0.md
        ├── 05_EVENTOS_V0.md
        ├── 06_ATOMIZACAO.md
        ├── 07_APRENDIZADO_CONTINUO.md
        ├── 08_MULTILINGUE_E_FILTROS.md
        ├── 09_GRAVIDADE_COGNITIVA.md
        ├── 10_STACK_E_FERRAMENTAS.md
        ├── 11_TESTES_E_DATASET.md
        ├── 12_POLICY_PRIVACIDADE_SEGURANCA.md
        ├── 13_MODELO_DE_DADOS_V0.md
        ├── 14_DOMAIN_PACK_MEMORY.md
        ├── 15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md
        ├── 16_LICOES_DO_LABORATORIO_INTELIGENCIA_LOCAL.md
        ├── 17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md
        ├── 18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md
        └── 19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md
```

## Evidência experimental preservada

`16_LICOES_DO_LABORATORIO_INTELIGENCIA_LOCAL.md` registra achados de uma bateria anterior com 508 cenários sobre mecanismos locais de um protótipo. O documento é tratado como **evidência histórica**, não como arquitetura-alvo: reaproveitamos método, métricas e falhas observadas sem transportar automaticamente limitações do protótipo para o novo Core.

`18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md` registra a análise arquitetural de um acervo privado anterior com 32 fichas neuro/cognitivas. O conteúdo original não é reproduzido: a leitura propõe estudar essas fichas como **Lentes Cognitivas componíveis**, não como 32 primitivas rígidas do Core.

`19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md` formaliza o significado arquitetural do **360**: Core no centro, órbita extensível de lentes, agentes, guards, challengers, evaluators e policies, com ativação seletiva, orçamento e critérios de parada. Também registra a pista histórica de uma hierarquia 32 → 12 → 8 sem inventar o mapeamento ausente no recorte disponível.

## Foco vigente

O foco atual é o **Eva Engine® como infraestrutura cognitiva generalista e potencial motor empresarial**, não a experiência de um bloco de notas.

O projeto deve separar três tipos de escala:

- escala operacional;
- escala cognitiva;
- escala de domínio.

E deve investigar a engenharia em camadas:

```text
substrato determinístico
→ sinais
→ representação
→ contexto
→ recuperação
→ lentes
→ agentes especialistas
→ cruzamento
→ relações/inferência
→ challenger/contraprova
→ aprendizado
→ avaliação
→ orquestração
→ governança
```

As próximas frentes centrais são:

- Cognitive Kernel e invariantes universais;
- Evidence Model e separação entre score, evidência, inferência e confiança;
- Evaluation Plane e baselines;
- Cognitive Lens Registry / Lens Stacks e orquestração seletiva;
- arquitetura de agentes/guards determinísticos, heurísticos e opcionais por modelo;
- Challenger/Critic e mecanismos de contraprova;
- aprendizado contínuo supervisionado em múltiplos níveis;
- Capability Registry e Schema Registry;
- event log, lineage, rastreabilidade e versionamento cognitivo;
- dataset de referência e laboratório de testes;
- primeira implementação executável no Cursor sem estreitar a arquitetura;
- experimentos de escala sintética antes de qualquer alegação empresarial.

## Fase privada de P&D

Na fase atual, documentação, datasets, intenção experimental e resultados permanecem privados no repositório autorizado salvo decisão explícita de divulgação. Protótipos de produto não precisam ser expostos para que o Core seja especificado.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas e versionadas.
