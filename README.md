# WORKFLOW — Anti-Vibe Coding (Akita Way)

> **SEGUIR ESTE CHECKLIST ANTES DE QUALQUER REALIZAÇÃO OPERACIONAL**  
> Metodologia de desenvolvimento disciplinado com IA. Consulte o [`CLAUDE.MD`](./CLAUDE.MD) para a especificação completa do projeto.

---

## ⚡ Princípios Fundamentais

- **Disciplina > Intuição** — Nunca confie cegamente na IA. Estruture o problema primeiro.
- **Anti-Vibe Coding** — Analise, valide e entenda cada resposta da IA antes de aceitar.
- **Planejamento Antes da Execução** — Arquitetura e requisitos são definidos pelo humano.
- **One-Shot é um Mito** — O processo é iterativo: Planejamento → TDD → Implementação → Refatoração → Deploy.
- **Documentação é Código** — Se a arquitetura mudou, atualize o `CLAUDE.MD` antes de prosseguir.

---

## 📋 Checklist Operacional

### Fase 1 — Fundação e Estrutura

- [ ] Definir o domínio do problema com clareza
- [ ] Identificar todos os componentes necessários (banco de dados, APIs externas, serviços)
- [ ] Criar ou atualizar o `CLAUDE.MD` com:
  - [ ] Stack tecnológica
  - [ ] Variáveis de ambiente necessárias
  - [ ] Estrutura de diretórios
  - [ ] Responsabilidades de cada serviço/módulo
- [ ] Registrar decisões de design (ADRs) no `CLAUDE.MD`

### Fase 2 — Desenvolvimento com TDD

- [ ] Solicitar **testes unitários/integrados antes de qualquer implementação**
- [ ] Recusar implementação sem testes correspondentes (Red → Green → Refactor)
- [ ] Validar que os testes **falham** antes de escrever a implementação
- [ ] Implementar o mínimo de código necessário para os testes passarem
- [ ] Refatorar mantendo todos os testes verdes
- [ ] Se a IA alucinar ou divergir: **pare, desative o autocomplete e edite manualmente**

### Fase 3 — Segurança e Isolamento (AI-Jail)

- [ ] Configurar **Docker Container** para isolar a execução da IA
- [ ] Definir e aplicar modelo de permissões para agentes de IA
- [ ] Monitorar cada comando executado pela IA no terminal
- [ ] Confirmar que nenhuma credencial ou chave real está exposta ao agente
- [ ] Nunca executar a IA diretamente na máquina local sem sandboxing

### Fase 4 — Refatoração Multisserviço

- [ ] Usar estrutura de **Monorepo** para visibilidade global dos serviços
- [ ] Escrever testes de integração para validar a comunicação entre serviços
- [ ] Garantir que mudanças de contrato de dados disparam falhas nos testes de integração
- [ ] Validar todos os serviços afetados após cada refatoração

---

## 📁 Documentação Adicional

| Arquivo | Descrição |
|---------|-----------|
| [`CLAUDE.MD`](./CLAUDE.MD) | Especificação completa: stack, ADRs, regras de negócio |
| [`docs/phases/phase-1-foundation.md`](./docs/phases/phase-1-foundation.md) | Guia detalhado da Fase 1 |
| [`docs/phases/phase-2-tdd.md`](./docs/phases/phase-2-tdd.md) | Guia detalhado da Fase 2 — TDD |
| [`docs/phases/phase-3-security.md`](./docs/phases/phase-3-security.md) | Guia detalhado da Fase 3 — Segurança |
| [`docs/phases/phase-4-refactoring.md`](./docs/phases/phase-4-refactoring.md) | Guia detalhado da Fase 4 — Refatoração |
| [`docs/guidelines/anti-vibe-coding.md`](./docs/guidelines/anti-vibe-coding.md) | Princípios Anti-Vibe Coding |
| [`docs/guidelines/prompt-engineering.md`](./docs/guidelines/prompt-engineering.md) | Engenharia de Prompt para desenvolvimento |

---

## 🚀 Fluxo Resumido

```
Planejamento → CLAUDE.MD → TDD → Implementação → Refatoração → Deploy
```

Não busque atalhos. Esta metodologia não é sobre criar software em 10 minutos — é sobre construir sistemas **robustos e manuteníveis**.
