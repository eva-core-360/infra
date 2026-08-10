# AGENTS.md — Regras para agentes do Eva Engine®

Este arquivo deve ser lido por qualquer agente de código, Cursor, assistente ou colaborador antes de alterar arquitetura ou implementação.

## Leitura obrigatória

Antes de trabalhar:

1. `docs/blueprint/00_BLUEPRINT_MESTRE.md`
2. `docs/blueprint/01_REGISTRO_DECISOES.md`
3. `docs/blueprint/02_CONTEXTO_CONTINUIDADE.md`
4. documento específico da área em que será feita a alteração

## Regra de autoridade arquitetural

O Blueprint vigente é a referência arquitetural. O agente não deve transformar preferência pessoal, conveniência momentânea ou sugestão automática em decisão estrutural sem registrar a proposta e sua justificativa.

## Regras não negociáveis da base atual

1. O Eva Engine® é generalista; Eva Memory® é produto consumidor.
2. Produtos dependem do Core; o Core não depende de produtos.
3. Conteúdo original nunca é sobrescrito pela interpretação.
4. RAW, DERIVED, INFERRED e LEARNED devem permanecer conceitualmente separados.
5. Inferências possuem confiança e rastreabilidade.
6. Correções são reversíveis e alimentam aprendizado.
7. Aprendizado individual não altera automaticamente o conhecimento global.
8. O motor nasce multilíngue por arquitetura.
9. O sistema é orientado a eventos.
10. A expansão cognitiva deve possuir limites explícitos.
11. O motor não deve depender de grafo visual.
12. O Core não deve ficar acoplado a fornecedores específicos de IA, embeddings ou nuvem.
13. Começar como monólito modular; microserviços só quando houver necessidade comprovada.
14. Toda mudança de comportamento relevante deve ter teste.
15. Toda mudança estrutural deve atualizar a documentação correspondente.

## Processo de implementação

Para cada capacidade nova:

```text
IDEIA
  ↓
ESPECIFICAÇÃO
  ↓
CASOS DE TESTE
  ↓
IMPLEMENTAÇÃO
  ↓
TESTES
  ↓
OBSERVAÇÃO
  ↓
AJUSTE
```

Não inverter para “gerar código e depois descobrir qual era a regra”.

## Política de mudanças

### Pode fazer diretamente

- implementar comportamento já especificado;
- criar testes para comportamento aprovado;
- corrigir bugs sem alterar princípios;
- melhorar tipagem, organização e documentação sem mudar semântica;
- sugerir refatorações compatíveis com o Blueprint.

### Deve registrar antes de alterar

- entidades fundamentais;
- ontologia;
- formato de eventos;
- separação de camadas de memória;
- política de confiança;
- política de aprendizagem;
- estratégia de persistência;
- limites da expansão cognitiva;
- contratos públicos da API/SDK;
- dependência estrutural de um fornecedor externo.

## Critério para dependências

Adicionar biblioteca somente quando:

- resolve problema real;
- reduz complexidade total;
- possui manutenção razoável;
- não viola privacidade/arquitetura;
- pode ser substituída por uma interface quando fizer sentido.

## Qualidade mínima

Código novo deve buscar:

- tipos explícitos;
- contratos pequenos;
- módulos coesos;
- baixo acoplamento;
- logs estruturados para pipeline cognitivo;
- testes de regressão;
- versionamento de regras relevantes.

## Linguagem e nomenclatura

Identificadores internos do Core devem ser neutros de idioma quando representam conceitos semânticos universais.

Exemplo preferido:

```text
ATOM_DECISION
REL_CONTINUES
```

Evitar conceitos universais nomeados apenas em português dentro do modelo canônico.

## Regra final

> Se uma decisão tornar o primeiro protótipo mais rápido, mas impedir o Eva Engine® de permanecer generalista, ela deve ser isolada no Domain Pack ou no produto, não embutida no Core.
