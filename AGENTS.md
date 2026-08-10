# AGENTS.md — Regras para agentes do Eva Engine®

Este arquivo deve ser lido por qualquer agente de código, Cursor, assistente ou colaborador antes de alterar arquitetura ou implementação.

## Leitura obrigatória

Antes de trabalhar:

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
25. documento específico da área em que será feita a alteração

## Autoridade arquitetural

O Blueprint vigente é a referência. Nenhum agente deve transformar preferência, conveniência momentânea, saída de modelo ou padrão local em decisão estrutural silenciosa.

## Foco vigente

O objeto principal é o **Eva Engine® como infraestrutura cognitiva generalista e potencial motor B2B enterprise**. Protótipos anteriores são laboratórios e evidência, não o limite conceitual do projeto.

A barra de engenharia é enterprise: auditabilidade, isolamento, custo, governança, resiliência, observabilidade, segurança, recuperação e prova econômica devem ser consideradas desde o Blueprint, mesmo quando a primeira implementação executável for pequena.

O projeto possui agora uma especificação de heartbeat executável em `36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md`. Implementação deve seguir essa spec por fatias pequenas, sem reconstruir arquitetura no Cursor.

## Regras não negociáveis da base atual

1. O Eva Engine® é generalista; produtos são consumidores.
2. Produtos dependem do Core; o Core não depende de produtos.
3. Conteúdo original nunca é sobrescrito pela interpretação.
4. RAW, DERIVED, INFERRED e LEARNED permanecem separados.
5. Signal, Evidence, Claim/Hypothesis, Score, Confidence e Decision não são sinônimos.
6. Score não vira confidence sem calibração apropriada.
7. Repetição/derivação da mesma ancestralidade não cria evidência independente automaticamente.
8. Correções são reversíveis e não apagam histórico necessário.
9. Aprendizado individual/tenant não altera automaticamente conhecimento global.
10. O motor nasce multilíngue por arquitetura.
11. O sistema é orientado a eventos.
12. Explosão Atômica Recursiva possui limites de profundidade, waves, fan-out, custo, tempo, risco, novidade e parada.
13. O Core não depende de UI, grafo visual, fornecedor específico de IA, embeddings ou nuvem.
14. Começar como monólito modular; microserviços somente quando justificados.
15. Mudança de comportamento relevante exige teste.
16. Mudança estrutural exige atualização documental.
17. A implementação inicial pode ser pequena; a arquitetura não deve ser estreita.
18. Crescimento ocorre por composição, registries, schemas, Domain Packs, lenses e capabilities.
19. Aprendizado contínuo não significa auto-modificação irrestrita.
20. Mudanças globais aprendidas exigem avaliação, versionamento, promoção e rollback.
21. Evaluators e baselines são obrigatórios para afirmar melhoria cognitiva.
22. O Core não impõe profundidade fixa de hierarquia de produto.
23. Informação da fase privada de P&D não deve ser publicada ou enviada para fora do contexto autorizado sem decisão explícita.
24. Learning Candidates, derivados experimentais e heurísticas candidatas não escrevem diretamente no Trusted Core.
25. Toda promoção do Learning Quarantine para o Trusted Core passa por Promotion Gate rastreável e versionado.
26. Toda capacidade promovida relevante possui caminho de revogação, correção ou rollback.
27. Derivados recursivos preservam lineage suficiente para ancestralidade, independência de evidência e blast radius.
28. Átomos e derivados relevantes circulam com Atomic/Cognitive Envelope suficiente para provenance, scope, lineage, integrity, version e policy.
29. Integrity & Resilience deve detectar degradação, anomalia, ausência de capability crítica e risco de propagação.
30. Falha conhecida é preferível a sucesso aparente produzido com peça crítica ausente.
31. Auto-recuperação automática só atua em estados/componentes cuja recuperação seja segura, idempotente ou explicitamente testada.
32. B2B enterprise é o horizonte estratégico vigente; custo, escalonamento para IA/humano e impacto operacional devem ser medidos quando aplicável.
33. Nenhuma alegação de economia, ROI ou superioridade empresarial sem baseline e nível de evidência correspondente.
34. A tese econômica é usar o mecanismo mais barato/previsível que satisfaça o requisito e escalar quando houver ganho mensurável — não eliminar IA por princípio.
35. Capability é contrato; agente/modelo/função é executor.
36. Health de capability pode ser técnico, cognitivo e econômico.
37. O Orchestrator seleciona por requisito, schema, policy, scope, health, risco, custo, latência e evidência — não por familiaridade com implementações.
38. Control Plane e Execution Plane permanecem conceitualmente separados.
39. Capability não pode criar recursão ilimitada diretamente; ela propõe `NextStepCandidate`.
40. Toda nova onda passa por Admission Control, budget e policy.
41. Hard constraints filtram antes de ranking de candidatos.
42. Fallback, retry, parallelism, replanning e escalation são decisões explícitas e rastreáveis.
43. Delegar um subplan não delega autoridade ilimitada; scope, budget, risk limit, fan-out e deadline acompanham a delegação.
44. Alto risco pode exigir IA/humano diretamente; deterministic-first não é dogma.
45. IA supervisora é capability governada; sua saída continua Artifact/Evidence Candidate.
46. O Orchestrator também possui health, métricas e precisa ser observável.
47. Políticas de roteamento aprendidas entram em Learning Quarantine antes de promoção.
48. O estado durável de planos/traces não deve depender da memória de um único processo.
49. Envelope e Payload são responsabilidades distintas; metadados pesados podem ficar por referência para controlar overhead.
50. Controlled Unlearning precisa retirar autoridade de aprendizado errado sem apagar o histórico auditável.
51. Promoção gera manifesto/versão; Trusted Core não sofre mutação silenciosa.
52. Sistemas enterprise atravessam Enterprise Integration Boundary/Anti-Corruption Layer; não acessam Kernel diretamente.
53. Tenant/scope é resolvido antes de admissão; não usar `default tenant` silencioso.
54. Autenticidade da fonte não significa verdade; output de modelo também não ganha autoridade automática.
55. Ações externas passam por `ActionRequest` + Policy/Permission + adapter autorizado.
56. Threat Model inclui integridade cognitiva: evidence, learning, promotion, routing e cost amplification são superfícies de segurança.
57. O primeiro heartbeat executável não depende de LLM/embeddings/UI; prova evento → envelope → registry → orchestration → capability determinística → artifact/evidence/trace → result.
58. Antes de banco/API, contratos centrais devem ser testáveis com implementações in-memory e fixtures determinísticos.
59. O primeiro heartbeat prova invariantes e failure containment antes de sofisticação cognitiva.

## Processo de implementação

```text
IDEIA / HIPÓTESE
  ↓
DEFINIÇÃO OPERACIONAL
  ↓
CASOS DE TESTE
  ↓
BASELINE
  ↓
IMPLEMENTAÇÃO
  ↓
TESTE ISOLADO
  ↓
TESTE DE COMPOSIÇÃO
  ↓
TESTE DE ESCALA
  ↓
RED TEAM / HOLDOUT
  ↓
FAULT INJECTION quando aplicável
  ↓
SHADOW MODE quando aplicável
  ↓
AVALIAÇÃO CONTRA BASELINE
  ↓
QUARANTINE / PROMOTION GATE
  ↓
CANARY quando aplicável
  ↓
PROMOÇÃO / REJEIÇÃO / ROLLBACK
```

Não inverter para “gerar código e depois descobrir qual era a regra”.

## Escada de evidência

```text
E0 — ideia
E1 — prova de mecanismo
E2 — bateria reproduzível
E3 — escala sintética
E4 — piloto de domínio
E5 — prova operacional
E6 — prova econômica
```

Uma bateria local positiva não autoriza alegação E5/E6.

## Orchestration guardrails

Preferir o fluxo:

```text
TaskRequirement
      ↓
Capability Registry Query
      ↓
Policy / Scope / Schema / Health Filter
      ↓
Admission Control
      ↓
OrchestrationPlan / Work Graph
      ↓
Budget Allocation
      ↓
Execution Plane
      ↓
Artifacts / Evidence / Metrics
      ↓
Stop / Replan / Escalate / Next Wave
```

Nunca permitir como padrão:

```text
CAP_A → chama CAP_B → chama CAP_C → ... sem controle
```

Preferir:

```text
CAP_A
  ↓
NextStepCandidate
  ↓
ORCHESTRATOR
  ↓ policy + budget + admission
  ↓
CAP_B autorizado
```

Stop reasons, budget consumption, fallbacks, retries, circuit breakers, escalations e replans relevantes precisam aparecer no trace.

## Learning Quarantine

```text
TRUSTED CORE ──eventos/snapshots permitidos──► LEARNING QUARANTINE

LEARNING QUARANTINE ──X──► escrita direta no TRUSTED CORE

LEARNING QUARANTINE ──Promotion Gate──► nova versão promovida
```

Em caso de erro promovido, preservar histórico e usar estados/relações como `revoked`, `superseded`, `invalidates`, `requires_recompute` quando apropriado. Quando necessário, executar Controlled Unlearning por lineage/checkpoint/replay.

## Integridade e resiliência

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

Não “destruir” conteúdo original como resposta padrão a interpretação ruim.

## Primeira implementação executável

Seguir `36_EXECUTABLE_ARCHITECTURE_SPEC_V0_1.md`.

Primeira fatia no Cursor:

```text
packages/contracts
packages/schemas
packages/envelope
```

Primeiro critério:

```text
tests pass
typecheck pass
invalid envelope fails
valid fixture round-trips without mutation
no DB
no HTTP
no LLM
no domain code
```

## Política de mudanças

Registrar antes de alterar:

- entidades fundamentais;
- ontologia e relações;
- formato de eventos;
- Cognitive Kernel;
- Atomic/Cognitive Envelope;
- trust/integrity states;
- Evidence Model;
- confiança/calibração;
- política de aprendizagem;
- Learning Quarantine / Promotion / Unlearning;
- Integrity & Resilience;
- taint propagation / blast radius;
- Enterprise Integration Boundary;
- tenant/scope model;
- persistência;
- limites de expansão/recursão;
- API/SDK pública;
- dependência estrutural de fornecedor externo;
- Capability / Health / Schema / Lens Registries;
- Orchestration Model / Work Graph / budget / admission / stop policy;
- comportamento global aprendido;
- Evaluation Plane;
- Threat Model;
- políticas de escala, custo e orçamento cognitivo;
- métricas B2B usadas para alegar valor.

## Qualidade mínima

Buscar:

- tipos explícitos;
- contratos pequenos;
- módulos coesos;
- baixo acoplamento;
- logs estruturados;
- testes de regressão;
- versionamento de regras;
- métricas de latência, custo e qualidade;
- schemas/migrações não destrutivas quando possível;
- lineage suficiente para explicar resultados e propagar correções;
- health signals para capabilities e Orchestrator;
- observabilidade de fallback, escalation, stop reasons e custo;
- fault injection para caminhos críticos quando aplicável;
- tenant/scope enforcement fora de prompts/modelos;
- nenhuma credencial/secret no repositório.

## Regras finais

> Se uma decisão acelera o protótipo mas estreita o Core, isole-a no Domain Pack ou produto.

> Se algo parece mais inteligente mas não pode ser medido, rastreado e revertido, ainda não está pronto para promoção.

> **Aprendizado nasce em quarentena; confiança é conquistada por promoção.**

> **Falha conhecida é preferível a sucesso aparente com peça crítica ausente.**

> **A capability pode pedir para continuar; o Orchestrator decide se o organismo continua.**

> **O primeiro coração não precisa pensar muito. Precisa bater certo.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**
