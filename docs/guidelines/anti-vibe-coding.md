# Anti-Vibe Coding — Princípios e Prática

> **Definição:** "Vibe Coding" é o ato de aceitar cegamente sugestões da IA, guiado pela impressão de que o código "parece certo", sem análise crítica.  
> O Anti-Vibe Coding é a disciplina que combate esse comportamento.

---

## O Problema do Vibe Coding

Quando um desenvolvedor entra no modo de "vibe coding":

1. Faz um prompt vago para a IA
2. Aceita o código gerado sem ler completamente
3. Executa e "parece funcionar"
4. Passa para a próxima feature
5. Acumula dívida técnica invisível até o sistema colapsar

O código gerado pode estar **funcionalmente correto** para o caso de teste do prompt, mas:
- Violar regras de negócio documentadas
- Introduzir vulnerabilidades de segurança
- Criar dependências circulares
- Usar padrões inconsistentes com o resto do sistema
- Fazer suposições incorretas sobre o domínio

---

## Os 6 Princípios Anti-Vibe

### Princípio 1: Disciplina > Intuição

A intuição é útil para exploração, mas perigosa para tomada de decisões técnicas. Antes de qualquer prompt:

- Estruture o problema por escrito
- Defina os critérios de aceitação
- Documente as restrições no `CLAUDE.MD`

### Princípio 2: Análise Obrigatória

Cada resposta da IA deve passar por uma análise antes de ser aceita:

```
☐ O código faz o que eu pedi?
☐ O código está correto para o domínio (não apenas para o prompt)?
☐ O código segue os padrões definidos no CLAUDE.MD?
☐ O código tem testes?
☐ Os testes cobrem os casos de borda?
☐ O código introduz vulnerabilidades?
☐ O código cria dependências desnecessárias?
```

### Princípio 3: Planejamento Antes da Execução

O design da arquitetura, a definição dos serviços e os requisitos são responsabilidade do **humano**, não da IA.

A IA é usada para **acelerar a implementação** de decisões já tomadas, não para tomar decisões arquiteturais.

### Princípio 4: One-Shot é um Mito

Não existe um prompt mágico que gera um sistema completo, correto e manutenível. O processo real é:

```
Planejamento → Documentação → TDD → Implementação → Revisão → Refatoração → Deploy
```

Cada etapa requer atenção humana. Pular etapas gera problemas maiores à frente.

### Princípio 5: Documentação é Código

Se a arquitetura mudou e o `CLAUDE.MD` não reflete essa mudança, a IA trabalhará com uma realidade desatualizada. Isso é tão perigoso quanto código desatualizado.

**Regra:** Antes de qualquer novo prompt que envolva mudança arquitetural, atualize o `CLAUDE.MD`.

### Princípio 6: Mão na Massa

Se a IA:
- Alucinar (afirmar algo falso com confiança)
- Divergir do contexto do projeto
- Sugerir código que viola as regras documentadas
- Entrar em loop de correções sem convergir

**Ação:** Pare. Desative o autocomplete. Edite manualmente. A IA é uma ferramenta — você é o engenheiro.

---

## Padrões de Prompt Anti-Vibe

### ✅ Prompt Estruturado (Bom)

```
Contexto: [Descreva o estado atual do sistema, referenciando o CLAUDE.MD]
Objetivo: [Descreva o que precisa ser feito]
Restrições: [Liste o que NÃO pode ser feito]
Critérios de Aceitação: [Liste como você saberá que está correto]
Primeiro passo: Escreva os testes para [feature X] antes de qualquer implementação.
```

### ❌ Vibe Prompt (Ruim)

```
"Cria um sistema de autenticação"
"Adiciona uma API de pagamentos"
"Refatora o código para ser mais limpo"
```

---

## Sinais de Alerta (Red Flags)

Se você notar os seguintes comportamentos, pare imediatamente:

- A IA sugere código sem perguntar sobre o contexto
- A IA afirma com confiança algo que contradiz sua documentação
- A IA gera implementação antes de você pedir os testes
- A IA ignora restrições que você mencionou
- O código "parece funcionar" mas você não consegue explicar por quê
- A IA começa a sugerir bibliotecas não listadas no `CLAUDE.MD`

---

## Checklist Anti-Vibe (Por Feature)

Antes de submeter qualquer código gerado por IA:

- [ ] Li todo o código linha por linha
- [ ] Entendo o que cada parte faz
- [ ] Os testes foram escritos antes da implementação
- [ ] O código segue os padrões do `CLAUDE.MD`
- [ ] Não há vulnerabilidades óbvias
- [ ] Não há dependências desnecessárias adicionadas
- [ ] O código não viola regras de negócio documentadas
- [ ] Executei os testes e eles passam

---

*Consulte também: [Engenharia de Prompt](./prompt-engineering.md)*
