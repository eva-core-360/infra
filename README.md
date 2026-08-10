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
8. `docs/blueprint/20_EXPLOSAO_ATOMICA_RECURSIVA_E_ESCALONAMENTO_DE_IA.md`
9. `docs/blueprint/21_QUARENTENA_COGNITIVA_PROMOCAO_E_RECUPERACAO.md`
10. `AGENTS.md`

Depois, consultar os documentos específicos da área em que irá trabalhar.

## Princípio central

> Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.

Protótipos anteriores são laboratórios e evidência; **não definem o teto conceitual do Core**.

## Princípios de escala e evidência

> **Nascer pequeno na implementação não significa nascer pequeno na arquitetura.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**

O Eva Engine® deve crescer por composição: schemas, registries, Domain Packs, capabilities, providers, lentes, agentes, relações e mecanismos de aprendizagem devem ampliar o sistema sem exigir reconstrução do núcleo.

O projeto distingue ideia, prova de mecanismo, bateria reproduzível, escala sintética, piloto de domínio, prova operacional e prova econômica.

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
        ├── 19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md
        ├── 20_EXPLOSAO_ATOMICA_RECURSIVA_E_ESCALONAMENTO_DE_IA.md
        └── 21_QUARENTENA_COGNITIVA_PROMOCAO_E_RECUPERACAO.md
```

## Evidência e conceitos preservados

- `16_...` registra achados de uma bateria anterior com 508 cenários como **evidência histórica**, não como arquitetura-alvo.
- `18_...` propõe as fichas cognitivas privadas como **Lentes Cognitivas componíveis**.
- `19_...` formaliza o **360** como Core central cercado por órbita extensível de lentes, agentes, guards, challengers, evaluators e policies.
- `20_...` formaliza a **Explosão Atômica Recursiva em ondas** e o escalonamento progressivo de mecânica para IA supervisora.
- `21_...` cria o **Learning Quarantine Plane**: candidatos de aprendizagem e derivados experimentais ficam fora do Trusted Core; só atravessam por Promotion Gate após avaliação, versionamento e possibilidade de recuperação/rollback.

## Foco vigente

O foco atual é o **Eva Engine® como infraestrutura cognitiva generalista e potencial motor empresarial**, não a experiência de um produto específico.

A engenharia deve distinguir:

- escala operacional;
- escala cognitiva;
- escala de domínio.

Fluxo conceitual em evolução:

```text
substrato determinístico
→ sinais
→ representação
→ contexto
→ recuperação
→ lentes
→ especialistas
→ cruzamento
→ inferência
→ challenger
→ avaliação
→ policy
→ resultado
→ derivados cognitivos
→ nova onda
→ candidatos de aprendizagem
→ Learning Quarantine
→ Promotion Gate
→ nova versão promovida do Trusted Core
```

Próximas frentes centrais:

- Cognitive Kernel e invariantes universais;
- Evidence Model;
- Evaluation Plane e baselines;
- Cognitive Lens Registry / Lens Stacks;
- agentes/guards determinísticos, heurísticos e opcionais por modelo;
- Challenger/Critic;
- `Cognitive Derivative`, `Learning Candidate` e `Wave`;
- métricas de novidade, ganho de informação e valor marginal;
- Supervisory AI Plane e critérios de escalonamento;
- Learning Quarantine, Promotion Gate, Shadow Mode e Recovery Protocol;
- Capability Registry e Schema Registry;
- lineage, blast radius, rastreabilidade e versionamento cognitivo;
- datasets, red team, testes de escala e pilotos de domínio.

## Fase privada de P&D

Na fase atual, documentação, datasets, intenção experimental e resultados permanecem privados no repositório autorizado salvo decisão explícita de divulgação.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas, avaliadas e versionadas.
