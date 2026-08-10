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
10. `docs/blueprint/32_OBSERVABILITY_COGNITIVE_ECONOMICS_V0_1.md`
11. `docs/blueprint/33_LEARNING_QUARANTINE_PROMOTION_UNLEARNING_V1_0.md`
12. `docs/blueprint/34_ENTERPRISE_INTEGRATION_BOUNDARY_V0_1.md`
13. `docs/blueprint/35_ENTERPRISE_COGNITIVE_THREAT_MODEL_V0_1.md`
14. `docs/blueprint/36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md`
15. `docs/blueprint/01_REGISTRO_DECISOES.md`
16. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
17. `docs/blueprint/15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`
18. `docs/blueprint/17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md`
19. `docs/blueprint/18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md`
20. `docs/blueprint/19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md`
21. `docs/blueprint/20_EXPLOSAO_ATOMICA_RECURSIVA_E_ESCALONAMENTO_DE_IA.md`
22. `docs/blueprint/21_QUARENTENA_COGNITIVA_PROMOCAO_E_RECUPERACAO.md`
23. `docs/blueprint/22_ORGANISMO_COGNITIVO_INTEGRIDADE_E_RESILIENCIA.md`
24. `docs/blueprint/23_POSICIONAMENTO_B2B_DORES_E_TESE_DE_VALOR.md`
25. `AGENTS.md`

Depois, consultar os documentos especializados da área em que irá trabalhar.

O `00_BLUEPRINT_MESTRE.md` preserva a fundação inicial. O `24_MAPA_MESTRE_ARQUITETURA_ENTERPRISE_V0_2.md` é a fotografia consolidada da arquitetura enterprise. Os documentos `25` a `36` formalizam núcleo, evidência, registries, orquestração, circulação, resiliência, avaliação, economia cognitiva, aprendizagem isolada, integração enterprise, threat model e primeiro heartbeat executável.

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

> **O motor precisa saber quanto custou pensar e se o ganho justificou o trabalho.**

> **Aprender é propor mudança; promover é conceder autoridade.**

> **A empresa não entra no Core; atravessa uma membrana que traduz, limita, autentica e deixa rastro.**

> **O primeiro coração não precisa pensar muito. Precisa bater certo.**

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
ENTERPRISE INTEGRATION BOUNDARY
adapter · auth · tenant · scope · schema · provenance · idempotency
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
                             Evaluation + Promotion Gate
                                         │
                                         ▼
                              promoted/versioned state

Integrity & Resilience observa o caminho inteiro.
Evaluation Plane compara capability, composição e sistema contra baselines.
Observability & Cognitive Economics mede comportamento, custo, escalonamento e valor marginal.
Threat Model cobre dados, evidence, learning, scope, promotion, agents e cost attacks.
Supervisory AI / Human Authority entra por escalonamento quando justificado.
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
        ├── 31_EVALUATION_PLANE_V0_1.md
        ├── 32_OBSERVABILITY_COGNITIVE_ECONOMICS_V0_1.md
        ├── 33_LEARNING_QUARANTINE_PROMOTION_UNLEARNING_V1_0.md
        ├── 34_ENTERPRISE_INTEGRATION_BOUNDARY_V0_1.md
        ├── 35_ENTERPRISE_COGNITIVE_THREAT_MODEL_V0_1.md
        └── 36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md
```

---

## Páginas estruturais recentes

- `16_...` — evidência histórica de uma bateria anterior com 508 cenários.
- `18_...` — Lentes Cognitivas componíveis.
- `19_...` — arquitetura 360 orbital e hierarquia de agentes/guards.
- `20_...` — Explosão Atômica Recursiva em ondas e escalonamento seletivo de IA.
- `21_...` — fundação histórica do segundo círculo: Learning Quarantine, Promotion Gate e recuperação.
- `22_...` — organismo cognitivo, Atomic Envelope, integridade e resiliência.
- `23_...` — foco B2B enterprise, dores e tese econômica.
- `24_...` — Mapa Mestre Enterprise v0.2.
- `25_...` — Cognitive Kernel v0.1.
- `26_...` — Evidence Model v0.1.
- `27_...` — Schema, Capability e Health Registries.
- `28_...` — Orchestration Model v0.1.
- `29_...` — Atomic/Cognitive Envelope v1.0.
- `30_...` — Integrity & Resilience Plane v0.1.
- `31_...` — Evaluation Plane v0.1.
- `32_...` — Observability & Cognitive Economics v0.1.
- `33_...` — Learning Quarantine, Promotion & Controlled Unlearning v1.0; consolida isolamento, manifests, checkpoints, replay e revogação de influência aprendida.
- `34_...` — Enterprise Integration Boundary v0.1; adapters, Anti-Corruption Layer, tenant/scope, ingest/egress, replay/backfill, idempotência e Integration Health.
- `35_...` — Enterprise Cognitive Threat Model v0.1; protege código, dados, evidence, learning, promotion, scope, agents, orchestration, evaluation e custo.
- `36_...` — Executable Architecture Spec v0.1; define o primeiro heartbeat executável e a ordem de implementação no Cursor.

---

## Foco vigente

O Blueprint arquitetural já possui base suficiente para iniciar o primeiro heartbeat executável sem abandonar as frentes de pesquisa de longo prazo.

Próxima sequência:

```text
Executable Architecture Spec v0.1
        ↓
criar repositório/runtime executável privado
        ↓
Cursor — STEP 1
contracts + schemas + envelope
        ↓
STEP 2
registries + policy + budget
        ↓
STEP 3
orchestrator + deterministic capability + trace
        ↓
STEP 4
integrity + API + persistence adapter
        ↓
CI + fault injection + benchmark
        ↓
Heartbeat v0.1
        ↓
capabilities cognitivas progressivamente mais sofisticadas
        ↓
primeiro piloto B2B E4 após evidência suficiente
```

Questão imediata ainda aberta: confirmar se o runtime executável viverá em repositório privado separado (preferência arquitetural atual: `eva-core-360/engine` ou equivalente) ou no próprio `infra`.

O projeto permanece em fase privada de P&D. Documentação, datasets, intenção experimental e resultados permanecem no repositório/contextos autorizados salvo decisão explícita de divulgação.

O Blueprint é vivo: decisões podem evoluir, mas mudanças estruturais devem ser registradas, avaliadas e versionadas.
