# AGENTS.md — Regras para agentes do Eva Engine®

Este arquivo deve ser lido por qualquer agente de código, Cursor, assistente ou colaborador antes de alterar arquitetura ou implementação.

## Leitura obrigatória

Antes de trabalhar:

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
12. documento específico da área em que será feita a alteração

## Autoridade arquitetural

O Blueprint vigente é a referência. Nenhum agente deve transformar preferência, conveniência momentânea, saída de modelo ou padrão local em decisão estrutural silenciosa.

## Foco vigente

O objeto principal é o **Eva Engine® como infraestrutura cognitiva generalista e potencial motor B2B enterprise**. Protótipos anteriores são laboratórios e evidência, não o limite conceitual do projeto.

A barra de engenharia é enterprise: auditabilidade, isolamento, custo, governança, resiliência, observabilidade, segurança, recuperação e prova econômica devem ser considerados desde o Blueprint, mesmo quando a primeira implementação executável for pequena.

## Regras não negociáveis da base atual

1. O Eva Engine® é generalista; produtos são consumidores.
2. Produtos dependem do Core; o Core não depende de produtos.
3. Conteúdo original nunca é sobrescrito pela interpretação.
4. RAW, DERIVED, INFERRED e LEARNED permanecem conceitualmente separados.
5. Inferências possuem confiança, evidência e rastreabilidade adequadas ao risco.
6. Correções são reversíveis e não apagam histórico relevante.
7. Aprendizado individual não altera automaticamente conhecimento global.
8. O motor nasce multilíngue por arquitetura.
9. O sistema é orientado a eventos.
10. Expansão e Explosão Atômica possuem limites explícitos de profundidade, custo, risco, novidade e parada.
11. O Core não depende de grafo visual.
12. O Core não fica acoplado a fornecedor específico de IA, embeddings ou nuvem.
13. Começar como monólito modular; microserviços somente quando justificados.
14. Mudança de comportamento relevante exige teste.
15. Mudança estrutural exige atualização documental.
16. A implementação inicial pode ser pequena; a arquitetura não deve ser estreita.
17. Crescimento ocorre prioritariamente por composição, registries, schemas, Domain Packs, lenses e capabilities.
18. Aprendizado contínuo não significa auto-modificação irrestrita.
19. Mudanças globais aprendidas exigem avaliação, versionamento, promoção e rollback.
20. Evaluators e baselines são obrigatórios para afirmar melhoria cognitiva.
21. O Core não impõe profundidade fixa de hierarquia de produto.
22. Capacidades devem ser descobríveis/versionáveis quando o Capability Registry existir.
23. Resultado de protótipo é evidência, não arquitetura-alvo automática.
24. Termos como aprendizado, confiança, inteligência, escala e economia exigem definição operacional testável.
25. Escala operacional, cognitiva e de domínio são problemas distintos.
26. Informação da fase privada de P&D não deve ser publicada ou enviada para fora do contexto autorizado sem decisão explícita.
27. **Learning Candidates, derivados experimentais e heurísticas candidatas não podem escrever diretamente no Trusted Core.**
28. **Toda promoção do Learning Quarantine para o Trusted Core precisa passar por Promotion Gate rastreável e versionado.**
29. **Toda capacidade promovida relevante precisa ter caminho de revogação, correção ou rollback.**
30. **Derivados recursivos precisam preservar lineage suficiente para localizar ancestralidade e calcular blast radius de um erro.**
31. IA supervisora é permitida e esperada quando agrega valor; não deve ser chamada onde um mecanismo mais simples resolve com qualidade equivalente ou superior.
32. **Átomos e derivados relevantes devem circular com Atomic/Cognitive Envelope suficiente para provenance, scope, lineage, integrity e policy.**
33. **Integrity & Resilience Plane deve detectar degradação, anomalia, ausência de capability crítica e risco de propagação antes que falhas silenciosas contaminem o resultado.**
34. **Falha conhecida é preferível a sucesso aparente produzido com uma peça crítica ausente.**
35. Auto-recuperação só pode alterar automaticamente estados e componentes cuja recuperação seja segura, idempotente ou explicitamente testada.
36. **B2B enterprise é o horizonte estratégico vigente; o motor deve medir custo, escalonamento para IA/humano e impacto operacional desde que aplicável.**
37. Nenhuma alegação de economia, ROI ou superioridade empresarial pode ser feita sem baseline e nível de evidência correspondente.
38. A tese econômica é usar o mecanismo mais barato/previsível que satisfaça o requisito e escalar para IA potente quando houver ganho mensurável — não eliminar IA por princípio.

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

## Aprendizado contínuo

A arquitetura distingue pelo menos:

```text
L1 — sessão/contexto
L2 — individual/tenant/organização
L3 — domínio
L4 — global
```

Quanto maior o alcance da mudança, maior a exigência de evidência, holdout, evaluator, baseline, aprovação, versionamento, monitoramento e rollback.

Um agente nunca deve promover automaticamente padrão local para conhecimento global.

## Learning Quarantine

Candidatos de aprendizagem podem ser produzidos pelo processamento, mas permanecem fora do Trusted Core até promoção.

Preferir fronteira forte:

```text
TRUSTED CORE ──eventos/snapshots permitidos──► LEARNING QUARANTINE

LEARNING QUARANTINE ──X──► escrita direta no TRUSTED CORE

LEARNING QUARANTINE ──Promotion Gate──► nova versão promovida
```

Em caso de erro promovido, preservar histórico e usar relações/estados como `revoked`, `superseded`, `invalidates`, `requires_recompute` quando apropriado. Não apagar a origem se ela for necessária para auditoria.

## Integridade e resiliência

O Integrity & Resilience Plane deve ser tratado como responsabilidade transversal.

Preferir fluxo:

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

Não “destruir” conteúdo original como resposta padrão a uma interpretação ruim. Preservar provenance e auditabilidade.

## Política de mudanças

Registrar antes de alterar:

- entidades fundamentais;
- ontologia e relações;
- formato de eventos;
- Atomic/Cognitive Envelope;
- trust tiers / integrity states;
- separação de memória;
- Evidence Model;
- confiança/calibração;
- política de aprendizagem;
- Learning Quarantine e Promotion Gate;
- Integrity & Resilience Plane;
- taint propagation / blast radius;
- persistência;
- limites da expansão/recursão;
- API/SDK pública;
- dependência estrutural de fornecedor externo;
- Capability Registry / Health Registry / Schema Registry / Lens Registry;
- comportamento global aprendido;
- Evaluation Plane;
- políticas de escala, custo e orçamento cognitivo;
- definição de métricas B2B usadas para alegar valor.

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
- health signals para capabilities críticas;
- observabilidade de fallback, escalonamento e custo;
- fault injection para caminhos críticos quando aplicável.

## Linguagem e nomenclatura

Identificadores internos universais devem ser neutros de idioma, por exemplo:

```text
ATOM_DECISION
REL_CONTINUES
CAP_ATOMIZATION
LEARNING_CANDIDATE
PROMOTION_GATE
INTEGRITY_STATE
ATOMIC_ENVELOPE
```

## Regras finais

> Se uma decisão acelera o protótipo mas estreita o Core, isole-a no Domain Pack ou produto.

> Se algo parece mais inteligente mas não pode ser medido, rastreado e revertido, ainda não está pronto para promoção.

> **Aprendizado nasce em quarentena; confiança é conquistada por promoção.**

> **Falha conhecida é preferível a sucesso aparente com peça crítica ausente.**

> **A ambição define o espaço arquitetural. O teste define o que podemos afirmar.**
