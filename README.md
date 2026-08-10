# Eva Engine® — Infra & Blueprint

Este repositório é a fonte privada de verdade arquitetural do **Eva Engine®**, uma infraestrutura cognitiva generalista projetada com horizonte **B2B enterprise**.

O projeto não é um bloco de notas, um chatbot ou um wrapper de LLM. Protótipos anteriores são laboratórios e evidência experimental; não definem o teto conceitual do Core.

---

## Regra de continuidade

Antes de propor arquitetura, código ou decisões estruturais, qualquer novo chat, agente ou desenvolvedor deve ler, nesta ordem:

1. `docs/blueprint/00_BLUEPRINT_MESTRE.md`
2. `docs/blueprint/24_MAPA_MESTRE_ARQUITETURA_ENTERPRISE_V0_2.md`
3. `docs/blueprint/25_COGNITIVE_KERNEL_V0_1.md`
4. `docs/blueprint/26_EVIDENCE_MODEL_V0_1.md`
5. `docs/blueprint/27_CAPABILITY_HEALTH_SCHEMA_REGISTRIES_V0_1.md`
6. `docs/blueprint/28_ORCHESTRATION_MODEL_V0_1.md`
7. `docs/blueprint/29_ATOMIC_COGNITIVE_ENVELOPE_V1_0.md`
8. `docs/blueprint/30_INTEGRITY_RESILIENCE_PLANE_V0_1.md`
9. `docs/blueprint/31_EVALUATION_PLANE_V0_1.md`
10. `docs/blueprint/01_REGISTRO_DECISOES.md`
11. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
12. `docs/blueprint/15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`
13. `docs/blueprint/17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md`
14. `docs/blueprint/18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md`
15. `docs/blueprint/19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md`
16. `docs/blueprint/20_EXPLOSAO_ATOMICA_RECURSIVA_E_ESCALONAMENTO_DE_IA.md`
17. `docs/blueprint/21_QUARENTENA_COGNITIVA_PROMOCAO_E_RECUPERACAO.md`
18. `docs/blueprint/22_ORGANISMO_COGNITIVO_INTEGRIDADE_E_RESILIENCIA.md`
19. `docs/blueprint/23_POSICIONAMENTO_B2B_DORES_E_TESE_DE_VALOR.md`
20. `AGENTS.md`

Depois, consultar os documentos especializados da área em que irá trabalhar.

O `00_BLUEPRINT_MESTRE.md` preserva a fundação inicial. O `24_MAPA_MESTRE_ARQUITETURA_ENTERPRISE_V0_2.md` é a fotografia consolidada da arquitetura enterprise. Os documentos `25` a `31` formalizam o núcleo irredutível, o modelo de evidência, registries, orquestração, envelope cognitivo, integridade/resiliência e avaliação.

---

## Princípios centrais

> **Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.**

> **Nascer pequeno na implementação não significa nascer pequeno na arquitetura.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**

> **Aprendizado nasce em quarentena; confiança é conquistada por promoção.**

> **O Kernel deve permanecer menor que o ecossistema que ele governa.**

> **Score não é Confidence; repetição não cria evidência independente.**

> **A capability pode pedir para continuar; o Orchestrator decide se o organismo continua.**

> **Inteligência pode se fragmentar; identidade, origem e responsabilidade não podem se perder.**

> **Uma versão só melhora quando supera o baseline sem violar hard gates de segurança, privacidade, custo e integridade.**

---

## Horizonte B2B enterprise

O Blueprint usa B2B enterprise como barra de engenharia desde o início. O objetivo é investigar problemas corporativos em que organizações gastam muito para pensar, correlacionar, investigar, coordenar e operar usando combinações de:

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

Nenhuma alegação externa de economia, escala, superioridade ou ROI será feita antes da evidência correspondente.

---

## Mapa arquitetural resumido

```text
ENTERPRISE ENVIRONMENT
ERP · CRM · logs · docs · finance · support · APIs · sensors · humans
          │
          ▼
BOUNDARY / INGESTION
schema · auth · scope · provenance · validation · normalization
          │
          ▼
ATOMIC / COGNITIVE ENVELOPE
identity · schema · root/correlation · scope · provenance
trust · integrity · policy · version · lineage · trace
          │
          ▼
╔════════════════════════════════════════════════════════════════════╗
║                    TRUSTED COGNITIVE FABRIC                      ║
║                                                                  ║
║  Cognitive Kernel                                                ║
║       │                                                          ║
║       ▼                                                          ║
║  Orchestration Control Plane                                     ║
║  requirement · registry query · admission · plan · budget        ║
║       │                                                          ║
║       ▼                                                          ║
║  Schema Registry · Capability Registry · Health Registry         ║
║       │                                                          ║
║       ▼                                                          ║
║  Execution Plane                                                 ║
║  Context · Lenses · Specialists · Rules · Models · Agents        ║
║       │                                                          ║
║       ▼                                                          ║
║  Crossing → Signals → Evidence → Claim/Hypothesis                ║
║       │                                                          ║
║       ▼                                                          ║
║  Challenger → Counter-Evidence → Confidence/Uncertainty          ║
║       │                                                          ║
║       ▼                                                          ║
║  Policy → Result + Cognitive Derivatives                         ║
║                         │                                        ║
║                         ▼                                        ║
║                 NextStepCandidate                                ║
║                         │                                        ║
║                  Admission Control                               ║
║                         │                                        ║
║                    New Wave ↺                                    ║
╚════════════════════════════════════════════════════════════════════╝
          │                              │
          ▼                              ▼
      CONSUMER                   LEARNING CANDIDATES
                                         │
                                         ▼
                                LEARNING QUARANTINE
                                         │
                                   Promotion Gate
                                         │
                                         ▼
                              promoted/versioned state

Integrity & Resilience observa o caminho inteiro.
Evaluation Plane compara capability, composição e sistema contra baselines.
Supervisory AI / Human Authority entra por escalonamento quando justificado.
Observability & Economics mede qualidade, latência, custo e taxa de escalonamento.
```

---

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
        ├── 23_POSICIONAMENTO_B2B_DORES_E_TESE_DE_VALOR.md
        ├── 24_MAPA_MESTRE_ARQUITETURA_ENTERPRISE_V0_2.md
        ├── 25_COGNITIVE_KERNEL_V0_1.md
        ├── 26_EVIDENCE_MODEL_V0_1.md
        ├── 27_CAPABILITY_HEALTH_SCHEMA_REGISTRIES_V0_1.md
        ├── 28_ORCHESTRATION_MODEL_V0_1.md
        ├── 29_ATOMIC_COGNITIVE_ENVELOPE_V1_0.md
        ├── 30_INTEGRITY_RESILIENCE_PLANE_V0_1.md
        └── 31_EVALUATION_PLANE_V0_1.md
```

---

## Páginas estruturais recentes

- `16_...` — evidência histórica de uma bateria anterior com 508 cenários.
- `18_...` — Lentes Cognitivas componíveis.
- `19_...` — arquitetura 360 orbital e hierarquia de agentes/guards.
- `20_...` — Explosão Atômica Recursiva em ondas e escalonamento seletivo de IA.
- `21_...` — Learning Quarantine, Promotion Gate e recuperação de erro.
- `22_...` — organismo cognitivo, Atomic Envelope, integridade e resiliência.
- `23_...` — foco B2B enterprise, dores e tese econômica.
- `24_...` — Mapa Mestre Enterprise v0.2.
- `25_...` — Cognitive Kernel v0.1, contratos universais e teste de pureza.
- `26_...` — Evidence Model v0.1, independência, counter-evidence, causalidade e calibração.
- `27_...` — Schema, Capability e Health Registries; catálogo vivo, dependency/fallback graph e health técnico/cognitivo/econômico.
- `28_...` — Orchestration Model v0.1; Control/Execution Plane, Work Graph, budgets, Admission Control, fan-out, stop, backpressure, circuit breakers e escalonamento.
- `29_...` — Atomic/Cognitive Envelope v1.0; identidade, scope, provenance, root/correlation/causation, três eixos de estado, idempotência, temporalidade, privacy, version vector e overhead controlado.
- `30_...` — Integrity & Resilience Plane v0.1; fault classes, containment zones, taint propagation, blast radius, circuit breakers, safe modes, recovery, verification e fault injection.
- `31_...` — Evaluation Plane v0.1; baselines, golden/holdout, slices, scorecards, calibration, shadow/canary, ablation, economic evaluation e promotion gates.

---

## Foco vigente

As próximas frentes centrais são:

```text
Cognitive Kernel v0.1
        ↓
Evidence Model v0.1
        ↓
Capability + Health + Schema Registries v0.1
        ↓
Orchestration Model v0.1
        ↓
Atomic / Cognitive Envelope v1.0
        ↓
Integrity & Resilience v0.1
        ↓
Evaluation Plane v0.1
        ↓
Learning Quarantine / Promotion final
        ↓
Observability + Economics
        ↓
Enterprise Integration
        ↓
Threat Model / Fault Injection
        ↓
primeiro piloto B2B E4
```

O projeto permanece em fase privada de P&D. Documentação, datasets, intenção experimental e resultados permanecem no repositório/contextos autorizados salvo decisão explícita de divulgação.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas, avaliadas e versionadas.
