# Eva Engine® — Infra & Blueprint

Este repositório é a fonte de verdade arquitetural do **Eva Engine®**, núcleo cognitivo generalista que dará origem ao **Eva Memory®** e, futuramente, poderá servir como motor para outros produtos digitais.

## Regra de continuidade

Antes de propor arquitetura, código ou decisões estruturais, qualquer pessoa ou agente deve ler, nesta ordem:

1. `docs/blueprint/00_BLUEPRINT_MESTRE.md`
2. `docs/blueprint/01_REGISTRO_DECISOES.md`
3. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
4. `AGENTS.md`

Depois, consultar os documentos específicos da área em que irá trabalhar.

## Princípio central

> Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.

O Eva Memory® será o primeiro produto consumidor e laboratório real do motor, mas o Core deve nascer generalista.

## Estrutura inicial

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
        └── 05_EVENTOS_V0.md
```

Esta estrutura será expandida conforme o Blueprint amadurecer.
