# EVA ENGINE® — MAPA MESTRE DE ARQUITETURA ENTERPRISE v0.2

**Status:** fotografia arquitetural vigente, em evolução  
**Função:** consolidar em uma única página o salto arquitetural produzido após o Blueprint Mestre v0.1. Este documento não substitui as páginas especializadas; ele serve como mapa de navegação e estado atual do sistema.

---

# 1. Definição atual

O Eva Engine® é projetado como uma **infraestrutura cognitiva generalista B2B enterprise**, orientada a eventos, capaz de decompor problemas complexos em mecanismos determinísticos, heurísticos, estatísticos, especialistas, agentes e IA supervisora, escolhidos conforme custo, risco, evidência e contexto.

Não é:

- um bloco de notas;
- um chatbot;
- um wrapper de LLM;
- um único agente;
- uma base de dados com automações;
- um sistema que aprende diretamente em produção sem isolamento.

É um **Cognitive Runtime / Cognitive Fabric** com execução confiável, aprendizagem controlada, avaliação, orquestração, resiliência e governança.

---

# 2. Mapa arquitetural completo

```text
                               ┌───────────────────────────────────────────────┐
                               │           ENTERPRISE ENVIRONMENT              │
                               │                                               │
                               │ ERP · CRM · logs · support · finance · APIs   │
                               │ docs · sensors · agents · humans · systems    │
                               └──────────────────────┬────────────────────────┘
                                                      │
                                                      ▼
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                              BOUNDARY / INGESTION PLANE                                 │
│                                                                                         │
│ schema · auth · provenance · tenant scope · validation · dedup · security · normalization│
└─────────────────────────────────────────────┬───────────────────────────────────────────┘
                                              │
                                              ▼
                                    ┌───────────────────┐
                                    │  ATOMIC ENVELOPE  │
                                    │ id · lineage      │
                                    │ trust · scope     │
                                    │ risk · policy     │
                                    └─────────┬─────────┘
                                              │
                                              ▼
╔═════════════════════════════════════════════════════════════════════════════════════════╗
║                           TRUSTED COGNITIVE FABRIC                                      ║
║                                                                                         ║
║    ┌───────────────┐      ┌────────────────┐      ┌────────────────────────┐            ║
║    │ ORCHESTRATOR  │─────►│ CONTEXT ENGINE │─────►│ COGNITIVE LENS ROUTER  │            ║
║    └───────┬───────┘      └────────────────┘      └────────────┬───────────┘            ║
║            │                                                  │                        ║
║            │                         ┌────────────────────────┼────────────────────┐    ║
║            │                         ▼                        ▼                    ▼    ║
║            │                    SPECIALIST A             SPECIALIST B        SPECIALIST C║
║            │                    deterministic            statistical        model/local ║
║            │                         │                        │                    │    ║
║            │                         └──────────────┬─────────┴──────────────┬─────┘    ║
║            │                                        ▼                        │          ║
║            │                                    CROSSING                     │          ║
║            │                                        │                        │          ║
║            │                         ┌──────────────┼──────────────┐         │          ║
║            │                         ▼              ▼              ▼         │          ║
║            │                       ATOMS         RELATIONS       SIGNALS      │          ║
║            │                         └──────────────┼──────────────┘         │          ║
║            │                                        ▼                        │          ║
║            │                                    INFERENCE                    │          ║
║            │                                        │                        │          ║
║            │                         ┌──────────────┴──────────────┐         │          ║
║            │                         ▼                             ▼         │          ║
║            │                    CHALLENGER                     EVIDENCE       │          ║
║            │                         │                             │         │          ║
║            │                         └──────────────┬──────────────┘         │          ║
║            │                                        ▼                        │          ║
║            │                                    EVALUATOR                    │          ║
║            │                                        │                        │          ║
║            │                                        ▼                        │          ║
║            │                                      POLICY                     │          ║
║            │                                        │                        │          ║
║            │                     ┌──────────────────┴──────────────────┐     │          ║
║            │                     ▼                                     ▼     │          ║
║            │                  RESULT                            COGNITIVE DERIVATIVES    ║
║            │                     │                                     │                ║
║            │                     │                                     ▼                ║
║            │                     │                                  NEW WAVE            ║
║            │                     │                                     │                ║
║            └─────────────────────┴─────────────────────────────────────┘                ║
║                                    bounded recursion                                    ║
╚═════════════════════════════════════════════════════════════════════════════════════════╝
                                              │
                        ┌─────────────────────┼──────────────────────┐
                        │                     │                      │
                        ▼                     ▼                      ▼
              ┌─────────────────┐  ┌──────────────────────┐  ┌─────────────────────┐
              │ CONSUMER/OUTPUT │  │ LEARNING CANDIDATES  │  │ ESCALATION REQUEST  │
              └─────────────────┘  └──────────┬───────────┘  └──────────┬──────────┘
                                              │                         │
                                              ▼                         ▼
                               ╔════════════════════════╗    ┌─────────────────────┐
                               ║ LEARNING QUARANTINE    ║    │ SUPERVISORY AI      │
                               ║                        ║    │ / HUMAN AUTHORITY   │
                               ║ rules · weights       ║    │ only when justified│
                               ║ relations · routing   ║    └─────────────────────┘
                               ║ lens stacks · models  ║
                               ╚───────────┬────────────╝
                                           │
                                           ▼
                                  ┌──────────────────┐
                                  │ PROMOTION GATE   │
                                  │ eval · holdout   │
                                  │ red team · shadow│
                                  │ canary · approval│
                                  └─────────┬────────┘
                                            │
                                            ▼
                                  PROMOTED VERSIONED STATE
```

---

# 3. Planos transversais

Os blocos abaixo não pertencem a uma única etapa. Eles observam ou limitam o sistema inteiro.

```text
┌──────────────────────────────────────────────────────────────────────┐
│ INTEGRITY & RESILIENCE PLANE                                       │
│ anomaly · drift · poisoning · health · watchdog · circuit breaker  │
│ isolation · rollback · reprocessing · blast radius · recovery      │
└──────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────┐
│ OBSERVABILITY & ECONOMICS PLANE                                     │
│ traces · lineage · latency · cost/event · AI escalation · failures  │
│ correction rate · quality · throughput · ROI inputs                 │
└──────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────┐
│ GOVERNANCE & POLICY PLANE                                           │
│ privacy · authorization · tenant isolation · risk · compliance      │
│ retention · promotion policy · human authority · audit              │
└──────────────────────────────────────────────────────────────────────┘
```

---

# 4. Princípio do organismo

O Eva Engine® deve ser pensado como um organismo de **responsabilidades especializadas**.

```text
Core        = núcleo estável
Capabilities= células funcionais
Guards      = membranas/defesas
Events      = circulação
Envelope    = identidade de cada unidade circulante
Integrity   = sistema de defesa e recuperação
Watchdogs   = supervisão de saúde
Quarantine  = área de aprendizado isolada
Promotion   = processo de aceitação de mudança
```

Essa é uma metáfora de engenharia, não uma alegação biológica.

---

# 5. Explosão Atômica

A atomização não termina na primeira fragmentação.

```text
EVENT
  ↓
ATOMS
  ↓
RELATIONS
  ↓
DERIVATIVES
  ↓
NEW METADATA
  ↓
NEW WAVE
  ↓
NEW ATOMS / RELATIONS / HYPOTHESES
  ↓
...
```

A recursão só continua enquanto existir valor marginal suficiente.

Critérios conceituais:

```text
novelty >= floor
information_gain >= floor
confidence >= floor
risk <= budget
cost <= budget
latency <= budget
depth <= max_depth
privacy_scope = allowed
```

---

# 6. Lentes cognitivas

As 32 fichas cognitivas históricas não são tratadas como primitivas rígidas do Core.

Elas inspiram um **Cognitive Lens Registry**: perspectivas que ajudam o motor a decidir **como observar** determinado fenômeno.

```text
ATOM       = o que foi representado
LENS       = de qual perspectiva observar
CAPABILITY = o que o motor sabe fazer
AGENT      = uma forma possível de executar
ORCHESTRATOR = quem decide quando e em qual ordem
```

Lentes podem crescer sem aumentar proporcionalmente o núcleo.

---

# 7. Escalonamento de inteligência

A direção econômica é usar a menor camada que resolva o problema com qualidade suficiente.

```text
L0  deterministic mechanics
 ↓
L1  heuristic / statistical
 ↓
L2  specialized algorithms / local models
 ↓
L3  agent ensembles / challengers / validators
 ↓
L4  supervisory AI / high-capability models
 ↓
L5  human authority
```

A subida de nível depende de risco, ambiguidade, valor, custo e insuficiência das camadas anteriores.

---

# 8. Aprendizado em dois círculos

```text
CIRCLE 1 — TRUSTED EXECUTION
production rules · promoted schemas · validated capabilities

CIRCLE 2 — LEARNING QUARANTINE
candidates · experiments · new weights · new routes · new hypotheses
```

Regra absoluta vigente:

> **O Learning Quarantine pode observar o sistema autorizado, mas não possui caminho de escrita direta para o Trusted Core.**

A passagem ocorre apenas por Promotion Gate.

---

# 9. Correção e recuperação

O motor é projetado assumindo que algum erro poderá atravessar validações.

```text
ERROR DISCOVERED
  ↓
TRACE ORIGIN
  ↓
REVOKE / SUPERSEDE
  ↓
TRACE DESCENDANTS
  ↓
BLAST RADIUS
  ↓
MARK STALE / TAINTED / INVALID
  ↓
REPROCESS
  ↓
VERIFY
```

Objetivo: corrigir a árvore contaminada sem apagar a história necessária para auditoria.

---

# 10. Tese B2B enterprise

Problema econômico de referência:

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

O Eva Engine® investiga quanto dessa pilha pode ser reduzida, coordenada ou elevada por:

- mecânica determinística;
- contexto persistente;
- memória reutilizável;
- especialistas baratos;
- agentes governados;
- IA seletiva;
- investigação assistida;
- auditabilidade;
- aprendizado controlado.

A tese de valor é **mensurável**, não retórica.

---

# 11. O que deve ser medido em enterprise

```text
quality
latency
throughput
cost_per_event
cost_per_resolved_case
AI_escalation_rate
human_escalation_rate
correction_rate
false_positive_rate
false_negative_rate
quarantine_rate
rollback_rate
time_to_context
time_to_resolution
investigation_hours_saved
rework_rate
ROI inputs
```

Cada domínio selecionará o subconjunto relevante.

---

# 12. Escada de evidência

```text
E0 — ideia
E1 — prova de mecanismo
E2 — bateria reproduzível
E3 — escala sintética
E4 — piloto de domínio real
E5 — prova operacional
E6 — prova econômica
```

A arquitetura pode mirar E6 enquanto uma capability específica ainda está em E1/E2.

---

# 13. Principais invariantes atuais

1. Original preservado.
2. RAW ≠ DERIVED ≠ INFERRED ≠ LEARNED.
3. Produtos dependem do Core; Core não depende de produtos.
4. Evento é abstração universal de entrada atual.
5. Inferência possui evidência/rastreabilidade proporcional ao risco.
6. Explosão Atômica é recursiva, mas limitada.
7. Aprendizado candidato nasce fora do Trusted Core.
8. Promotion Gate é a única passagem de aprendizado para estado promovido.
9. Derivados preservam lineage suficiente para correção.
10. Integrity & Resilience pode isolar e degradar, mas não reescrever silenciosamente conhecimento global.
11. IA é uma camada da arquitetura, não a arquitetura inteira.
12. B2B enterprise é a barra de engenharia vigente.
13. ROI e economia só são afirmados com evidência operacional/econômica.
14. Implementação pequena não autoriza arquitetura estreita.
15. Responsabilidade lógica não implica microserviço físico.

---

# 14. Próxima sequência de especificação

A partir deste mapa, as próximas páginas devem aprofundar, nesta ordem aproximada:

```text
Cognitive Kernel
    ↓
Atomic/Cognitive Envelope
    ↓
Evidence Model
    ↓
Capability + Health Registry
    ↓
Orchestrator / Routing Model
    ↓
Integrity & Resilience Protocols
    ↓
Learning Quarantine / Promotion Protocol
    ↓
Evaluation Plane
    ↓
Observability + Economics
    ↓
Enterprise Integration / Multi-tenant
    ↓
Threat Model / Adversarial Testing
    ↓
Pilot Selection Framework
```

A ordem pode mudar quando uma dependência técnica justificar.

---

# 15. Norte

> **O Eva Engine® pretende transformar uma grande quantidade de trabalho cognitivo corporativo em uma engrenagem controlada de mecanismos especializados: cada dado entra identificado, cada capacidade atua onde deve, cada inferência pode ser desafiada, cada aprendizado nasce em quarentena, cada falha pode ser rastreada e a IA mais cara só é chamada quando sua presença compra valor real.**
