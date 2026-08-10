# Eva Engine® — Quarentena Cognitiva, Promoção e Recuperação

**Status:** base arquitetural vigente, em evolução  
**Função:** formalizar o “segundo círculo” do Eva Engine®: um plano isolado onde derivados, hipóteses e candidatos de aprendizagem podem ser testados sem contaminar o núcleo confiável. Também define como detectar, conter e corrigir informação que tenha sido incorporada por engano.

---

# 1. A ideia central

O Eva Engine® pode evoluir continuamente, mas **não deve aprender diretamente dentro do mesmo espaço que executa conhecimento confiável**.

A arquitetura passa a distinguir dois círculos lógicos:

```text
╔══════════════════════════════════════════════════════════════════╗
║                 CÍRCULO 2 — LEARNING QUARANTINE                 ║
║                                                                  ║
║   derivados experimentais     candidatos de regra               ║
║   hipóteses                    candidatos de peso                ║
║   novas relações              rotas candidatas                  ║
║   heurísticas candidatas      lens stacks candidatos            ║
║   novas abstrações            padrões ainda não promovidos      ║
║                                                                  ║
║              NÃO ESCREVE DIRETAMENTE NO CORE                    ║
║                              │                                   ║
║                              ▼                                   ║
║                    ┌──────────────────┐                          ║
║                    │ PROMOTION GATE   │                          ║
║                    │ testes           │                          ║
║                    │ holdout          │                          ║
║                    │ challenger       │                          ║
║                    │ evaluator        │                          ║
║                    │ policy           │                          ║
║                    │ aprovação        │                          ║
║                    └────────┬─────────┘                          ║
╚═════════════════════════════╪════════════════════════════════════╝
                              │
                              │ artefato promovido e versionado
                              ▼
╔══════════════════════════════════════════════════════════════════╗
║                   CÍRCULO 1 — TRUSTED CORE                      ║
║                                                                  ║
║   regras promovidas          schemas vigentes                   ║
║   capacidades validadas      ontologia vigente                  ║
║   estado aprendido aceito    políticas vigentes                 ║
║   memória confiável          versões aprovadas                  ║
║                                                                  ║
║                 EXECUÇÃO DE PRODUÇÃO                             ║
╚══════════════════════════════════════════════════════════════════╝
```

Princípio:

> **O círculo de aprendizagem pode observar o Core, mas não deve possuir caminho de escrita direta para ele.**

A única passagem permitida é uma **promoção explícita, avaliada, versionada e reversível**.

---

# 2. Nome técnico

O segundo círculo será referido inicialmente como:

**Learning Quarantine Plane**  
**Plano de Quarentena de Aprendizado**

O mecanismo de passagem será:

**Promotion Gateway / Promotion Gate**

O primeiro círculo pode ser referido como:

**Trusted Execution Core**

Esses nomes descrevem funções reais e evitam depender de metáforas na implementação.

---

# 3. Por que essa separação é necessária

A Explosão Atômica Recursiva cria uma propriedade poderosa e perigosa:

```text
resultado
   ↓
derivado
   ↓
nova onda
   ↓
nova relação
   ↓
nova hipótese
   ↓
novo candidato de aprendizagem
```

Se qualquer derivado puder se tornar verdade imediatamente, um erro inicial pode produzir uma cascata de erros.

Riscos reais incluem:

- **feedback loop auto-confirmatório** — uma inferência passa a reforçar a si própria;
- **semantic drift** — o significado aprendido se desloca progressivamente;
- **derived-state contamination** — derivados incorretos contaminam novas decisões;
- **data/knowledge poisoning** — dados adversariais ou ruins induzem comportamento nocivo;
- **error propagation** — um erro ancestral se espalha por descendentes;
- **provenance loss** — perde-se a capacidade de saber de onde veio a conclusão;
- **overfitting local** — uma exceção local vira regra ampla;
- **premature promotion** — um padrão ainda fraco entra em produção cedo demais.

Portanto:

> **Aprender e executar não devem compartilhar a mesma superfície mutável.**

---

# 4. Isolamento forte

A separação entre os círculos deve ser arquitetural, não apenas uma convenção de equipe.

Direção desejada:

```text
TRUSTED CORE
    │
    │ eventos/snapshots permitidos
    ▼
LEARNING QUARANTINE

LEARNING QUARANTINE
    X───────────────► TRUSTED CORE
       escrita direta proibida
```

Na implementação madura, considerar:

- armazenamento separado para candidatos;
- credenciais diferentes;
- permissões de banco diferentes;
- ausência de tabela compartilhada gravável;
- APIs distintas;
- logs distintos;
- filas distintas quando necessário;
- namespaces/tenants de experimento;
- schemas de promoção explícitos;
- assinatura/hash de artefatos promovidos;
- deploy/versionamento separado do aprendizado bruto.

A primeira implementação pode ser modular no mesmo repositório/processo, mas a fronteira lógica deve existir desde o início.

---

# 5. O que pode entrar no círculo 2

O segundo círculo recebe **candidatos**, não verdades.

Exemplos:

```text
LearningCandidate
RuleCandidate
WeightCandidate
ThresholdCandidate
RelationCandidate
OntologyCandidate
AliasCandidate
RoutingCandidate
LensActivationCandidate
CapabilityCandidate
PatternCandidate
DomainKnowledgeCandidate
```

Cada candidato precisa carregar, quando aplicável:

```text
candidate_id
candidate_type
scope
source_event_ids
source_derivation_ids
origin_agent
origin_lens
origin_rule
created_at
engine_version
proposed_change
evidence_refs
support_count
counterevidence_refs
novelty_score
confidence_estimate
risk_class
privacy_class
expected_benefit
known_failure_modes
status
```

---

# 6. O Promotion Gate

Nada sai da quarentena apenas porque parece útil.

O fluxo de promoção deve poder crescer conforme o risco:

```text
CANDIDATO
    │
    ▼
VALIDAÇÃO ESTRUTURAL
    │
    ▼
PROVENANCE CHECK
    │
    ▼
DEDUP / CONFLITOS
    │
    ▼
TESTES UNITÁRIOS / GOLDEN
    │
    ▼
HOLDOUT
    │
    ▼
RED TEAM / CHALLENGER
    │
    ▼
EVALUATOR
    │
    ▼
BASELINE COMPARISON
    │
    ▼
RISK / POLICY GATE
    │
    ├──────────────► REJEITAR
    │
    ├──────────────► MANTER EM QUARENTENA
    │
    └──────────────► PROMOVER
                         │
                         ▼
                  NOVA VERSÃO DO CORE
```

Quanto maior o alcance da mudança, maior a exigência de promoção.

---

# 7. Promoção não é mutação silenciosa

Uma mudança promovida deve gerar uma nova versão ou artefato identificável.

Exemplo conceitual:

```text
rulepack 1.7.2
     +
Candidate C-908 aprovado
     ↓
rulepack 1.8.0
```

ou:

```text
ontology 0.4.1
     +
novo relation type aprovado
     ↓
ontology 0.5.0
```

Princípio:

> **O Core não “muda de ideia” silenciosamente. O Core muda de versão.**

Isso permite:

- reproduzir resultado antigo;
- comparar versões;
- canary deployment;
- rollback;
- auditoria;
- atribuição causal de regressões.

---

# 8. E se o Core já engoliu algo errado?

Essa é uma capacidade obrigatória.

O sistema não pode depender da fantasia de que erros nunca serão promovidos.

Precisamos de **Correction & Recovery Protocol**.

Quando uma informação promovida for considerada incorreta:

```text
ERRO DETECTADO
    │
    ▼
IDENTIFICAR ARTEFATO / DERIVADO RAIZ
    │
    ▼
MARCAR COMO REVOKED / SUPERSEDED
    │
    ▼
PERCORRER LINEAGE DOS DESCENDENTES
    │
    ▼
CALCULAR BLAST RADIUS
    │
    ▼
MARCAR DERIVADOS DEPENDENTES
    │
    ├── stale
    ├── tainted
    ├── invalid
    └── requires_recompute
    │
    ▼
REPROCESSAR SOB VERSÃO CORRIGIDA
    │
    ▼
COMPARAR RESULTADOS
    │
    ▼
PROMOVER CORREÇÃO / ROLLBACK
```

Termo importante:

**Blast Radius** = extensão da contaminação causada por um erro.

Em um motor recursivo, saber o blast radius é tão importante quanto saber que ocorreu um erro.

---

# 9. Não apagar a história

Correção não deve significar destruir o rastro.

Preferir relações como:

```text
supersedes
revokes
invalidates
corrects
derived_from
recomputed_from
```

Exemplo:

```text
Inference I-42
status = revoked
reason = source_relation_invalid
superseded_by = I-87
```

Assim o sistema sabe:

- o que acreditou antes;
- por que acreditou;
- quando descobriu o erro;
- o que substituiu aquela interpretação.

Isso é essencial para auditoria empresarial.

---

# 10. Shadow Mode antes de promoção

Para mudanças importantes, uma capacidade candidata pode operar em **shadow mode**.

Ela processa eventos reais, mas não influencia a resposta oficial.

```text
EVENTO REAL
    │
    ├──────────────► CORE VIGENTE ───► RESULTADO OFICIAL
    │
    └──────────────► CANDIDATO SHADOW ─► RESULTADO SOMBRA
                                      │
                                      ▼
                                comparação
```

Isso permite medir:

- ganho;
- regressões;
- falsos positivos;
- falsos negativos;
- custo;
- latência;
- divergência por domínio;
- comportamento em casos raros.

Sem colocar a operação em risco.

---

# 11. Canary Promotion

Depois de shadow mode, mudanças de risco suficiente podem entrar em **canary**:

```text
1% do tráfego / tenants autorizados
        ↓
5%
        ↓
20%
        ↓
50%
        ↓
100%
```

A progressão depende de métricas e políticas.

Em determinados domínios, promoção pode exigir aprovação humana em cada etapa.

---

# 12. Hierarquia de supervisores no segundo círculo

O segundo círculo não é apenas um banco de candidatos.

Ele pode conter “ajudantes” especializados:

```text
┌─────────────────────────────────────────────────────────────┐
│                LEARNING QUARANTINE PLANE                    │
│                                                             │
│  Provenance Guard        verifica origem                    │
│  Poisoning Detector      busca manipulação/contaminação     │
│  Dedup Guard             evita aprender duplicata           │
│  Contradiction Agent     procura evidência contrária        │
│  Drift Monitor           detecta mudança semântica          │
│  Scope Guard             impede promoção local→global       │
│  Privacy Guard           controla dados permitidos          │
│  Evaluator               mede qualidade                     │
│  Cost Evaluator          mede custo marginal                │
│  Challenger              tenta derrubar hipótese            │
│  Promotion Controller    governa avanço                     │
│  Rollback Controller     desfaz versão problemática         │
└─────────────────────────────────────────────────────────────┘
```

Esses componentes podem ser determinísticos, estatísticos, algorítmicos, modelos locais ou IA supervisora, conforme necessidade.

---

# 13. Escalonamento de IA no segundo círculo

A quarentena é um dos melhores lugares para usar IA mais poderosa quando ela realmente acrescentar valor, porque:

- ela não altera produção diretamente;
- pode revisar candidatos complexos;
- pode procurar contradições;
- pode sintetizar evidência;
- pode propor testes;
- pode comparar hipóteses;
- pode supervisionar agentes menores.

Direção:

```text
mecânica / regras
      ↓ se insuficiente
estatística / algoritmos
      ↓ se insuficiente
modelos locais / especialistas
      ↓ se insuficiente
IA supervisora
      ↓
promoção ainda exige evaluator/policy
```

IA cara não é proibida. Ela é **escalonada para onde o valor e o risco justificam**.

---

# 14. Grandes corporações como horizonte arquitetural

**DIREÇÃO ESTRATÉGICA**

O Eva Engine® deve ser concebido para que, após validação adequada, possa atuar em ambientes onde organizações já gastam volumes relevantes com IA, investigação, análise, suporte, operações e automação.

A proposta de valor futura pode vir de uma combinação de:

- reduzir chamadas desnecessárias a modelos caros;
- usar mecanismos determinísticos onde oferecem maior precisão;
- manter IA potente em pontos de supervisão e ambiguidade real;
- reaproveitar memória e estrutura aprendida;
- diminuir retrabalho cognitivo;
- detectar padrões operacionais de alto valor;
- produzir explicabilidade e lineage que soluções puramente generativas nem sempre oferecem.

Nenhuma alegação econômica é presumida no Blueprint.

O objetivo arquitetural é **ser capaz de testar essas hipóteses seriamente em escala empresarial**.

---

# 15. “Validação total” como meta operacional

Em engenharia não existe garantia absoluta de ausência de falhas.

A expressão “não vai ao mercado sem validação total” será interpretada neste Blueprint como:

> **nenhuma capacidade crítica é promovida sem cumprir os gates de evidência, segurança, regressão, escala, domínio e operação definidos para seu nível de risco.**

Para capacidades empresariais críticas, isso poderá exigir:

```text
unit tests
golden tests
holdout
red team
adversarial tests
scale tests
fault injection
shadow mode
canary
rollback drill
security review
privacy review
human approval
operational SLOs
economic pilot
```

A barra de validação cresce com o impacto da capacidade.

---

# 16. Invariante de segurança cognitiva

**DECISÃO APROVADA**

> **Nenhum candidato de aprendizagem pode escrever diretamente no Trusted Core.**

> **Toda promoção precisa ser rastreável a evidência, versão e processo de avaliação.**

> **Toda capacidade promovida relevante precisa ter caminho de correção, revogação ou rollback.**

> **Todo derivado recursivo precisa preservar lineage suficiente para calcular sua origem e seu blast radius.**

---

# 17. Visão consolidada dos dois círculos

```text
                 ┌──────────────────────────────────┐
                 │      SUPERVISORY / EVAL LAYER    │
                 │  agentes · IA · humans · policy  │
                 └────────────────┬─────────────────┘
                                  │
        ╔═════════════════════════▼══════════════════════════╗
        ║        CÍRCULO 2 — LEARNING QUARANTINE            ║
        ║                                                    ║
        ║  candidates   experiments   shadow   challenger    ║
        ║  drift        poisoning     eval     red team      ║
        ║                                                    ║
        ║             ┌──────────────────┐                   ║
        ║             │  PROMOTION GATE  │                   ║
        ║             └────────┬─────────┘                   ║
        ╚══════════════════════╪═════════════════════════════╝
                               │ somente promoção aprovada
                               ▼
        ╔════════════════════════════════════════════════════╗
        ║          CÍRCULO 1 — TRUSTED EXECUTION CORE       ║
        ║                                                    ║
        ║   validated rules · schemas · memory · policies    ║
        ║   promoted learned state · capabilities            ║
        ║                                                    ║
        ║              EVA CORE 360®                         ║
        ╚════════════════════════════════════════════════════╝
```

---

# 18. Frases-guia

> **O motor pode aprender sem ter permissão para acreditar imediatamente no que aprendeu.**

> **Aprendizado nasce em quarentena; confiança é conquistada por promoção.**

> **O erro não deve ser impossível de acontecer. Deve ser possível de localizar, conter, corrigir e reprocessar.**

> **O Core executa o que foi promovido. O segundo círculo questiona o que ainda merece ser promovido.**
