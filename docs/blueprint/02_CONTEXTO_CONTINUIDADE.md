# Eva Engine® — Contexto de Continuidade

**Função deste documento:** permitir que um novo chat, agente ou desenvolvedor retome o projeto sem reconstruir a conversa original.

---

# 1. Estado atual do projeto

O projeto está na fase de **Blueprint arquitetural detalhado**, antes da implementação principal.

A intenção é construir uma especificação suficientemente clara para que Cursor/agentes possam programar por módulos com testes, sem inventar a arquitetura durante a implementação.

O repositório `eva-core-360/infra` é a fonte persistente de verdade do Blueprint.

---

# 2. Origem conceitual

A discussão começou a partir da mecânica de anotações do Eva Memory®.

Ideia inicial:

- a pessoa como centro (“EU”);
- áreas da vida ao redor;
- áreas com mais atividade/continuidade se aproximam;
- áreas deixadas de lado se afastam;
- essa dinâmica foi chamada de gravidade/proximidade cognitiva.

Durante o refinamento, percebeu-se que um grafo visual poderia ser difícil de construir, cansativo e ruim no mobile.

A decisão foi separar:

> **mecânica interna ≠ interface visual**

A gravidade pode continuar sendo calculada nos bastidores sem qualquer grafo obrigatório.

Direção visual atual para mobile: Home Cognitiva / Ranking Vivo.

---

# 3. Virada fundamental

A arquitetura deixou de ser pensada como “motor de notas”.

O objetivo passou a ser construir um motor capaz de servir futuramente a qualquer produto digital.

Portanto:

> Eva Engine® = Core generalista.

> Eva Memory® = primeiro produto consumidor e laboratório real.

Isso é a decisão arquitetural mais importante até agora.

---

# 4. Três modos lógicos desejados

Desde o início da discussão foram escolhidas três naturezas de raciocínio:

## Determinístico

Mesma regra/entrada conhecida produz comportamento previsível. Usado para fatos computáveis, parsing, validações e regras explícitas.

## Heurístico

Usa sinais e aproximações quando não existe certeza absoluta. Deve trabalhar com confiança e limites.

## Preditivo

Usa histórico/padrões para estimar tendência futura, sem transformar previsão em verdade.

Essas três naturezas podem coexistir no mesmo motor.

---

# 5. Atomização

O motor deve transformar conteúdo bruto em unidades menores, mantendo o original intacto.

Exemplo:

> “Hoje dormi mal porque trabalhei até tarde. Amanhã quero dormir às 22h.”

Pode gerar:

- observação: dormi mal;
- possível causa: trabalhei até tarde;
- intenção/experimento: dormir às 22h;
- temporal: amanhã.

A atomização é matéria-prima para relações, continuidade, aprendizado e gravidade.

---

# 6. “Explosão atômica”

A ideia evoluiu para **Expansão Cognitiva Controlada**.

Uma informação nova pode ativar memórias semanticamente próximas, gerar relações e revelar recorrências.

Mas isso precisa de contenção para não virar explosão combinatória.

Limites previstos:

- profundidade;
- número de candidatos;
- número de átomos;
- confiança mínima;
- tempo;
- custo;
- escopo de privacidade.

---

# 7. Aprendizado contínuo

Princípio:

> **Usar a Eva é ensinar a Eva.**

A Eva deve aprender progressivamente o significado particular do usuário sem redefinir o conhecimento global.

Exemplo:

Se naquele contexto “cérebro” costuma significar arquitetura/backend do projeto, o perfil semântico individual aprende isso.

Correções explícitas valem mais que sinais comportamentais indiretos.

Aprendizado previsto em duas velocidades:

- rápido: após correções/feedbacks importantes;
- lento: recalibração periódica baseada em padrões consistentes.

---

# 8. Multilíngue desde a arquitetura

O Core não deve nascer em português para depois ser traduzido.

Language Packs reconhecem expressões em cada idioma e convertem para conceitos internos neutros, como:

```text
ATOM_DECISION
ATOM_INTENTION
REL_CONTINUES
```

O objetivo é permitir novos idiomas sem reconstruir o núcleo semântico.

---

# 9. Filtros e palavrões

A memória original não é censurada.

Palavrões podem ser detectados tecnicamente, mas:

- não são apagados;
- não equivalem automaticamente a emoção negativa;
- não bloqueiam atomização;
- controles de exibição pertencem à camada de produto/política.

Exemplo:

> “Caralho, deu certo!”

não pode virar “sentimento negativo” apenas pela palavra usada.

---

# 10. O que movimenta o motor

O motor é orientado a eventos.

Ele acorda quando algo acontece:

```text
content.created
content.updated
classification.corrected
relation.created
search.performed
memory.archived
...
```

Processa os módulos necessários e volta a ficar ocioso.

A passagem do tempo também pode alterar pesos efetivos, mas a fórmula ainda será definida.

---

# 11. Áreas da vida no Eva Memory®

Base atual aprovada:

1. Saúde
2. Emocional
3. Família
4. Relacionamentos
5. Vida Social
6. Trabalho & Carreira
7. Finanças
8. Projetos & Criação
9. Estudos & Conhecimento
10. Casa & Ambiente
11. Lazer & Experiências
12. Propósito & Espiritualidade
13. Desenvolvimento Pessoal

Modelo:

- 13 áreas-base;
- “EU” não entra na contagem;
- até 2 áreas personalizadas;
- total possível: 15 espaços.

A pessoa não deve ser obrigada a classificar manualmente toda nota.

---

# 12. Interface atual imaginada

Evitar depender de grafo.

Mobile pode mostrar ranking dinâmico:

```text
Saúde ↑
atividade crescente

Projetos & Criação ↑
retomado recentemente

Finanças →
estável

Família ↓
baixa atividade recente
```

A posição é determinada pela mecânica, mas o usuário recebe uma interface conhecida e simples.

---

# 13. Stack atual

Direção inicial:

- Cursor para programação assistida;
- GitHub para fonte de verdade e versionamento;
- TypeScript como linguagem principal;
- monólito modular;
- PostgreSQL/Supabase;
- vetores no Postgres quando necessário;
- API HTTP/REST primeiro;
- background workers para processamento profundo;
- providers intercambiáveis para embeddings/IA;
- dataset JSON/JSONL versionado;
- testes unitários, multilíngues, regressão e golden tests.

---

# 14. Como continuar em um novo chat

Um novo chat NÃO deve reconstruir o projeto do zero.

Fluxo recomendado:

1. Ler `00_BLUEPRINT_MESTRE.md`.
2. Ler `01_REGISTRO_DECISOES.md`.
3. Ler este arquivo.
4. Identificar qual documento específico está sendo refinado.
5. Continuar do estado vigente.
6. Quando uma decisão for aprovada, atualizar o documento especializado, o Blueprint Mestre quando necessário e o Registro de Decisões.

Evitar perguntas do tipo “me explique novamente o projeto” se a resposta estiver no repositório.

---

# 15. Próxima frente de trabalho

A próxima página técnica do Blueprint é a **Ontologia v0**.

Objetivo:

- definir poucos átomos muito bem;
- formalizar exemplos positivos/negativos;
- definir ambiguidade;
- preparar dataset de referência;
- permitir primeira implementação real no Cursor.

Não tentar resolver toda a linguagem humana na primeira versão.

---

# 16. Princípio de trabalho do projeto

O Blueprint é vivo.

Não usar linguagem como “fechado para sempre”. Preferir:

- base vigente;
- decisão aprovada;
- versão atual;
- pronto para seguir;
- hipótese em validação.

A arquitetura pode evoluir, desde que a mudança seja explícita, documentada e testável.
