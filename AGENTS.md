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
7. `docs/blueprint/01_REGISTRO_DECISOES.md`
8. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
9. `docs/blueprint/15_ESCALA_EXPONENCIAL_E_ARQUITETURA_DE_PLATAFORMA.md`
10. `docs/blueprint/17_FOCO_MOTOR_EMPRESARIAL_E_ENGENHARIA_DE_ESCALA.md`
11. `docs/blueprint/18_LENTES_COGNITIVAS_E_ORQUESTRACAO.md`
12. `docs/blueprint/19_ARQUITETURA_360_ORBITAL_E_HIERARQUIA_DE_AGENTES.md`
13. `docs/blueprint/20_EXPLOSAO_ATOMICA_RECURSIVA_E_ESCALONAMENTO_DE_IA.md`
14. `docs/blueprint/21_QUARENTENA_COGNITIVA_PROMOCAO_E_RECUPERACAO.md`
15. `docs/blueprint/22_ORGANISMO_COGNITIVO_INTEGRIDADE_E_RESILIENCIA.md`
16. `docs/blueprint/23_POSICIONAMENTO_B2B_DORES_E_TESE_DE_VALOR.md`
17. documento específico da área em que será feita a alteração

## Autoridade arquitetural

O Blueprint vigente é a referência. Nenhum agente deve transformar preferência, conveniência momentânea, saída de modelo ou padrão local em decisão estrutural silenciosa.

## Foco vigente

O objeto principal é o **Eva Engine® como infraestrutura cognitiva generalista e potencial motor B2B enterprise**. Protótipos anteriores são laboratórios e evidência, não o limite conceitual do projeto.

A barra de engenharia é enterprise: auditabilidade, isolamento, custo, governança, resiliência, observabilidade, segurança, recuperação e prova econômica devem ser consideradas desde o Blueprint, mesmo quando a primeira implementação executável for pequena.

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

Em caso de erro promovido, preservar histórico e usar estados/relações como `revoked`, `superseded`, `invalidates`, `requires_recompute` quando apropriado.

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
- Learning Quarantine / Promotion Gate;
- Integrity & Resilience;
- taint propagation / blast radius;
- persistência;
- limites de expansão/recursão;
- API/SDK pública;
- dependência estrutural de fornecedor externo;
- Capability / Health / Schema / Lens Registries;
- Orchestration Model / Work Graph / budget / admission / stop policy;
- comportamento global aprendido;
- Evaluation Plane;
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
- fault injection para caminhos críticos quando aplicável.

## Regras finais

> Se uma decisão acelera o protótipo mas estreita o Core, isole-a no Domain Pack ou produto.

> Se algo parece mais inteligente mas não pode ser medido, rastreado e revertido, ainda não está pronto para promoção.

> **Aprendizado nasce em quarentena; confiança é conquistada por promoção.**

> **Falha conhecida é preferível a sucesso aparente com peça crítica ausente.**

> **A capability pode pedir para continuar; o Orchestrator decide se o organismo continua.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**
