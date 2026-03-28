# Fase 1 — Fundação e Estrutura

> **Objetivo:** Estabelecer uma base sólida antes de escrever qualquer linha de código.  
> A IA só entra em ação depois que esta fase estiver completa.

---

## Por Que Esta Fase é Crítica

Iniciar o desenvolvimento sem uma fundação clara é a principal causa do "vibe coding" — o ato de aceitar cegamente sugestões da IA sem entender o contexto do sistema. Ao definir o domínio, a arquitetura e a especificação **antes** de envolver a IA, você garante que ela trabalhe como colaboradora técnica e não como oráculo.

---

## Etapas

### 1.1 Definição do Domínio

Antes de qualquer outra coisa, responda:

- **Qual problema este sistema resolve?**
- **Quem são os usuários?**
- **Quais são as entidades principais do domínio?**
- **Quais são as fronteiras do sistema?** (O que está dentro e o que está fora do escopo)

Documente as respostas no `CLAUDE.MD`.

### 1.2 Identificação de Componentes

Liste todos os componentes que o sistema precisa:

- Banco(s) de dados e seus modelos
- APIs externas a serem consumidas
- Serviços internos e suas responsabilidades
- Filas, caches, storage e outros recursos de infraestrutura

### 1.3 Criação e Preenchimento do CLAUDE.MD

O arquivo `CLAUDE.MD` é a **única fonte da verdade** do projeto. Preencha:

```markdown
## Stack Tecnológica
## Variáveis de Ambiente
## Estrutura de Diretórios
## Responsabilidades dos Serviços
## Regras de Negócio
## Decisões de Design (ADRs)
```

**Regra:** Toda mudança de arquitetura deve ser registrada no `CLAUDE.MD` **antes** de qualquer interação com a IA.

### 1.4 Estrutura de Diretórios

Crie a estrutura de diretórios do projeto antes de codificar. Isso orienta tanto o desenvolvedor quanto a IA sobre onde cada coisa deve estar.

### 1.5 Configuração do Ambiente

- Crie o arquivo `.env.example` com todas as variáveis necessárias (sem valores reais)
- Configure o `.gitignore` para excluir `.env`, artefatos de build e dependências
- Configure o Docker para isolamento (ver Fase 3)

---

## Checklist da Fase 1

- [ ] Domínio do problema definido e documentado
- [ ] Componentes necessários identificados
- [ ] `CLAUDE.MD` criado e preenchido com stack, variáveis, estrutura e responsabilidades
- [ ] Decisões de arquitetura registradas como ADRs
- [ ] Estrutura de diretórios criada
- [ ] `.env.example` criado
- [ ] `.gitignore` configurado

---

## Erros Comuns a Evitar

| Erro | Consequência | Correção |
|------|-------------|----------|
| Pular esta fase e ir direto ao código | IA gera código sem contexto, levando a retrabalho | Sempre complete esta fase primeiro |
| CLAUDE.MD desatualizado | IA trabalha com uma realidade diferente do projeto | Atualize o arquivo a cada mudança arquitetural |
| Definir a estrutura depois de codificar | Código mal organizado, difícil de mover | Defina antes, refatore depois se necessário |

---

*Próxima fase: [Fase 2 — Desenvolvimento com TDD](./phase-2-tdd.md)*
