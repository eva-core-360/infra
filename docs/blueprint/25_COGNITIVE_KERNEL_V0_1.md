# Eva Engine® — Cognitive Kernel v0.1

**Status:** base arquitetural vigente para refinamento e testes  
**Função:** definir o núcleo irredutível do Eva Engine®: as poucas responsabilidades universais que precisam existir no centro para que todo o restante — idiomas, lentes, agentes, domínios, modelos, aprendizado e produtos — possa crescer ao redor sem contaminar o Core.

---

# 1. Definição

O **Cognitive Kernel** não é a parte que “sabe mais”.

Ele é a parte que **garante que tudo o que sabe, faz, deriva ou aprende passe por contratos universais, rastreáveis e governáveis**.

Princípio:

> **O Kernel deve permanecer menor que o ecossistema que ele governa.**

Quanto mais capacidades o Eva Engine® ganhar, menos desejável é empurrar detalhes específicos para dentro do Kernel.

O Kernel deve conhecer estruturas universais de execução — nunca detalhes de um produto, idioma, domínio ou fornecedor.

---

# 2. O que pertence ao Kernel

O Kernel deve possuir apenas responsabilidades que continuam verdadeiras em qualquer domínio.

```text
IDENTIDADE
ESCOPO
EVENTO
ENVELOPE
ESTADO
LINEAGE
VERSÃO
POLÍTICA
ROTEAMENTO
TRACE
ORÇAMENTO
INTEGRIDADE
```

Esses elementos são o “esqueleto” do organismo.

Não são a inteligência especializada.

---

# 3. O que NÃO pertence ao Kernel

**DECISÃO APROVADA COMO PRINCÍPIO DE FRONTEIRA**

Não pertencem ao Cognitive Kernel:

```text
notas
áreas da vida
CRM
saúde
finanças
logística
léxicos de idioma
prompts
embeddings
LLMs
modelos específicos
heurísticas de um domínio
regras de UI
visualização
lentes específicas
agentes específicos
fórmulas de produto
provedor de banco
provedor de nuvem
```

Esses elementos vivem em módulos, capabilities, registries, Domain Packs, adapters ou planos externos.

Regra:

> **Se uma capacidade pode desaparecer sem destruir a identidade do Eva Engine®, ela provavelmente não pertence ao Kernel.**

---

# 4. Visão em caixa

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                         EVA ENGINE® ECOSYSTEM                              │
│                                                                             │
│  Language · Atomizer · Context · Lenses · Relations · Learning · AI · B2B │
│  Domain Packs · Integrations · Agents · Evaluators · Products             │
│                                  │                                          │
│                                  ▼                                          │
│                    ┌───────────────────────────┐                            │
│                    │     COGNITIVE KERNEL      │                            │
│                    │                           │                            │
│                    │ identity                  │                            │
│                    │ scope                     │                            │
│                    │ envelopes                 │                            │
│                    │ state transitions         │                            │
│                    │ lineage                   │                            │
│                    │ capability invocation     │                            │
│                    │ policy gates              │                            │
│                    │ budget                    │                            │
│                    │ trace                     │                            │
│                    │ version/integrity         │                            │
│                    └─────────────┬─────────────┘                            │
│                                  │                                          │
│                                  ▼                                          │
│                       STORAGE / EVENT LOG                                   │
│                     via interfaces/adapters                                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

# 5. Primitiva 1 — Kernel Envelope

Todo objeto aceito pelo Kernel deve viajar dentro de um envelope universal.

O **Atomic Envelope** descrito anteriormente é especialização cognitiva desse princípio.

Contrato conceitual mínimo:

```text
KernelEnvelope
├── object_id
├── object_type
├── root_event_id
├── parent_id?
├── tenant_id / scope_id
├── created_at
├── provenance
├── schema_id
├── schema_version
├── engine_version
├── epistemic_level
├── trust_state
├── integrity_state
├── policy_context
├── lineage_refs[]
├── trace_id
└── payload_ref / payload
```

O Kernel não precisa compreender semanticamente o `payload` para aplicar identidade, escopo, lineage, versão e políticas estruturais.

---

# 6. Três eixos que nunca devem ser confundidos

Uma das responsabilidades mais importantes do Kernel é manter três dimensões separadas.

## 6.1 Epistemic Level

O que o objeto representa em relação ao conhecimento:

```text
RAW
DERIVED
INFERRED
LEARNED
```

## 6.2 Trust State

Qual o status de confiança operacional daquele objeto:

```text
UNVERIFIED
CANDIDATE
PROMOTED
SUPERSEDED
REVOKED
```

## 6.3 Integrity State

Qual a situação de integridade conhecida:

```text
CLEAN
SUSPECT
QUARANTINED
TAINTED
INVALIDATED
REQUIRES_RECOMPUTE
```

Exemplo:

```text
Objeto A
Epistemic = INFERRED
Trust      = PROMOTED
Integrity  = CLEAN
```

ou:

```text
Objeto B
Epistemic = LEARNED
Trust      = CANDIDATE
Integrity  = QUARANTINED
```

Essas dimensões são ortogonais.

Uma inferência pode estar promovida. Um aprendizado pode ainda estar em quarentena. Um dado RAW pode estar contaminado.

---

# 7. Primitiva 2 — Event

A decisão vigente permanece:

> **Evento é a unidade universal de entrada operacional.**

O Kernel aceita eventos sem pressupor que sejam notas, mensagens ou documentos.

```text
Event
├── event_id
├── event_type
├── source
├── actor?
├── timestamp
├── scope
├── schema
└── payload
```

Exemplos possíveis:

```text
content.created
payment.failed
deployment.failed
sensor.threshold_exceeded
customer.replied
contract.changed
machine.stopped
```

O Kernel conhece o evento como estrutura. O significado detalhado pertence às capabilities e Domain Packs.

---

# 8. Primitiva 3 — Cognitive Artifact

O Kernel precisa de um tipo universal para representar qualquer objeto produzido durante o processamento sem conhecer seu significado específico.

Nome inicial:

**Cognitive Artifact**

Pode representar:

```text
átomo
relação
sinal
contexto
hipótese
inferência
metadado
estado
resultado
contradição
learning candidate
```

Contrato conceitual:

```text
CognitiveArtifact
├── artifact_id
├── artifact_type
├── envelope
├── produced_by
├── evidence_refs[]
├── parent_refs[]
├── confidence?
├── score?
├── status
└── content
```

O `artifact_type` é extensível via Schema Registry.

O Kernel não hardcoda a ontologia inteira.

---

# 9. Primitiva 4 — Lineage Edge

A Explosão Atômica Recursiva exige que todo derivado relevante possa declarar sua ancestralidade.

```text
LineageEdge
├── from_id
├── to_id
├── derivation_type
├── produced_by
├── created_at
├── engine_version
└── trace_id
```

Tipos conceituais possíveis:

```text
DERIVED_FROM
SUPPORTED_BY
INFERRED_FROM
GENERATED_BY
SUPERSEDES
INVALIDATES
REQUIRES_RECOMPUTE
```

O Kernel deve ser capaz de reconstruir:

```text
resultado
   ↑
inferência
   ↑
relação
   ↑
átomo
   ↑
evento raiz
```

E também o caminho inverso para calcular blast radius:

```text
erro raiz
   ↓
derivados
   ↓
descendentes
   ↓
objetos afetados
```

---

# 10. Primitiva 5 — Processing Context

Toda execução precisa carregar contexto operacional suficiente para limitar o processamento.

```text
ProcessingContext
├── tenant_id
├── scope_id
├── trace_id
├── root_event_id
├── engine_version
├── policy_set
├── capability_budget
├── time_budget
├── compute_budget
├── cost_budget
├── risk_budget
├── max_depth
├── max_waves
└── deadline
```

Isso transforma limites em parte da execução, não em comentários espalhados pelo código.

---

# 11. Primitiva 6 — Capability Invocation

O Kernel não executa toda inteligência diretamente.

Ele invoca capabilities por contrato.

```text
CapabilityInvocation
├── capability_id
├── capability_version
├── input_refs[]
├── processing_context
├── required_policy
├── expected_output_schema
└── invocation_id
```

Resposta conceitual:

```text
CapabilityResult
├── invocation_id
├── status
├── artifacts[]
├── evidence_refs[]
├── metrics
├── warnings[]
└── escalation_request?
```

Isso permite que uma capability seja implementada como:

```text
função TypeScript
SQL
algoritmo estatístico
serviço local
modelo pequeno
agente
LLM externo
humano
```

sem alterar a identidade do Kernel.

---

# 12. Primitiva 7 — Policy Gate

O Kernel não precisa conhecer todas as políticas do mundo, mas precisa garantir que chamadas críticas respeitem um ponto de decisão explícito.

```text
PolicyDecision
├── decision_id
├── action
├── subject
├── resource
├── scope
├── result          # allow / deny / require_approval
├── policy_version
├── reason
└── trace_id
```

Nenhuma capability crítica deve possuir caminho lateral que ignore Policy.

---

# 13. Primitiva 8 — Processing Trace

Toda execução relevante precisa ser reconstruível.

```text
ProcessingTrace
├── trace_id
├── root_event_id
├── started_at
├── finished_at
├── modules_called[]
├── capabilities_called[]
├── policies_checked[]
├── artifacts_created[]
├── escalations[]
├── warnings[]
├── latency_ms
├── compute_usage
└── external_cost
```

O trace alimenta:

- auditoria;
- debugging;
- observabilidade;
- FinOps;
- avaliação de custo cognitivo;
- investigação de falhas;
- comparação entre versões.

---

# 14. Primitiva 9 — Version Vector

O motor precisa conseguir declarar quais versões participaram de um resultado.

```text
VersionVector
├── engine_version
├── kernel_version
├── ontology_version
├── schema_version
├── language_pack_version?
├── capability_versions{}
├── policy_version
├── model_versions{}
└── domain_pack_versions{}
```

Nem todos os campos precisam estar presentes em toda execução.

O objetivo é impedir resultados sem contexto de versão.

---

# 15. Máquina de estados mínima

Um artefato não deve simplesmente “existir”. Ele percorre estados explícitos.

```text
RECEIVED
   │
   ▼
VALIDATED
   │
   ▼
ADMITTED
   │
   ├─────────────► QUARANTINED
   │                    │
   │                    └──► REJECTED / PROMOTED
   │
   ▼
ACTIVE
   │
   ├──► SUPERSEDED
   ├──► REVOKED
   ├──► INVALIDATED
   └──► REQUIRES_RECOMPUTE
```

O fluxo exato pode variar por tipo de artefato, mas a existência de estados explícitos é parte da arquitetura.

---

# 16. Kernel e Learning Quarantine

**DECISÃO APROVADA**

O Kernel deve possuir uma fronteira estrutural entre execução confiável e aprendizado candidato.

```text
TRUSTED EXECUTION
       │
       ├────────────► produz Learning Candidate
       │                         │
       │                         ▼
       │                LEARNING QUARANTINE
       │                         │
       │                    Promotion Gate
       │                         │
       └◄────────────────────────┘
          somente artefato promovido
```

O Kernel **não aceita escrita direta de estado global aprendido** originada de candidate sem promoção válida.

---

# 17. Kernel e Supervisory AI

IA supervisora não faz parte do Kernel.

Ela é uma capability externa e governada.

O Kernel pode receber um pedido de escalonamento:

```text
EscalationRequest
├── reason
├── risk
├── ambiguity
├── attempted_capabilities[]
├── unresolved_conflicts[]
├── budget_remaining
└── required_authority
```

O Orchestrator/Policy decide se a escalada será:

```text
modelo maior
agente especializado
humano
ou silêncio/adiamento
```

O Kernel apenas garante que o escalonamento seja rastreável e autorizado.

---

# 18. O Kernel deve ser replayable

**HIPÓTESE FORTE / REQUISITO DE ENGENHARIA**

Sempre que possível, uma execução determinística deve poder ser reproduzida com:

```text
evento original
+
versões
+
configuração
+
políticas
+
inputs referenciados
```

Objetivo:

```text
mesma entrada + mesmo estado + mesmas versões
≈ mesmo resultado determinístico
```

Componentes probabilísticos devem registrar seeds, versões ou parâmetros suficientes quando tecnicamente viável, sabendo que provedores externos podem não oferecer determinismo absoluto.

---

# 19. O Kernel deve falhar fechado nos pontos críticos

Princípio:

> **Quando não é possível provar autorização, integridade, schema ou lineage mínimo exigido, o Kernel prefere conter a operação a aceitar silenciosamente o objeto.**

Isso não significa interromper tudo por qualquer aviso.

A política deve distinguir:

```text
warning
recoverable_error
quarantine
hard_reject
escalation
```

---

# 20. Critério de admissão de uma nova responsabilidade no Kernel

Antes de adicionar qualquer função ao Kernel, perguntar:

```text
1. Ela é universal em todos os domínios?
2. Ela precisa existir mesmo sem IA, idioma e produto?
3. A ausência dela quebra integridade, lineage ou execução?
4. Ela pode ser implementada como capability externa?
5. Ela aumenta muito o acoplamento do Core?
6. Ela pode evoluir independentemente?
```

Regra prática:

> **Na dúvida, manter fora do Kernel até existir evidência de que precisa estar dentro.**

---

# 21. Teste de pureza do Kernel

O Cognitive Kernel v0 deve conseguir rodar sem:

```text
LLM
embeddings
language pack
Domain Pack
UI
produto de notas
modelo de saúde
modelo financeiro
agente generativo
```

E ainda assim conseguir:

1. receber um evento genérico;
2. validar envelope/schema;
3. preservar identidade e origem;
4. criar `trace_id`;
5. aplicar escopo e política estrutural;
6. invocar uma capability stub;
7. receber um artefato derivado;
8. registrar lineage;
9. bloquear escrita direta de Learning Candidate no Trusted Core;
10. registrar custo/latência;
11. revogar um artefato;
12. localizar seus descendentes;
13. marcar descendentes para recomputação;
14. reproduzir a cadeia de processamento.

Se ele não consegue fazer isso, ainda não é um Kernel confiável.

---

# 22. Diagrama de sequência mínima

```text
SOURCE
  │
  │ Event
  ▼
BOUNDARY
  │ validate + scope
  ▼
KERNEL
  │ create trace
  │ admit envelope
  │ policy check
  ▼
ORCHESTRATOR
  │ capability invocation
  ▼
CAPABILITY
  │ produces artifacts
  ▼
KERNEL
  │ validate artifacts
  │ attach lineage
  │ enforce trust/integrity state
  ├──────────────► RESULT
  │
  └──────────────► LEARNING CANDIDATE
                         │
                         ▼
                  QUARANTINE ONLY
```

---

# 23. Relação com o modelo do organismo

Na metáfora biológica:

```text
Kernel Envelope     = membrana/identidade de circulação
Lineage             = genealogia/rastro
Policy Gate         = barreira seletiva
Integrity State     = estado imunológico
Capability          = célula especializada
Trace               = sinais vitais/histórico de atividade
Quarantine          = isolamento
Promotion Gate      = admissão controlada de nova capacidade
```

A metáfora ajuda a raciocinar.

A implementação deve usar contratos formais, estados, testes e métricas.

---

# 24. Invariantes do Cognitive Kernel v0.1

**DECISÕES APROVADAS COMO BASE VIGENTE**

```text
K01 — nada entra sem identidade e escopo.
K02 — original e derivado permanecem distinguíveis.
K03 — epistemic level, trust state e integrity state são dimensões separadas.
K04 — todo derivado relevante possui lineage.
K05 — toda execução relevante possui trace.
K06 — capability é invocada por contrato e versão.
K07 — política crítica não pode ser ignorada por caminho lateral.
K08 — Learning Candidate não escreve diretamente no Trusted Core.
K09 — artefato promovido pode ser revogado/superseded sem apagar auditoria.
K10 — o Kernel não depende de produto, domínio, idioma ou fornecedor de IA.
K11 — custo, tempo e risco são parte do contexto de processamento.
K12 — falhas de integridade podem produzir quarantine/recompute, não corrupção silenciosa.
K13 — o Kernel deve permitir localizar descendentes de um artefato para blast radius.
K14 — o Kernel deve ser pequeno o suficiente para permanecer estável enquanto o ecossistema cresce.
```

---

# 25. Questões ainda em aberto

- formato final do `KernelEnvelope`;
- quais estados mínimos serão persistidos na v0;
- se `CognitiveArtifact` será uma interface única ou família de interfaces;
- mecanismo físico de event log;
- persistência do lineage graph;
- política de idempotência;
- semântica final de `trust_state`;
- semântica final de `integrity_state`;
- formato do `VersionVector`;
- modelo de capability registry;
- orçamento padrão de processamento;
- replay determinístico entre versões;
- estratégia de snapshots;
- fronteira exata entre Kernel e Orchestrator;
- fronteira exata entre Kernel e Integrity & Resilience Plane.

Essas questões devem ser resolvidas por especificação + teste, sem expandir o Kernel por conveniência.

---

# 26. Frase-guia

> **O Cognitive Kernel não existe para pensar por toda a Eva. Existe para garantir que tudo o que pensa, deriva, aprende ou executa tenha identidade, limites, história e responsabilidade.**
