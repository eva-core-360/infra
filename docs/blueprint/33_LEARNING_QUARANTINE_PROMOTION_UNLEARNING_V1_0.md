# Eva Engine® — Learning Quarantine, Promotion & Unlearning v1.0

**Status:** base arquitetural vigente para refinamento, implementação e testes  
**Função:** consolidar o segundo círculo do Eva Engine® como plano isolado de aprendizagem candidata, experimentação, avaliação, promoção, revogação e desaprendizado controlado, impedindo que descoberta experimental contamine silenciosamente o Trusted Core.

---

# 1. Princípio central

O Eva Engine® pode aprender continuamente sem possuir permissão para acreditar imediatamente no que aprendeu.

```text
TRUSTED EXECUTION
      │
      │ sinais / feedback / snapshots autorizados
      ▼
LEARNING QUARANTINE
      │
      │ candidatos
      ▼
EVALUATION + CHALLENGE + POLICY
      │
      ▼
PROMOTION GATE
      │
      ├────────► REJECT
      ├────────► HOLD
      ├────────► SHADOW
      ├────────► CANARY
      └────────► PROMOTE VERSION
```

Regra:

> **Aprender pode ser contínuo; confiar é um processo de promoção.**

---

# 2. O segundo círculo é uma trust boundary

O Learning Quarantine Plane não é uma pasta, fila ou tabela com nome diferente.

Ele representa uma **fronteira de confiança**.

```text
╔══════════════════════════════════════════════════════════════╗
║                LEARNING QUARANTINE PLANE                    ║
║                                                              ║
║  experimental rules · weights · routes · relations          ║
║  candidate lenses · candidate capabilities · hypotheses     ║
║  candidate schemas · candidate domain knowledge             ║
║                                                              ║
║             NO DIRECT WRITE TO TRUSTED CORE                 ║
╚═══════════════════════════╤══════════════════════════════════╝
                            │
                     Promotion Artifact
                            │
                            ▼
                   ┌──────────────────┐
                   │  PROMOTION GATE  │
                   └────────┬─────────┘
                            │
                            ▼
╔══════════════════════════════════════════════════════════════╗
║                   TRUSTED EXECUTION                         ║
║  versioned · observable · reversible · policy governed      ║
╚══════════════════════════════════════════════════════════════╝
```

Direção de implementação madura:

- credenciais separadas;
- permissões separadas;
- namespaces/tabelas separadas;
- ausência de escrita direta em estado promovido;
- APIs de promoção explícitas;
- artefatos promovidos assináveis/verificáveis quando justificável;
- logs e traces próprios;
- segregação por tenant/scope;
- trilha de auditoria de promoção;
- rollback independente do ambiente de experimentação.

A v0 executável pode compartilhar processo/repositório, mas não autoridade de escrita.

---

# 3. Candidate é uma classe de confiança, não um tipo semântico

Um candidato pode representar qualquer mudança durável proposta:

```text
RuleCandidate
WeightCandidate
ThresholdCandidate
RelationCandidate
RoutingCandidate
LensActivationCandidate
CapabilityCandidate
SchemaCandidate
OntologyCandidate
AliasCandidate
PatternCandidate
DomainKnowledgeCandidate
ModelCandidate
PolicyCandidate
EvaluatorCandidate
```

Todos compartilham a propriedade:

```text
trust_state = CANDIDATE
```

Não existe promoção automática por quantidade de uso, repetição ou aparência de qualidade.

---

# 4. Learning Candidate Envelope

Contrato conceitual:

```text
LearningCandidate
├── candidate_id
├── candidate_type
├── scope
│   ├── session
│   ├── tenant
│   ├── domain
│   └── global
├── proposed_change
├── source_refs[]
├── training_evidence_refs[]
├── counterevidence_refs[]
├── independence_groups[]
├── produced_by
├── mechanism_version
├── engine_version
├── created_at
├── expected_benefit
├── expected_cost_delta
├── expected_risk_delta
├── known_failure_modes[]
├── privacy_class
├── risk_class
├── evaluation_plan_id
├── status
└── cognitive_envelope
```

O payload específico varia por tipo de candidato.

---

# 5. Quatro níveis de alcance, quatro barras de evidência

```text
L1 — SESSION / CONTEXT
alcance curto
reversão fácil
promoção leve

L2 — TENANT / ORGANIZATION
personalização persistente
isolamento obrigatório
baseline por tenant quando aplicável

L3 — DOMAIN
pode afetar muitos tenants do mesmo domínio
exige datasets e evaluators de domínio

L4 — GLOBAL
altera comportamento geral
maior barra de evidência, segurança e aprovação
```

Princípio:

> **Quanto maior o raio de impacto potencial, maior a exigência de evidência e controle.**

---

# 6. Candidate Lifecycle

```text
DISCOVERED
    │
    ▼
REGISTERED
    │
    ▼
STRUCTURALLY_VALID
    │
    ▼
UNDER_EVALUATION
    │
    ├────────► REJECTED
    ├────────► HOLD
    │
    ▼
SHADOW_ELIGIBLE
    │
    ▼
SHADOW
    │
    ├────────► REJECTED
    ├────────► REVISE
    │
    ▼
CANARY_ELIGIBLE
    │
    ▼
CANARY
    │
    ├────────► ROLLBACK
    │
    ▼
PROMOTED
    │
    ├────────► SUPERSEDED
    ├────────► REVOKED
    └────────► UNLEARNING_REQUIRED
```

Nem todo candidato precisa passar por shadow/canary. A policy define exigência conforme risco e alcance.

---

# 7. Promotion Gate

O Promotion Gate recebe uma proposta formal, não apenas um `candidate_id`.

Contrato conceitual:

```text
PromotionRequest
├── candidate_id
├── target_scope
├── target_version
├── baseline_ref
├── evaluation_report_refs[]
├── holdout_report_ref?
├── red_team_report_ref?
├── shadow_report_ref?
├── canary_plan_ref?
├── counterevidence_summary
├── security_review_ref?
├── privacy_review_ref?
├── economic_impact_ref?
├── rollback_plan_ref
├── approval_requirements[]
└── trace_id
```

Gate mínimo:

```text
STRUCTURE
   ↓
PROVENANCE
   ↓
SCOPE
   ↓
EVIDENCE QUALITY
   ↓
COUNTER-EVIDENCE
   ↓
BASELINE COMPARISON
   ↓
HOLDOUT / ADVERSARIAL quando exigido
   ↓
SECURITY / PRIVACY
   ↓
COST / LATENCY
   ↓
ROLLBACK READINESS
   ↓
POLICY
   ↓
PROMOTE / HOLD / REJECT
```

---

# 8. Promotion Manifest

Toda promoção relevante deve gerar um **Promotion Manifest** imutável ou append-oriented.

```text
PromotionManifest
├── promotion_id
├── candidate_id
├── source_version
├── target_version
├── promoted_scope
├── promoted_at
├── approved_by[]
├── evaluator_versions[]
├── dataset_versions[]
├── policy_version
├── evidence_refs[]
├── known_limitations[]
├── rollback_target
├── artifact_hash?
└── trace_id
```

Princípio:

> **O Core não muda de ideia; o Core muda de versão com uma justificativa auditável.**

---

# 9. Shadow Mode

Shadow Mode permite executar um candidato sobre tráfego autorizado sem afetar o resultado oficial.

```text
EVENT
  │
  ├────────► TRUSTED VERSION ─────► OFFICIAL RESULT
  │
  └────────► CANDIDATE SHADOW ────► SHADOW RESULT
                                       │
                                       ▼
                                   EVALUATION
```

Medir:

- qualidade;
- divergência;
- falsos positivos/negativos;
- latência;
- custo;
- taxa de escalonamento;
- comportamento por segmento;
- novas falhas;
- impacto econômico estimado;
- efeitos em downstream capabilities.

Shadow não concede autoridade de escrita em produção.

---

# 10. Canary Promotion

Canary reduz blast radius de uma mudança já aprovada para exposição limitada.

```text
PROMOTED CANDIDATE
       │
       ▼
AUTHORIZED CANARY SCOPE
       │
       ├── small traffic slice
       ├── selected tenants
       ├── selected capability path
       └── explicit time window
       │
       ▼
OBSERVE + EVALUATE
       │
       ├────────► EXPAND
       └────────► ROLLBACK
```

Canary não substitui holdout ou Evaluation Plane; mede comportamento operacional real.

---

# 11. O problema do aprendizado contaminado

Um candidato pode parecer bom porque aprendeu sobre dados ruins.

Fontes de contaminação:

```text
duplicação
feedback fraudulento
poisoning
bias de seleção
leakage entre treino e holdout
Evidence Echo
dados de outro tenant
rótulos errados
semantic drift
outliers tratados como norma
self-generated evidence
```

Todo candidato relevante deve manter lineage de:

```text
training evidence
validation evidence
holdout evidence
counter-evidence
```

---

# 12. Unlearning — corrigir aprendizado já promovido

**DECISÃO APROVADA COMO CAPACIDADE NECESSÁRIA**

O motor precisa possuir caminho explícito para remover a influência de algo promovido que se revelou incorreto, nocivo, inválido ou fora de escopo.

Nome arquitetural:

**Controlled Unlearning / Learning Revocation**

Unlearning não significa apagar a história.

Significa:

```text
IDENTIFICAR O QUE NÃO DEVE MAIS INFLUENCIAR
      ↓
REVOGAR SUA AUTORIDADE
      ↓
LOCALIZAR DESCENDENTES
      ↓
CALCULAR BLAST RADIUS
      ↓
RECOMPUTAR ESTADO DERIVADO
      ↓
VERIFICAR RESULTADO
      ↓
PROMOVER ESTADO CORRIGIDO
```

---

# 13. Unlearning Protocol

```text
LEARNING DEFECT DETECTED
        │
        ▼
ROOT CAUSE / ARTIFACT IDENTIFICATION
        │
        ▼
REVOKE / SUPERSEDE
        │
        ▼
FREEZE FURTHER PROPAGATION
        │
        ▼
LINEAGE TRAVERSAL
        │
        ▼
BLAST RADIUS
        │
        ├── direct descendants
        ├── downstream decisions
        ├── derived indexes
        ├── routing policies
        ├── learned weights
        └── dependent candidates
        │
        ▼
MARK TAINT / REQUIRES_RECOMPUTE
        │
        ▼
REPROCESS FROM TRUSTED ANCESTOR
        │
        ▼
EVALUATE
        │
        ▼
CORRECTED VERSION
```

---

# 14. Tipos de unlearning

## 14.1 Rule Unlearning

Revogar regra/heurística promovida.

## 14.2 Weight Unlearning

Retirar peso aprendido e reconstruir estado a partir de checkpoint/base confiável.

## 14.3 Relation Unlearning

Revogar relação aprendida e reavaliar inferências dependentes.

## 14.4 Routing Unlearning

Retirar política de roteamento aprendida que degradou custo/qualidade.

## 14.5 Domain Knowledge Unlearning

Corrigir conhecimento de domínio promovido como inválido/obsoleto.

## 14.6 Data Influence Revocation

Quando tecnicamente possível e necessário, remover influência de um conjunto de fontes invalidado.

O método físico depende do mecanismo. Alguns modelos exigirão retraining/rebuild em vez de remoção pontual.

---

# 15. Learning Checkpoints

Para mecanismos adaptativos, considerar checkpoints versionados.

```text
STATE v10
  ↓ learning
STATE v11
  ↓ learning
STATE v12
```

Se v12 é contaminado:

```text
restore trusted checkpoint v11
          +
replay authorized clean learning events
          ↓
STATE v12b
```

Esse padrão reduz dependência de “cirurgia” impossível em estado aprendido.

---

# 16. Learning Event Log

O aprendizado durável precisa de um log suficiente para replay/auditoria.

```text
LearningEvent
├── event_id
├── candidate_id
├── action
├── scope
├── evidence_refs[]
├── evaluator_ref?
├── policy_ref?
├── previous_state_ref?
├── resulting_state_ref?
├── timestamp
└── trace_id
```

A arquitetura não exige event sourcing total, mas exige histórico suficiente para reconstruir mudanças relevantes.

---

# 17. Supervisores do Learning Plane

```text
LEARNING QUARANTINE
│
├── Provenance Guard
├── Scope Guard
├── Privacy Guard
├── Dedup Guard
├── Poisoning Detector
├── Evidence Independence Checker
├── Contradiction / Challenger
├── Drift Monitor
├── Evaluator
├── Cost Evaluator
├── Promotion Controller
└── Rollback / Unlearning Controller
```

Esses papéis são capabilities; podem ser implementados por regra, estatística, algoritmo, modelo local, IA supervisora ou humano conforme risco.

---

# 18. O Learning Plane também possui Health

Métricas candidatas:

```text
candidate_generation_rate
candidate_rejection_rate
promotion_rate
rollback_rate
unlearning_rate
shadow_divergence
holdout_regression_rate
scope_violation_rate
poisoning_detection_rate
promotion_latency
promotion_cost
post_promotion_incident_rate
```

Uma taxa crescente de rollback pode indicar problema no gate, nos dados ou nos evaluators.

---

# 19. Learning Economics

Aprendizado também custa.

Medir, quando aplicável:

```text
cost_per_candidate
cost_per_evaluation
cost_per_promoted_change
cost_per_shadow_run
cost_per_canary
cost_of_rollback
cost_of_unlearning
observed_value_after_promotion
```

Princípio:

> **Aprender não é automaticamente valioso; mudança durável precisa justificar seu custo e risco.**

---

# 20. Isolamento por tenant e domínio

Um candidato de tenant A não pode ganhar autoridade sobre tenant B por acidente.

```text
TENANT A SIGNALS
      ↓
L2 CANDIDATE — scope=A
      │
      X────────► tenant B
      │
      X────────► global
      │
      └────────► explicit broader promotion process only
```

Promover L2 → L3/L4 é uma nova decisão de aprendizagem, não continuação automática.

---

# 21. Aprendizado por IA não ganha privilégio

Uma IA pode:

- sugerir regra;
- detectar padrão;
- propor relação;
- gerar teste;
- criticar candidato;
- recomendar promoção.

Mas sua saída permanece:

```text
Artifact / Candidate
```

Nunca:

```text
Trusted Rule by default
```

---

# 22. Promotion Gate também precisa ser protegido

O gate é alvo crítico.

Riscos:

```text
policy bypass
forged evaluator result
stale baseline
holdout leakage
approval spoofing
artifact substitution
race condition
cross-tenant scope confusion
compromised promotion controller
```

Logo, o Promotion Gate pertence ao Threat Model e ao Integrity & Resilience Plane.

---

# 23. Invariantes v1.0

1. Learning Candidate nunca escreve diretamente em Trusted Core.
2. Alcance do aprendizado é explícito.
3. Promoção gera versão/manifesto auditável.
4. Evidência de treinamento e avaliação permanece distinguível.
5. Holdout não pode ser silenciosamente usado como treino.
6. Counter-evidence acompanha candidatos relevantes.
7. Promoção de maior alcance exige barra de evidência maior.
8. Shadow não altera resultado oficial.
9. Canary possui rollback definido antes de iniciar.
10. Toda mudança promovida relevante pode ser revogada.
11. Unlearning preserva histórico e remove autoridade, não evidência histórica.
12. Blast radius é calculável a partir de lineage quando necessário.
13. Checkpoints/replay são preferidos quando remoção pontual não é tecnicamente segura.
14. IA não possui autoridade especial de promoção.
15. Learning Plane possui health, observabilidade e economics próprios.
16. Promotion Gate é componente crítico e protegido.

---

# 24. Questões em aberto

- formato físico do Learning Store;
- separação física inicial por credenciais/tabelas;
- formato final do Promotion Manifest;
- critérios por nível L1-L4;
- requisitos de aprovação humana por risco;
- política de retenção de candidatos rejeitados;
- estratégia de checkpoint por mecanismo;
- unlearning de modelos externos/proprietários;
- limites de replay;
- política de expiração de learning candidates;
- definição de learning debt;
- detecção de concept drift por domínio;
- custo máximo aceitável de promoção;
- assinatura/verificação criptográfica de artefatos promovidos.

---

# 25. Frases de fundação

> **O motor pode aprender sem ter permissão para acreditar imediatamente no que aprendeu.**

> **Aprender é propor mudança; promover é conceder autoridade.**

> **Desaprender não é apagar o passado. É retirar do passado errado o poder de continuar moldando o futuro.**
