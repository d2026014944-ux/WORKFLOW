# Engenharia de Prompt para Desenvolvimento de Software

> **Objetivo:** Estruturar interações com a IA para obter resultados previsíveis, corretos e alinhados com o contexto do projeto.  
> Prompts bem estruturados são tão importantes quanto código bem escrito.

---

## Por Que a Qualidade do Prompt Importa

A IA responde ao que você diz, não ao que você quer dizer. Um prompt vago gera uma resposta genérica. Um prompt estruturado gera uma resposta contextualizada e útil.

A diferença entre um engenheiro que usa IA produtivamente e um que se frustra com ela está, em grande parte, na qualidade dos prompts.

---

## A Anatomia de um Bom Prompt

Um prompt eficaz para desenvolvimento de software tem 5 elementos:

### 1. Contexto

Forneça o estado atual do sistema. Referencie o `CLAUDE.MD` sempre que possível.

```
"Estou trabalhando em um sistema de e-commerce com a seguinte stack: [stack].
O serviço de pedidos está em services/orders/ e expõe uma API REST.
Os contratos de dados estão documentados no CLAUDE.MD."
```

### 2. Objetivo

Diga exatamente o que precisa ser feito, sem ambiguidade.

```
"Preciso adicionar suporte a cupons de desconto no fluxo de checkout."
```

### 3. Restrições

Liste explicitamente o que não pode acontecer.

```
"Restrições:
- Não altere a interface pública do serviço de pedidos
- Não adicione novas dependências sem aprovação
- O desconto máximo aplicável é 30%"
```

### 4. Critérios de Aceitação

Defina como você saberá que o resultado está correto.

```
"Critérios de aceitação:
- Um cupom válido reduz o total do pedido pelo percentual configurado
- Um cupom expirado é rejeitado com erro 400
- Um cupom já utilizado é rejeitado com erro 409
- O desconto nunca ultrapassa 30% do valor total"
```

### 5. Próximo Passo Específico

Peça apenas **um passo de cada vez**.

```
"Primeiro passo: Escreva apenas os testes unitários para o validador de cupons.
Não implemente o validador ainda."
```

---

## Templates de Prompt por Situação

### Template: Solicitação de Testes

```
Contexto: [descreva o módulo/serviço]
Feature: [nome da feature]
Casos de uso a testar:
1. [caso de uso 1]
2. [caso de uso 2]
3. [caso de uso 3 — caso de borda]

Escreva os testes unitários para [feature] cobrindo estes casos.
Use [framework de teste] seguindo o padrão dos testes existentes em [caminho/para/testes].
NÃO escreva a implementação.
```

### Template: Solicitação de Implementação

```
Os testes em [caminho/para/testes] estão em estado Red (falham).
Implemente [feature] para que esses testes passem.

Restrições:
- [restrição 1]
- [restrição 2]

Siga a arquitetura documentada no CLAUDE.MD.
```

### Template: Refatoração

```
O módulo [módulo] precisa ser refatorado para [objetivo da refatoração].

Estado atual: [descreva o estado atual]
Estado desejado: [descreva o estado final]

Os contratos públicos (APIs/interfaces) NÃO devem ser alterados.

Antes de refatorar, identifique todos os pontos do sistema que serão afetados.
```

### Template: Investigação de Bug

```
Tenho um bug no módulo [módulo]:

Comportamento atual: [o que acontece]
Comportamento esperado: [o que deveria acontecer]
Passos para reproduzir: [lista de passos]

Analise o código em [caminho] e identifique a causa raiz.
NÃO proponha correção ainda — apenas explique a causa.
```

---

## Práticas de Prompt

### ✅ Faça

- Forneça contexto antes de fazer a pergunta
- Peça um passo de cada vez
- Referencie o `CLAUDE.MD` em prompts que envolvem arquitetura
- Especifique o framework/padrão a seguir
- Defina critérios de aceitação mensuráveis
- Peça os testes antes da implementação

### ❌ Evite

- Prompts de uma linha para problemas complexos
- Pedir implementação e testes no mesmo prompt
- Assumir que a IA conhece o contexto do projeto sem informá-la
- Aceitar a primeira resposta sem verificar se atende os critérios
- Corrigir a IA múltiplas vezes no mesmo contexto sem reiniciar

---

## Gerenciamento de Contexto

A IA tem um limite de contexto. Em sessões longas:

1. Resuma o progresso a cada poucas interações
2. Referencie o `CLAUDE.MD` para reancorá-la ao contexto do projeto
3. Se a qualidade das respostas cair, inicie uma nova sessão com contexto resumido
4. Nunca continue uma sessão onde a IA claramente perdeu o contexto

### Template: Resumo de Sessão

```
Resumo da sessão até agora:
- Implementamos: [lista do que foi feito]
- Estado atual: [o que está funcionando]
- Próximo objetivo: [o que precisamos fazer]
- Restrições ativas: [lista de restrições]

A partir daqui, continuemos com [próximo passo].
```

---

## Iteração Produtiva

O fluxo ideal de uma sessão de desenvolvimento com IA:

```
1. Forneça contexto (CLAUDE.MD + estado atual)
2. Solicite testes para a próxima feature
3. Valide os testes (Red)
4. Solicite a implementação
5. Valide a implementação (Green)
6. Solicite refatoração se necessário
7. Atualize o CLAUDE.MD com o que foi implementado
8. Repita para a próxima feature
```

---

*Consulte também: [Anti-Vibe Coding](./anti-vibe-coding.md)*
