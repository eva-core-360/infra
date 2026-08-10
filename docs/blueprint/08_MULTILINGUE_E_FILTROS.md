# Eva Engine® — Arquitetura Multilíngue e Filtros

**Status:** especificação inicial

---

# 1. Objetivo

Permitir que o motor compreenda diferentes idiomas sem criar uma ontologia separada para cada língua.

Princípio:

```text
idioma da entrada
   ↓
Language Pack
   ↓
evidências linguísticas
   ↓
conceitos canônicos do Core
```

---

# 2. Core independente de idioma

Exemplo:

```text
pt-BR: “decidi”
en: “I decided”
es: “decidí”
```

Todos podem produzir evidência para:

```text
ATOM_DECISION
```

A ontologia não deve armazenar apenas palavras portuguesas como definição estrutural.

---

# 3. Estrutura de Language Pack

Hipótese:

```text
language-pack/
  metadata
  lexical_signals
  patterns
  temporal_rules
  negation_rules
  profanity_lexicon
  colloquialisms
  tests
```

Cada pack deve possuir versão própria.

---

# 4. Detecção de idioma

Requisitos:

- suportar conteúdo curto;
- registrar confiança;
- permitir idioma informado pelo produto como pista;
- suportar mistura de idiomas futuramente;
- não bloquear processamento quando confiança for baixa.

Questão em aberto: biblioteca/provider inicial.

---

# 5. Datas e tempo

Language Packs precisam compreender expressões locais:

```text
hoje
ontem
amanhã
semana passada
daqui a três dias
segunda-feira
às 14h
há seis meses
```

E equivalentes em outros idiomas.

Internamente, o Core deve receber representação temporal normalizada + referência ao texto original.

---

# 6. Negação

Negação é crítica para evitar classificações erradas.

Exemplo:

> “Não decidi mudar de fornecedor.”

A presença da palavra “decidi” não pode gerar automaticamente uma Decision positiva.

Language Pack deve produzir evidência de negação/escopo.

---

# 7. Profanidade

Princípios aprovados:

1. preservar original;
2. não censurar automaticamente;
3. não usar palavrão como sinônimo de negatividade;
4. permitir atributo técnico quando necessário;
5. analisar contexto antes de inferir agressão;
6. filtros de visualização pertencem à camada de produto/policy.

Exemplos distintos:

```text
“Caralho, deu certo!”
```

vs.

```text
insulto dirigido explicitamente a alguém
```

A mesma palavra pode exercer funções pragmáticas diferentes.

---

# 8. Gírias e vocabulário pessoal

Language Pack fornece conhecimento linguístico geral.

Perfil Semântico Individual fornece significado pessoal/contextual.

Exemplo:

```text
“cérebro”
```

pode ter significado global anatômico, mas em um contexto de projeto pode ser aprendido como arquitetura/backend.

---

# 9. Filtros técnicos

Filtros possíveis:

```text
profanity
url
email
phone
currency
number
date
time
emoji
mention
hashtag
code_fragment
```

Nem todo filtro gera átomo. Muitos apenas produzem metadados/evidências.

---

# 10. Conteúdo sensível

Detecção de conteúdo sensível deve ser separada da ontologia cognitiva.

Responsabilidades de política:

- visibilidade;
- compartilhamento;
- retenção;
- execução de ação;
- restrições de produto.

O motor não deve apagar memória pessoal original apenas porque um classificador marcou sensibilidade.

---

# 11. Testes multilíngues

Criar pares semanticamente equivalentes:

```text
pt-BR: “Decidi mudar amanhã.”
en: “I decided to change tomorrow.”
es: “Decidí cambiar mañana.”
```

Resultado conceitual esperado:

```text
ATOM_DECISION
ATOM_TEMPORAL
```

Objetivo: testar equivalência semântica entre packs.

---

# 12. Estratégia de lançamento

Nascer multilíngue por arquitetura não significa suportar todos os idiomas na v0.

Pode-se implementar primeiro:

- pt-BR completo para o dataset inicial;
- en como segundo pack de validação arquitetural;
- demais idiomas por expansão posterior.

A quantidade final da primeira release ainda está em aberto.
