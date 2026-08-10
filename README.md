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
        └── 14_DOMAIN_PACK_MEMORY.md
```

## Situação atual

A fundação conceitual já está registrada. O próximo passo é aprofundar a Ontologia v0, gerar o primeiro dataset de casos e então criar a estrutura executável do `eva-engine` no Cursor.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas e versionadas.
