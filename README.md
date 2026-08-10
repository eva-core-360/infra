# Eva Engine® — Infra & Blueprint

Este repositório é a fonte de verdade arquitetural do **Eva Engine®**, núcleo cognitivo generalista que dará origem ao **Eva Memory®** e, futuramente, poderá servir como motor para outros produtos digitais.

## Regra de continuidade

Antes de propor arquitetura, código ou decisões estruturais, qualquer pessoa ou agente deve ler, nesta ordem:

1. `docs/blueprint/00_BLUEPRINT_MESTRE.md`
2. `docs/blueprint/01_REGISTRO_DECISOES.md`
3. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
4. `docs/blueprint/15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`
5. `AGENTS.md`

Depois, consultar os documentos específicos da área em que irá trabalhar.

## Princípio central

> Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.

O Eva Memory® será o primeiro produto consumidor e laboratório real do motor, mas o Core deve nascer generalista.

## Princípio de escala

> **Nascer pequeno na implementação não significa nascer pequeno na arquitetura.**

O Eva Engine® deve crescer por composição: novos idiomas, schemas, Domain Packs, capabilities, providers, relações e mecanismos de aprendizagem devem ampliar o sistema sem exigir reconstrução do núcleo.

Aprendizado contínuo é desejado, porém sua promoção deve ser supervisionada, versionada, mensurável e reversível.

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
        └── 16_LICOES_DO_LABORATORIO_INTELIGENCIA_LOCAL.md
```

## Evidência experimental preservada

`16_LICOES_DO_LABORATORIO_INTELIGENCIA_LOCAL.md` registra achados de uma bateria anterior com 508 cenários sobre mecanismos locais do produto de anotações. O documento é tratado como **evidência histórica**, não como arquitetura-alvo: reaproveitamos método, métricas e falhas observadas sem transportar automaticamente limitações do protótipo para o novo Core.

## Situação atual

A fundação conceitual e a direção de escala já estão registradas. O foco vigente é aprofundar o **Eva Engine® como infraestrutura cognitiva generalista**, antes de voltar a discutir experiência de usuário ou particularidades do produto de notas.

As próximas frentes centrais são:

- Cognitive Kernel e invariantes universais;
- ontologia universal extensível;
- hierarquia interna sem profundidade rígida;
- aprendizado contínuo supervisionado em múltiplos níveis;
- evaluators e promotion pipeline;
- Capability Registry e Schema Registry;
- event log, rastreabilidade e versionamento cognitivo;
- dataset de referência e laboratório de testes;
- primeira implementação executável no Cursor sem estreitar a arquitetura.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas e versionadas.
