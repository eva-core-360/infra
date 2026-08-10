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
10. `docs/blueprint/22_ORGANISMO_COGNITIVO_INTEGRIDADE_E_RESILIENCIA.md`
11. `docs/blueprint/23_POSICIONAMENTO_B2B_DORES_E_TESE_DE_VALOR.md`
12. `AGENTS.md`

Depois, consultar os documentos específicos da área em que irá trabalhar.

## Princípio central

> Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.

Protótipos anteriores são laboratórios e evidência; **não definem o teto conceitual do Core**.

## Princípios de escala e evidência

> **Nascer pequeno na implementação não significa nascer pequeno na arquitetura.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**

O Eva Engine® deve crescer por composição: schemas, registries, Domain Packs, capabilities, providers, lentes, agentes, relações e mecanismos de aprendizagem devem ampliar o sistema sem exigir reconstrução do núcleo.

O projeto distingue ideia, prova de mecanismo, bateria reproduzível, escala sintética, piloto de domínio, prova operacional e prova econômica.

## Horizonte B2B enterprise

O Blueprint usa **B2B enterprise** como barra de engenharia desde o início. O objetivo é investigar problemas corporativos em que empresas gastam muito para pensar, correlacionar, investigar e coordenar usando combinações de:

```text
LLMs
+
agentes
+
consultorias
+
analistas
+
processamento
+
retrabalho
+
investigação manual
+
infraestrutura
```

A tese não é eliminar IA. É decompor o trabalho e resolver cada camada com o mecanismo de menor custo e maior previsibilidade que satisfaça o requisito, escalando para IA potente ou humano quando isso produzir ganho mensurável.

Nenhuma alegação externa de economia, escala ou ROI será feita antes da evidência correspondente.

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
        ├── 21_QUARENTENA_COGNITIVA_PROMOCAO_E_RECUPERACAO.md
        ├── 22_ORGANISMO_COGNITIVO_INTEGRIDADE_E_RESILIENCIA.md
        └── 23_POSICIONAMENTO_B2B_DORES_E_TESE_DE_VALOR.md
```

## Evidência e conceitos preservados

- `16_...` registra achados de uma bateria anterior com 508 cenários como **evidência histórica**, não como arquitetura-alvo.
- `18_...` propõe as fichas cognitivas privadas como **Lentes Cognitivas componíveis**.
- `19_...` formaliza o **360** como Core central cercado por órbita extensível de lentes, agentes, guards, challengers, evaluators e policies.
- `20_...` formaliza a **Explosão Atômica Recursiva em ondas** e o escalonamento progressivo de mecânica para IA supervisora.
- `21_...` cria o **Learning Quarantine Plane**: candidatos de aprendizagem e derivados experimentais ficam fora do Trusted Core; só atravessam por Promotion Gate após avaliação, versionamento e possibilidade de recuperação/rollback.
- `22_...` formaliza o motor como **organismo cognitivo de responsabilidades especializadas**, com Atomic Envelope, Integrity & Resilience Plane, health, watchdogs, quarantine, recuperação e detecção de peças ausentes/degradadas.
- `23_...` registra o foco **B2B enterprise**, a pilha de dores corporativas e a tese econômica de IA seletiva, auditável e proporcional ao valor produzido.

## Foco vigente

O foco atual é o **Eva Engine® como infraestrutura cognitiva generalista e potencial motor empresarial**, não a experiência de um produto específico.

A engenharia deve distinguir:

- escala operacional;
- escala cognitiva;
- escala de domínio;
- integridade e resiliência;
- custo e prova econômica.

Fluxo conceitual em evolução:

```text
EVENT / INPUT
   ↓
Atomic Envelope
   ↓
Ingress Guards
   ↓
Trusted Cognitive Fabric
   ↓
Context · Lenses · Specialists
   ↓
Crossing · Inference
   ↓
Challenger · Evaluator · Policy
   ↓
Result
   ├──────────────► consumer
   └──────────────► cognitive derivatives
                         ↓
                     new wave
                         ↓
                 learning candidates
                         ↓
                 Learning Quarantine
                         ↓
                   Promotion Gate
                         ↓
               promoted/versioned state

Integrity & Resilience Plane observes the whole path
and can isolate, degrade, alert, recover or escalate.
```

Próximas frentes centrais:

- Cognitive Kernel e invariantes universais;
- Atomic/Cognitive Envelope final;
- Evidence Model;
- Evaluation Plane e baselines;
- Integrity & Resilience Plane;
- Cognitive Lens Registry / Lens Stacks;
- agentes/guards determinísticos, heurísticos e opcionais por modelo;
- Challenger/Critic;
- `Cognitive Derivative`, `Learning Candidate` e `Wave`;
- métricas de novidade, ganho de informação e valor marginal;
- Supervisory AI Plane e critérios de escalonamento;
- Learning Quarantine, Promotion Gate, Shadow Mode e Recovery Protocol;
- Capability Registry, Health Registry e Schema Registry;
- lineage, taint propagation, blast radius e versionamento cognitivo;
- observabilidade, cost-per-event e AI escalation rate;
- datasets, red team, fault injection, testes de escala e pilotos enterprise;
- seleção do primeiro problema B2B E4 com baseline operacional e econômico.

## Fase privada de P&D

Na fase atual, documentação, datasets, intenção experimental e resultados permanecem privados no repositório autorizado salvo decisão explícita de divulgação.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas, avaliadas e versionadas.
