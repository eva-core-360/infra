# Eva Engine® — Contexto de Continuidade

**Função deste documento:** permitir que um novo chat, agente ou desenvolvedor retome o projeto sem reconstruir a conversa original e sem reduzir o Eva Engine® ao primeiro produto que inspirou seus mecanismos.

---

# 1. Estado atual do projeto

O projeto saiu da fase de Blueprint puramente conceitual e atingiu uma **base arquitetural suficiente para iniciar o primeiro heartbeat executável**, ainda em P&D privado.

O repositório `eva-core-360/infra` permanece a fonte persistente de verdade arquitetural.

**Foco vigente:** Eva Engine® como infraestrutura cognitiva generalista B2B enterprise, orientada a eventos, com execução confiável, evidência, orquestração, aprendizagem isolada, resiliência, avaliação, observabilidade, economia cognitiva e segurança cognitiva.

O primeiro runtime ainda não foi iniciado. A especificação executável está em:

`36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md`

Questão imediata em aberto: confirmar se o runtime viverá em repositório privado separado, com preferência atual por algo como:

```text
eva-core-360/engine
```

---

# 2. Origem — laboratório, não teto

A origem prática veio de mecanismos testados em um produto de notas/memória.

Isso forneceu evidência de que combinações pequenas, especialmente determinísticas, podem gerar comportamento útil.

O produto anterior é tratado como:

```text
LABORATORIO
+
EVIDENCIA HISTORICA
+
FONTE DE CASOS DE TESTE
```

não como arquitetura-alvo.

A bateria histórica com 508 cenários está resumida em:

`16_LICOES_DO_LABORATORIO_INTELIGENCIA_LOCAL.md`

Lição central:

> mecanismos simples podem produzir muito valor; heurísticas sem avaliação podem amplificar erro.

---

# 3. Definição atual do Eva Engine®

Não é:

- bloco de notas;
- chatbot;
- wrapper de LLM;
- único agente;
- banco com automações;
- sistema que aprende diretamente em produção.

É um **Cognitive Runtime / Cognitive Fabric** generalista.

Princípio:

> **Produtos dependem do Eva Engine®. O Eva Engine® não depende de nenhum produto consumidor.**

---

# 4. Horizonte B2B enterprise

O público-alvo estratégico é enterprise.

Dores investigadas:

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

A tese econômica é decompor trabalho cognitivo e usar o mecanismo mais barato/previsível que satisfaça o requisito, escalando para IA potente ou humano quando houver ganho mensurável.

Nenhuma economia ou ROI é afirmada antes de prova correspondente.

Escada de evidência:

```text
E0 ideia
E1 prova de mecanismo
E2 bateria reproduzível
E3 escala sintética
E4 piloto de domínio
E5 prova operacional
E6 prova econômica
```

---

# 5. Arquitetura 360

O conceito 360 evoluiu para um Core estável cercado por órbita extensível de lentes, capabilities, agentes, guards, evaluators, policies e supervisores.

```text
                  ORBITA COGNITIVA
        lens · guard · specialist · evaluator
                    ╲    │    ╱
                     [ CORE ]
                    ╱    │    ╲
        policy · challenger · registry · agent
```

O Core não precisa crescer proporcionalmente ao número de capacidades.

Ele precisa saber:

```text
registrar
descobrir
selecionar
autorizar
orquestrar
limitar
avaliar
versionar
revogar
```

---

# 6. Organismo cognitivo

Metáfora vigente:

```text
organismo                = Cognitive Fabric
núcleo                    = Trusted Execution Core / Cognitive Kernel
célula                    = Capability / Guard / Specialist
membrana                  = Integration Boundary / Policy Gate
sistema imunológico       = Integrity & Resilience Plane
circulação                = Event & Artifact Flow
mutação candidata         = Learning Candidate
homeostase                = Operational Stability
```

A metáfora é arquitetural, não alegação neurocientífica.

---

# 7. Cognitive Kernel

Documento:

`25_COGNITIVE_KERNEL_V0_1.md`

O Kernel é mínimo e neutro.

Conhece:

```text
identity
scope
envelopes
events
state transitions
lineage
policy gates
capability invocation
budgets
traces
versions
integrity
```

Não conhece notas, domínios, idiomas, LLMs ou fornecedores específicos.

Princípio:

> **O Kernel deve permanecer menor que o ecossistema que governa.**

---

# 8. Atomic / Cognitive Envelope

Documento:

`29_ATOMIC_COGNITIVE_ENVELOPE_V1_0.md`

Todo artefato relevante circula com identidade, scope, lineage, trust, integrity, versão e policy suficientes.

Separação:

```text
ENVELOPE
controle / identidade / governança

PAYLOAD
conteúdo semântico
```

Metadados pesados podem ser referenciados para evitar overhead excessivo.

---

# 9. Evidence Model

Documento:

`26_EVIDENCE_MODEL_V0_1.md`

Conceitos distintos:

```text
SIGNAL
EVIDENCE
CLAIM
HYPOTHESIS
SCORE
CONFIDENCE
DECISION
```

Regra central:

> **Score não é Confidence.**

Outro princípio:

> **novo derivado não significa nova evidência independente.**

Lineage e independence groups protegem contra Evidence Echo.

---

# 10. Cognitive Lenses

Documentos:

`18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md`

`19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md`

Lentes são formas de observar, não necessariamente executores.

```text
LENS
como observar

CAPABILITY
o que o sistema sabe fazer

AGENT / MECHANISM
quem/como executa
```

O acervo histórico de 32 lentes é fonte de arquitetura e futuras composições; não é lista fixa do Core.

Existe pista histórica de redução/hierarquia `32 → 12 → 8`, ainda não reconstruída de forma confiável.

---

# 11. Registries

Documento:

`27_CAPABILITY_HEALTH_SCHEMA_REGISTRIES_V0_1.md`

```text
SCHEMA REGISTRY
que estrutura é esta?

CAPABILITY REGISTRY
quem sabe fazer o quê?

HEALTH REGISTRY
quem está apto a fazer agora?
```

Health possui dimensões:

```text
technical
cognitive
economic
```

Capability é contrato; agente/modelo/função é executor.

---

# 12. Orchestration

Documento:

`28_ORCHESTRATION_MODEL_V0_1.md`

Separação:

```text
CONTROL PLANE
planeja · seleciona · autoriza · limita · replaneja

EXECUTION PLANE
executa capabilities · produz artifacts/evidence/metrics
```

Regra central:

> **A capability pode pedir para continuar; o Orchestrator decide se o organismo continua.**

Capabilities propõem `NextStepCandidate`; nova onda exige Admission Control + budget + policy.

---

# 13. Explosão Atômica Recursiva

Documento:

`20_EXPLOSAO_ATOMICA_RECURSIVA_E_ESCALONAMENTO_DE_IA.md`

A resposta pode gerar derivados; derivados podem alimentar nova onda.

```text
WAVE 0 original
WAVE 1 derivados primários
WAVE 2 relações/contexto
WAVE 3 hipóteses
WAVE 4 contraprovas
...
STOP
```

Toda expansão possui limites de:

```text
fan-out
waves
depth
cost
time
risk
novelty / information gain
```

---

# 14. Integrity & Resilience

Documento:

`30_INTEGRITY_RESILIENCE_PLANE_V0_1.md`

Fluxo:

```text
DETECT
  ↓
CLASSIFY
  ↓
CONTAIN
  ↓
ISOLATE / DEGRADE / QUARANTINE
  ↓
TRACE LINEAGE
  ↓
BLAST RADIUS
  ↓
RECOVER
  ↓
VERIFY
```

Princípio:

> **O organismo pode tolerar falhas de peças; não pode tolerar perda silenciosa de integridade.**

---

# 15. Learning Quarantine + Controlled Unlearning

Documento vigente consolidado:

`33_LEARNING_QUARANTINE_PROMOTION_UNLEARNING_V1_0.md`

O segundo círculo é uma trust boundary.

```text
TRUSTED EXECUTION
      ↓ sinais autorizados
LEARNING QUARANTINE
      ↓ evaluation/challenge
PROMOTION GATE
      ↓
PROMOTED VERSION
```

Learning Candidate nunca escreve diretamente no Core.

Promoção gera manifesto/versionamento.

Se algo promovido estiver errado:

```text
revoke authority
→ trace lineage
→ blast radius
→ recompute
→ evaluate
→ corrected version
```

Princípio:

> **Desaprender não é apagar o passado. É retirar do passado errado o poder de continuar moldando o futuro.**

---

# 16. Evaluation Plane

Documento:

`31_EVALUATION_PLANE_V0_1.md`

Avalia:

```text
capability
composition
system
```

Usa baselines, golden, holdout, adversarial, shadow, canary, calibration, ablation, cost/latency e hard safety gates.

Não existe “Eva Score” único que possa esconder regressão crítica em média agregada.

---

# 17. Observability & Cognitive Economics

Documento:

`32_OBSERVABILITY_COGNITIVE_ECONOMICS_V0_1.md`

Mede:

```text
quality
latency
cost
capability path
AI escalation
human escalation
wave count
stop reason
marginal cognitive value
```

Objetivo B2B:

> saber quanto custou pensar e se o ganho justificou o trabalho.

---

# 18. Enterprise Integration Boundary

Documento:

`34_ENTERPRISE_INTEGRATION_BOUNDARY_V0_1.md`

Sistemas externos não acessam o Kernel diretamente.

```text
ERP / CRM / logs / APIs / sensors
        ↓
ADAPTER
        ↓
ANTI-CORRUPTION / INTEGRATION BOUNDARY
        ↓
CANONICAL EVENT
        ↓
COGNITIVE ENVELOPE
```

Tenant/scope é resolvido antes da admissão.

Autenticidade da fonte não equivale a verdade.

Ações externas passam por `ActionRequest + Policy + adapter`.

---

# 19. Enterprise Cognitive Threat Model

Documento:

`35_ENTERPRISE_COGNITIVE_THREAT_MODEL_V0_1.md`

Ameaças cobertas incluem:

```text
cross-tenant leakage
provenance spoofing
data/knowledge poisoning
Evidence Echo / laundering
prompt injection
agent hijacking
orchestrator abuse
denial of wallet
resource exhaustion
schema confusion
replay
promotion-gate compromise
evaluation poisoning
observability blindness
supply-chain risk
insider risk
```

Princípio:

> **Segurança protege não só o que a Eva executa, mas também o que ela pode acreditar.**

---

# 20. Primeiro heartbeat executável

Documento:

`36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md`

Primeiro fluxo:

```text
EVENT
  ↓
INGRESS VALIDATION
  ↓
COGNITIVE ENVELOPE
  ↓
SCOPE / POLICY
  ↓
REGISTRIES
  ↓
ORCHESTRATION PLAN
  ↓
DETERMINISTIC CAPABILITY
  ↓
COGNITIVE ARTIFACT
  ↓
EVIDENCE / TRACE
  ↓
RESULT
  ↓
OBSERVABILITY
```

Sem LLM obrigatório, embeddings, UI ou domínio específico.

Primeira capability de prova:

```text
CAP_STRUCTURED_OBSERVATION_EXTRACT
```

Objetivo inicial não é provar “inteligência”. É provar invariantes, circulação, idempotência, scope, policy, failure containment e trace.

---

# 21. Primeira tarefa do Cursor

Depois de confirmar onde ficará o runtime executável, implementar somente:

```text
packages/contracts
packages/schemas
packages/envelope
```

Critérios:

```text
tests pass
typecheck pass
invalid envelopes fail validation
valid fixtures round-trip without mutation
no DB
no HTTP
no LLM
no domain code
```

Ordem posterior:

```text
registries
→ policy/budget
→ deterministic capability
→ orchestrator/trace
→ integrity
→ API
→ persistence
→ CI/benchmark
```

---

# 22. Stack vigente

- TypeScript;
- monólito modular;
- PostgreSQL/Supabase quando persistência física entrar;
- HTTP/REST inicialmente;
- workers para tarefas assíncronas futuras;
- providers intercambiáveis;
- GitHub como fonte de verdade;
- Cursor como executor da spec;
- testes unit/integration/golden/regression/adversarial/fault injection;
- logs estruturados;
- sem secrets no repositório.

Ferramentas específicas ainda abertas: package manager, runtime schema validator, HTTP framework, queue provider, observability provider.

---

# 23. Como continuar em novo chat/agente

1. Ler `README.md` e sua ordem obrigatória.
2. Ler `24_MAPA_MESTRE_ARQUITETURA_ENTERPRISE_V0_2.md`.
3. Ler `25` a `36` na ordem.
4. Ler `01_REGISTRO_DECISOES.md`.
5. Ler este documento.
6. Ler `AGENTS.md`.
7. Não voltar automaticamente para notas/Eva Memory.
8. Não inventar arquitetura no código.
9. Antes de implementação, seguir `36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md`.
10. Atualizar Blueprint se uma decisão estrutural mudar.

---

# 24. Questões imediatas em aberto

- runtime em repo separado ou no `infra` — preferência atual: repo privado separado;
- nome final do repo executável;
- package manager / monorepo tooling;
- runtime schema validation library;
- primeira estratégia de IDs;
- primeira persistence migration;
- authN/authZ;
- limites numéricos iniciais de budget;
- primeiro domínio B2B E4 depois do heartbeat;
- quando iniciar IA supervisora;
- quais Cognitive Lenses entram na primeira capability cognitiva pós-heartbeat.

---

# 25. Frases-guia

> **Não estamos construindo um bloco de notas que ficou grande. Estamos construindo um motor que começou pequeno o suficiente para ser testado.**

> **Nascer pequeno na implementação não significa nascer pequeno na arquitetura.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**

> **O primeiro coração não precisa pensar muito. Precisa bater certo.**
