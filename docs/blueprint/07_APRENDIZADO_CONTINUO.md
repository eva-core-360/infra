# Eva Engine® — Aprendizado Contínuo

**Status:** especificação inicial  
**Objetivo:** definir como o motor melhora com o uso sem perder previsibilidade, privacidade ou separação entre conhecimento global e individual.

---

# 1. Princípio

> **Usar a Eva é ensinar a Eva.**

Aprender continuamente não significa alterar um modelo neural a cada clique.

Na v0, aprendizado contínuo pode ser composto por:

- memória de correções;
- pesos adaptativos;
- aliases pessoais;
- contexto recorrente;
- padrões de classificação;
- histórico de aceitação/rejeição;
- estatística incremental.

---

# 2. Camadas de conhecimento

```text
GLOBAL KNOWLEDGE
ontologia, regras gerais, language packs

USER/ORG PROFILE
significados e pesos particulares

SESSION/ACTIVE CONTEXT
contexto temporário atual
```

O perfil individual nunca redefine silenciosamente o global.

---

# 3. Sinais explícitos

Alta força:

- classificação corrigida;
- classificação confirmada;
- relação criada manualmente;
- relação removida/rejeitada;
- área/contexto alterado manualmente;
- sugestão rejeitada explicitamente.

Todo sinal explícito deve registrar contexto e versão do motor que produziu a previsão original.

---

# 4. Sinais implícitos

Baixa ou média força:

- abriu novamente;
- continuou;
- buscou;
- retornou depois de tempo;
- arquivou;
- concluiu;
- ignorou sugestão.

Regra:

> sinal implícito isolado não deve provocar grande alteração.

---

# 5. Fast learning

Atualização imediata e pequena após feedback forte.

Exemplo:

```text
prediction = Health
correction = Projects
term/context = “cérebro da Eva”
```

O perfil pode aumentar associação entre esse contexto e Projects.

Não mudar ontologia global.

---

# 6. Slow learning

Executado em background e com menor frequência.

Analisa:

- erros recorrentes;
- acertos recorrentes;
- regras personalizadas que surgiram;
- relações sempre rejeitadas;
- associações contextuais consistentes;
- drift de comportamento.

Objetivo: recalibrar de forma estável.

---

# 7. Pesos adaptativos

Hipótese:

```text
base_score
+ user_adjustment
+ context_adjustment
= effective_score
```

Ajustes devem possuir:

- limites mínimo/máximo;
- decay ou revisão periódica quando necessário;
- número mínimo de evidências;
- rastreabilidade.

---

# 8. Perfil semântico individual

Pode registrar:

```text
term / phrase
context
preferred_entity
preferred_area
preferred_atom_type
support_count
reject_count
last_seen
confidence
```

Exemplo:

```text
phrase = “cérebro”
context = Eva project
preferred_area = Projects
support_count = 8
confidence = high
```

---

# 9. Não aprender ruído

Proteções candidatas:

- mínimo de ocorrências;
- janela temporal;
- peso maior para correção explícita;
- limite de ajuste por evento;
- rollback de perfil;
- expiração/revisão de associações antigas;
- detecção de conflito.

---

# 10. Métricas de aprendizagem

```text
correction_rate_before
correction_rate_after
acceptance_rate
personalized_accuracy
global_accuracy
profile_rule_count
profile_conflict_rate
```

A métrica principal não deve ser “quantas coisas aprendeu”, mas “quanto reduziu o esforço/correção sem aumentar erro”.

---

# 11. Privacidade

Aprendizado individual pode revelar vocabulário e padrões muito pessoais.

Portanto:

- escopo deve ser isolado;
- logs devem minimizar conteúdo sensível;
- compartilhamento global precisa de política explícita;
- nenhum aprendizado pessoal deve ser promovido automaticamente para todos.

---

# 12. Futuro: aprendizagem global

Somente em fase posterior poderá existir processo separado para avaliar padrões agregados e promover melhorias globais.

Esse processo deve ser:

- separado do fast learning;
- revisável;
- testado em dataset;
- versionado;
- compatível com políticas de privacidade.

Não faz parte da v0.
