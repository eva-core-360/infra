# Eva Engine® — Organismo Cognitivo, Integridade e Resiliência

**Status:** base arquitetural vigente, em evolução  
**Função:** traduzir a metáfora do Eva Engine® como um grande organismo em responsabilidades técnicas reais: unidades especializadas, circulação de informação com metadados mínimos, detecção de anomalias, quarentena, supervisão, recuperação e aviso quando uma peça necessária falhar.

---

# 1. A metáfora do organismo

A imagem do organismo é útil porque descreve uma arquitetura em que **nenhuma peça precisa fazer tudo**.

O motor central permanece pequeno, estável e protegido. Ao redor dele, componentes especializados atuam somente quando seu tipo de sinal, risco ou contexto exige.

```text
                         EVA CORE 360®
                    ORGANISMO COGNITIVO

        ┌──────────────────────────────────────────────┐
        │        INTEGRITY & RESILIENCE PLANE          │
        │                                              │
        │  health · anomaly · drift · poisoning        │
        │  watchdog · quarantine · recovery · alert    │
        │                                              │
        │   ┌──────────────────────────────────────┐   │
        │   │       COGNITIVE FABRIC              │   │
        │   │                                      │   │
        │   │ guard  lens  specialist  challenger  │   │
        │   │   \     |       |          /         │   │
        │   │    \    |       |         /          │   │
        │   │        [ TRUSTED CORE ]               │   │
        │   │    /    |       |         \          │   │
        │   │ policy evaluator router  memory       │   │
        │   │                                      │   │
        │   └──────────────────────────────────────┘   │
        │                                              │
        └──────────────────────────────────────────────┘
```

A metáfora biológica **não é uma alegação científica sobre o funcionamento do cérebro ou de organismos vivos**. Ela serve como modelo mental para decomposição, especialização, defesa, circulação, homeostase e recuperação.

---

# 2. Tradução da metáfora para arquitetura

| Metáfora | Termo arquitetural preferido | Responsabilidade |
|---|---|---|
| organismo | Cognitive System / Cognitive Fabric | sistema completo coordenado |
| núcleo | Trusted Execution Core | execução do estado e regras promovidas |
| célula especializada | Guard / Specialist / Capability | função pequena e especializada |
| sistema imunológico | Integrity & Resilience Plane | detectar, conter, rastrear e recuperar |
| sangue/circulação | Event & Data Flow | transportar eventos e derivados |
| membrana | Boundary / Policy Gate | controlar entrada, saída e permissão |
| anticorpo | Detector / Validator / Challenger | identificar sinal de risco específico |
| febre/alerta | Health Signal / Alert | indicar degradação ou falha |
| cicatrização | Recovery / Reprocessing | restaurar estado válido |
| mutação | Learning Candidate | mudança candidata, nunca promoção automática |
| homeostase | Operational Stability | manter o sistema dentro de limites conhecidos |

---

# 3. O átomo não deve circular nu

**DECISÃO APROVADA COMO PRINCÍPIO**

Toda unidade cognitiva relevante deve carregar um **Atomic Envelope / Cognitive Envelope**: um conjunto mínimo de metadados que permita saber de onde veio, quem a produziu, qual sua confiabilidade, a que contexto pertence e como rastrear seus descendentes.

A ideia é simples:

> **Nenhum átomo entra ou sai do organismo sem identidade, origem e contexto operacional suficientes para ser auditado.**

Contrato conceitual inicial:

```text
AtomicEnvelope
├── atom_id
├── root_event_id
├── parent_derivation_id
├── tenant_id / scope_id
├── schema_id
├── schema_version
├── provenance
├── source_type
├── origin_module
├── origin_lens
├── origin_agent
├── engine_version
├── created_at
├── trust_tier
├── epistemic_level        # RAW / DERIVED / INFERRED / LEARNED
├── confidence             # quando aplicável e calibrado
├── evidence_refs[]
├── lineage_refs[]
├── privacy_class
├── risk_class
├── integrity_state
├── content_hash           # quando aplicável
└── policy_tags[]
```

Nem todo campo será obrigatório em todo tipo de objeto. O Schema Registry definirá o mínimo exigido por categoria.

---

# 4. Ciclo saudável de circulação

```text
INPUT
  │
  ▼
INGRESS GUARDS
  │
  ├── schema válido?
  ├── origem conhecida?
  ├── escopo permitido?
  ├── integridade preservada?
  └── risco detectado?
  │
  ▼
ATOMIC ENVELOPE
  │
  ▼
ROUTER / ORCHESTRATOR
  │
  ▼
SPECIALISTS / LENSES
  │
  ▼
CROSSING
  │
  ▼
CHALLENGER / EVALUATOR
  │
  ▼
POLICY
  │
  ├──────────────► OUTPUT
  │
  └──────────────► DERIVATIVES
                       │
                       ▼
                LEARNING QUARANTINE
```

O caminho normal deve ser previsível e observável. Componentes especializados podem ser paralelos, mas o lineage precisa permanecer reconstruível.

---

# 5. O “vírus” em termos reais

O termo “vírus” representa qualquer elemento capaz de degradar o comportamento do sistema se for aceito como válido.

Exemplos:

```text
schema inválido
input adversarial
conteúdo corrompido
duplicata enganosa
regra incompatível
sinal fora de distribuição
prompt injection em um componente que use LLM
knowledge poisoning
data poisoning
semantic drift
modelo degradado
agente com comportamento divergente
dependência quebrada
estado inconsistente
relação auto-confirmatória
feedback fraudulento ou anômalo
```

O organismo não deve reagir sempre apagando.

Para preservar auditoria, a resposta preferida é:

```text
DETECT
  ↓
ISOLATE
  ↓
QUARANTINE
  ↓
TRACE LINEAGE
  ↓
ASSESS BLAST RADIUS
  ↓
REVOKE / SUPERSEDE / MARK TAINTED
  ↓
REPROCESS
  ↓
VERIFY
```

**O original imutável não deve ser destruído apenas porque uma interpretação derivada foi considerada nociva ou incorreta.**

---

# 6. Integrity & Resilience Plane

O segundo grande componente do organismo será tratado como **Integrity & Resilience Plane**.

Responsabilidades possíveis:

- validação de integridade;
- detecção de comportamento anômalo;
- detecção de drift;
- detecção de poisoning;
- monitoramento de dependências;
- health checks;
- heartbeats de agentes/serviços;
- análise de erros em cascata;
- circuit breakers;
- rate limits;
- isolamento de componentes;
- rollback;
- reprocessamento;
- auditoria;
- alertas;
- ativação do Learning Quarantine Plane;
- escalonamento para supervisão humana ou IA quando necessário.

Esse plano deve possuir autoridade para **impedir propagação**, mas não para reescrever silenciosamente o conhecimento promovido.

---

# 7. Supervisores e ausência de peça

A visão exige que uma pequena peça ausente ou degradada não passe silenciosamente.

Isso sugere uma combinação de:

```text
Capability Registry
+
Dependency Graph
+
Health Registry
+
Watchdogs
+
Observability
+
Supervisory Orchestration
```

Cada capability relevante pode possuir estado operacional:

```text
HEALTHY
DEGRADED
UNAVAILABLE
QUARANTINED
DISABLED
UNKNOWN
```

Exemplo:

```text
EVENT
  ↓
Orchestrator calcula plano
  ↓
CAP_TEMPORAL necessária
  ↓
Health Registry = DEGRADED
  ↓
Fallback disponível?
  ├── SIM → usa fallback + registra degradação
  └── NÃO → reduz capacidade / escala / interrompe
```

Princípio:

> **Falha conhecida deve ser preferida a sucesso aparente com peça crítica ausente.**

---

# 8. Auto-recuperação controlada

O sistema pode possuir mecanismos de self-healing, mas apenas para operações cuja recuperação seja segura e testada.

Possíveis ações automáticas:

```text
reiniciar worker
reprocessar job idempotente
alternar provider
isolar fila contaminada
reabrir circuit breaker após teste
reconstruir índice derivado
recalcular cache
reexecutar evaluator
restaurar versão conhecida
```

Ações que alterem conhecimento global, políticas, ontologia ou estado crítico **não entram em self-healing irrestrito**.

---

# 9. Observabilidade como sistema nervoso operacional

Em escala empresarial, não basta o organismo funcionar. Ele precisa revelar o que está acontecendo.

Cada fluxo relevante deve permitir reconstruir:

```text
quem recebeu
quem processou
qual capability foi usada
qual versão
qual custo
qual latência
qual evidência
qual decisão
qual fallback
qual erro
qual derivado nasceu
qual onda cognitiva foi acionada
qual política permitiu/bloqueou
```

Métricas iniciais de saúde podem incluir:

- success rate por capability;
- correction rate;
- false-positive rate;
- false-negative rate;
- drift score;
- quarantine rate;
- rollback rate;
- latency p50/p95/p99;
- cost per event;
- escalation rate para IA;
- escalation rate para humano;
- lineage completeness;
- stale/tainted derivatives;
- agent disagreement rate;
- evaluator regression rate.

---

# 10. Organismo ≠ microserviços obrigatórios

A metáfora de muitas células não significa criar centenas de microserviços no início.

Uma célula cognitiva pode ser:

```text
uma função
um módulo
uma regra
uma consulta SQL
um worker
um algoritmo
um serviço
um modelo local
um agente externo
```

A unidade arquitetural é a **responsabilidade**, não o processo de deploy.

O projeto continua com a decisão de começar como **monólito modular**, extraindo serviços somente quando escala, isolamento, segurança ou operação justificarem.

---

# 11. Organismo e Explosão Atômica

A Explosão Atômica Recursiva ganha um requisito adicional:

> cada nova geração de derivados precisa permanecer biologicamente “rastreável” no sentido arquitetural: lineage, integridade, escopo e confiança não podem se perder entre ondas.

```text
ATOM A
  │
  ├──► DERIVADO B
  │      ├──► RELAÇÃO C
  │      └──► HIPÓTESE D
  │              └──► CANDIDATO E
  │
  └── lineage completo
```

Se `B` for revogado, o sistema deve conseguir localizar `C`, `D` e `E` e avaliar seu blast radius.

---

# 12. Princípios derivados

**DECISÃO APROVADA**

1. O Eva Engine® deve operar como um sistema de responsabilidades especializadas, não como um agente monolítico.
2. Átomos e derivados relevantes devem possuir envelope mínimo de provenance, lineage, escopo e integridade.
3. O sistema deve possuir um Integrity & Resilience Plane separado do Learning Quarantine Plane.
4. Anomalias devem ser isoladas antes de serem promovidas ou propagadas.
5. Correção deve preservar auditabilidade; “destruir” dados não é o comportamento padrão.
6. Falhas de capabilities críticas precisam ser detectáveis e visíveis.
7. Supervisão deve combinar health checks, observabilidade, dependency graph e orchestration.
8. Auto-recuperação só é automática quando sua segurança é demonstrável.
9. A metáfora de organismo não obriga microserviços; responsabilidades podem começar dentro de um monólito modular.

---

# 13. Questões em aberto

- schema final do Atomic Envelope;
- trust tiers;
- integrity states;
- política de taint propagation;
- cálculo de blast radius;
- critérios de poisoning detection;
- estratégia de drift detection;
- política de circuit breakers;
- health model do Capability Registry;
- quando o supervisor escala para IA ou humano;
- quais recoveries podem ser totalmente automáticos;
- como medir homeostase cognitiva e operacional.

---

# 14. Frase de arquitetura

> **O Eva Engine® não será uma peça inteligente cercada de acessórios. Será um organismo de capacidades especializadas: cada unidade sabe o que pode fazer, cada átomo sabe de onde veio, cada ameaça pode ser isolada, cada falha pode ser percebida e cada aprendizado precisa sobreviver à validação antes de tocar o núcleo confiável.**
