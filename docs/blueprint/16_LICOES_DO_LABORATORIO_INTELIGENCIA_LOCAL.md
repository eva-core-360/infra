# Eva Engine® — Lições do Laboratório de Inteligência Local

**Status:** evidência histórica incorporada ao Blueprint; não promove automaticamente decisões de arquitetura.  
**Origem:** bateria experimental anterior construída sobre o produto de anotações Eva Memory / Note Pulse.  
**Objetivo:** preservar achados medidos que devem informar o novo Eva Engine® generalista, sem confundir limitações daquele protótipo com limites do novo Core.

---

# 1. Por que este laboratório importa agora

O laboratório foi criado quando a investigação ainda estava concentrada no produto de anotações, mas sua metodologia e seus resultados contêm evidências diretamente úteis para o Eva Engine®.

Ele demonstra, com medições, três fatos importantes:

1. mecanismos determinísticos simples podem produzir experiências percebidas como inteligentes;
2. heurísticas mal calibradas podem parecer sofisticadas e ainda assim piorar o resultado;
3. adaptação estatística a dados novos não é, por si só, aprendizado contínuo.

Esses três achados reforçam a direção atual do Eva Engine®: combinar determinismo, heurística e predição sob governança, avaliação e rastreabilidade.

---

# 2. Escopo e rigor da bateria

A rodada executou 508 cenários sobre um corpus sintético congelado de 138 notas, incluindo busca, associações, classificação em áreas, retomada, composição de heurísticas, escala, sistemas de escrita, red team e teste cego.

Controles relevantes usados no laboratório:

- corpus congelado com hash antes da execução;
- ground truth separado da entrada dos motores;
- barreira anti-vazamento dos campos de expectativa;
- oráculo independente para parte da avaliação;
- split exploração/holdout;
- contraexemplos e red team;
- medição de silêncio como comportamento correto;
- custo e escala medidos junto com qualidade;
- bloqueio explícito de rede;
- resultados brutos preservados para auditoria.

Limites conhecidos:

- corpus sintético;
- um único anotador;
- benchmark sem estudo com usuários;
- tempos medidos em Node/Linux, não em dispositivos móveis;
- algumas expectativas do próprio benchmark foram posteriormente marcadas como questionáveis.

Portanto, os números servem como diagnóstico de algoritmo e desenho experimental, não como prova de satisfação de usuário ou prontidão comercial.

---

# 3. Achado 1 — continuidade determinística funciona muito bem

A parte mais sólida da arquitetura anterior foi a inteligência de continuidade: lembrar, localizar e restaurar contexto.

Resultados observados incluíram:

- retomada tecnicamente correta em 30/30 casos;
- busca com recall aproximado de 0,939;
- top-1 aproximado de 0,886;
- top-3 aproximado de 0,955;
- silêncio correto em 8/8 consultas que deveriam retornar vazias;
- zero vazamento de lixeira;
- zero chamadas de rede durante os testes.

Lição arquitetural:

> Guardar e restaurar contexto confiável pode gerar mais valor percebido do que tentar inferir significado complexo cedo demais.

Para o novo Eva Engine®, isso sugere que memória, estado, eventos, histórico, recuperação e rastreabilidade devem ser capacidades de primeira classe do Cognitive Kernel.

---

# 4. Achado 2 — interpretação heurística pode falhar com confiança

Os componentes mais frágeis foram justamente os que tentavam “interpretar” significado por mecanismos simples.

Exemplos observados:

- classificação por léxico errou textos figurados com confiança máxima;
- confiança existente media densidade de palavras-chave, não probabilidade calibrada de acerto;
- empate entre áreas podia ser resolvido pela ordem de declaração do léxico;
- normalização de acentos era inconsistente;
- associações por PMI eram dominadas por duplicatas e raridade;
- expansão semântica por coocorrência produziu 0 ganhos e 11 ruídos em 46 consultas;
- com crescimento do acervo, algumas relações pioravam em vez de melhorar.

Lição arquitetural:

> Confidence precisa ser calibrada contra acerto real. Um número chamado de “confiança” sem calibração é apenas um score.

Consequência para o Eva Engine®:

- separar `score` de `confidence`;
- exigir evaluators de calibração;
- rastrear evidências usadas em cada inferência;
- permitir silêncio/abstenção;
- preferir múltiplas hipóteses a uma falsa certeza quando houver ambiguidade.

---

# 5. Achado 3 — pistas explicáveis funcionam melhor que conclusões opacas

O laboratório encontrou um padrão importante:

> A composição de heurísticas ajudava quando entregava pistas verificáveis; quando entregava conclusões confiantes, podia amplificar erro.

Exemplo de pista:

`Estas duas memórias se relacionam porque compartilham reunião, escopo e cliente.`

O usuário consegue entender o critério e rejeitar a relação se ela não fizer sentido.

Exemplo de conclusão perigosa:

`Esta informação pertence a Finanças — confiança 1,00.`

Se o critério estiver errado e oculto, o erro é incorporado ao sistema como se fosse fato.

Implicação proposta para o Eva Engine®:

- heurísticas de baixa ou média confiança devem produzir candidatos, pistas e relações explicáveis;
- conclusões automáticas exigem um patamar de evidência mais alto;
- `INFERRED` nunca deve ser promovido silenciosamente a `RAW` ou `DERIVED`;
- explicabilidade deve mostrar evidência real, não uma narrativa inventada depois do resultado.

---

# 6. Achado 4 — adaptação estatística não é aprendizado

O motor de associações do protótipo recalculava coocorrências quando o acervo mudava. O laboratório demonstrou que isso não constituía aprendizado contínuo.

Faltavam elementos como:

- parâmetro ajustável;
- objetivo ou função de perda;
- feedback do comportamento;
- comparação com baseline;
- promoção de uma nova versão;
- avaliação de melhora;
- rollback.

Em alguns testes de escala, a qualidade das relações chegou a degradar.

Essa evidência reforça a arquitetura atual do Learning Plane:

```text
uso
 → sinal
 → feedback
 → candidato de aprendizagem
 → avaliação
 → comparação com baseline
 → promoção ou rejeição
 → versionamento
 → monitoramento
 → rollback
```

Princípio:

> O motor só deve dizer que “aprendeu” quando existe mudança mensurável de comportamento ou parâmetro produzida por evidência e validada por avaliação.

---

# 7. Achado 5 — escala de dados e escala de capacidade são problemas diferentes

O laboratório mostrou crescimento linear e barato em várias estruturas, mas também demonstrou que qualidade semântica pode degradar com corpus maior.

Isso reforça a definição atual de crescimento exponencial do Eva Engine®:

> crescimento de capacidade por composição, não crescimento descontrolado de busca, relações ou custo.

O novo motor deve possuir orçamentos explícitos para recuperação e expansão:

- `max_candidates`;
- `max_depth`;
- `max_relations`;
- `minimum_confidence`;
- `time_budget`;
- `cost_budget`;
- `memory_scope`;
- `privacy_scope`.

---

# 8. Achado 6 — arquitetura multilíngue deve separar lógica de dados linguísticos

A bateria mostrou que grande parte da arquitetura de busca, ranking, retomada e relações era agnóstica ao idioma, enquanto léxicos e normalização eram fortemente dependentes da língua.

Isso reforça a decisão atual:

```text
Core semântico neutro
        +
Language Packs versionados
```

A falha do protótipo em acentos e sistemas de escrita não é argumento para abandonar o desenho multilíngue; é evidência de que normalização, tokenização, morfologia e locale packs precisam ser capacidades testadas formalmente.

---

# 9. O que NÃO deve ser copiado para o novo Core

O laboratório é evidência; o protótipo não é a arquitetura-alvo.

Não transportar automaticamente para o Eva Core:

- as 10 áreas de vida usadas naquele corpus;
- a entidade `note` como objeto universal;
- léxicos fixos como mecanismo principal de interpretação;
- PMI de documento inteiro como motor universal de relações;
- a antiga fórmula de confiança;
- conclusões específicas sobre não perseguir aprendizado adaptativo.

A última conclusão era coerente com as restrições daquele produto e daquela fase. A direção atual do Eva Engine® mudou: aprendizado contínuo supervisionado passa a ser objetivo arquitetural, com governança, isolamento e avaliação.

---

# 10. O que DEVE ser reaproveitado

O maior patrimônio desta bateria é o método.

O Eva Engine® deve herdar e ampliar:

- corpus congelado;
- hash e versionamento de datasets;
- holdout;
- red team;
- ground truth independente;
- anti-vazamento entre expectativa e inferência;
- silêncio/abstenção como métrica positiva;
- avaliação de alta confiança + erro;
- teste de escala;
- custo junto com qualidade;
- resultado bruto auditável;
- teste cego/revisão externa;
- regressão entre versões;
- classificação explícita entre métrica, julgamento e interpretação.

Isso deve evoluir para o **Evaluation Plane** do Eva Engine®.

---

# 11. Relação com o Cognitive Kernel

O laboratório sugere que o Kernel deve ser menor e mais rigoroso do que o antigo “motor de notas”.

Capacidades candidatas ao Kernel ou aos planos fundamentais:

```text
Event
Memory
State
Time
Entity
Atom
Relation
Context
Evidence
Inference
Confidence
Feedback
Version
Policy
Capability
Schema
```

Capacidades de produto como “área da vida”, “retomada de nota” ou “mapa” devem permanecer em Domain Packs ou produtos consumidores.

---

# 12. Conclusão estratégica

Esta bateria não prova que o Eva Engine® já existe. Ela prova algo mais útil para esta fase: existe evidência concreta de que mecanismos pequenos, auditáveis e determinísticos podem criar valor cognitivo real, enquanto heurísticas sem calibração podem destruir confiança.

O novo Eva Engine® deve, portanto, nascer com duas ambições simultâneas:

1. preservar a confiabilidade dos mecanismos simples que funcionam;
2. criar uma infraestrutura séria para interpretação e aprendizado contínuo que só promova mudanças quando a melhora for mensurável.

Frase de continuidade:

> **Não construir inteligência aparente. Construir capacidade mensurável, componível, explicável e capaz de aprender sob governança.**
