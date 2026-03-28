# CLAUDE.MD — Especificação do Projeto (Akita Way)

> **Este arquivo é a fonte da verdade do projeto.**  
> Toda decisão arquitetural, regra de negócio e mudança de design deve ser registrada aqui **antes** de qualquer interação com a IA ou escrita de código.  
> Mantenha este arquivo sempre atualizado. A IA trabalha a partir dele.

---

## 1. Visão Geral do Projeto

| Campo              | Valor |
|--------------------|-------|
| **Nome**           | WORKFLOW |
| **Objetivo**       | Repositório de workflow e checklist para desenvolvimento disciplinado com IA (Anti-Vibe Coding) |
| **Metodologia**    | Akita Way — Disciplina > Intuição |
| **Status**         | Em desenvolvimento |

---

## 2. Stack Tecnológica

> Liste aqui as tecnologias, frameworks e ferramentas que compõem o projeto.

```
# Exemplo — substitua conforme o projeto real
Linguagem:       (definir)
Framework:       (definir)
Banco de Dados:  (definir)
Containerização: Docker
CI/CD:           (definir)
Testes:          (definir — ex: Jest, pytest, Go test)
```

---

## 3. Variáveis de Ambiente

> **Nunca commite valores reais aqui.** Liste apenas os nomes e descrições.

```
# Exemplo
DATABASE_URL=          # Conexão com o banco de dados
API_KEY=               # Chave da API externa
SECRET_KEY=            # Chave secreta da aplicação
PORT=                  # Porta de execução do servidor
```

Utilize um arquivo `.env.example` na raiz do repositório com os nomes de todas as variáveis necessárias.

---

## 4. Estrutura de Diretórios

```
WORKFLOW/
├── CLAUDE.MD               ← Esta especificação (evolui com o projeto)
├── README.md               ← Checklist operacional
├── .env.example            ← Variáveis de ambiente necessárias (sem valores)
├── .gitignore
├── docs/
│   ├── phases/
│   │   ├── phase-1-foundation.md
│   │   ├── phase-2-tdd.md
│   │   ├── phase-3-security.md
│   │   └── phase-4-refactoring.md
│   └── guidelines/
│       ├── prompt-engineering.md
│       └── anti-vibe-coding.md
└── (serviços e código do projeto)
```

---

## 5. Responsabilidades dos Serviços e Modelos

> Descreva aqui cada serviço e o que ele faz. Atualize conforme o projeto cresce.

| Serviço / Módulo | Responsabilidade |
|------------------|------------------|
| *(definir)*      | *(definir)*      |

---

## 6. Regras de Negócio

> Registre aqui todas as decisões de negócio que impactam o comportamento do sistema.

1. *(Adicionar conforme surgirem)*

---

## 7. Decisões de Design (ADRs — Architecture Decision Records)

> Cada decisão importante de arquitetura deve ser registrada aqui com justificativa.

### ADR-001: Uso de Monorepo
- **Data:** 2026-03-28
- **Status:** Aceito
- **Contexto:** Projetos multisserviço beneficiam-se de visibilidade global para a IA e para o desenvolvedor.
- **Decisão:** Utilizar estrutura de monorepo.
- **Consequências:** Refatorações cruzadas entre serviços ficam mais seguras. Requer boa organização de diretórios.

### ADR-002: TDD como Requisito Não-Negociável
- **Data:** 2026-03-28
- **Status:** Aceito
- **Contexto:** A IA pode gerar código que compila mas não faz o que deve. Testes escritos antes da implementação protegem o sistema.
- **Decisão:** Nenhuma implementação é aceita sem testes escritos previamente.
- **Consequências:** Velocidade inicial menor, mas qualidade e manutenibilidade maiores.

### ADR-003: Isolamento via Docker (AI-Jail)
- **Data:** 2026-03-28
- **Status:** Aceito
- **Contexto:** Agentes de IA com acesso ao terminal podem executar comandos destrutivos ou vazar dados.
- **Decisão:** Toda execução de IA em ambiente local deve ser containerizada via Docker.
- **Consequências:** Proteção do sistema de arquivos local e das configurações sensíveis.

---

## 8. Workflow de Desenvolvimento (Akita Way)

```
Planejamento → Documentação (CLAUDE.MD) → TDD → Implementação → Refatoração → Deploy
```

### Fase 1 — Fundação e Estrutura
- [ ] Definir domínio do problema
- [ ] Identificar componentes necessários (DB, APIs, serviços)
- [ ] Criar/atualizar este arquivo CLAUDE.MD
- [ ] Documentar stack, variáveis de ambiente e estrutura de diretórios

### Fase 2 — Desenvolvimento com TDD
- [ ] Solicitar testes **antes** de qualquer implementação
- [ ] Recusar sugestões de implementação sem testes correspondentes
- [ ] Validar que os testes falham antes da implementação (Red)
- [ ] Implementar o código mínimo para passar nos testes (Green)
- [ ] Refatorar mantendo os testes verdes (Refactor)

### Fase 3 — Segurança e Isolamento
- [ ] Configurar Docker Container para execução da IA
- [ ] Definir modelo de permissões para agentes
- [ ] Monitorar comandos executados pela IA no terminal
- [ ] Nunca expor credenciais ou chaves reais ao agente

### Fase 4 — Refatoração Multisserviço
- [ ] Usar monorepo para visibilidade global
- [ ] Escrever testes de integração entre serviços
- [ ] Validar comunicação entre serviços após cada mudança de contrato

---

## 9. Princípios Fundamentais (Anti-Vibe Coding)

1. **Disciplina > Intuição:** Estruture o problema antes de solicitar qualquer código à IA.
2. **Análise Obrigatória:** Nunca aceite uma resposta da IA sem analisar, validar e entender se ela faz sentido no contexto do sistema.
3. **Planejamento Antes da Execução:** Design de arquitetura e definição de requisitos são responsabilidade do humano, não da IA.
4. **One-Shot é um Mito:** O processo é sempre iterativo. Não existe prompt mágico.
5. **Documentação é Código:** Se a arquitetura mudou, atualize este arquivo antes de prosseguir.
6. **Mão na Massa:** Se a IA alucinar ou divergir, pare, desative o autocomplete e edite manualmente.

---

## 10. Checklist de Onboarding para Novos Colaboradores

- [ ] Ler este arquivo (`CLAUDE.MD`) completamente
- [ ] Ler o `README.md`
- [ ] Configurar variáveis de ambiente a partir do `.env.example`
- [ ] Executar os testes existentes e garantir que passam
- [ ] Não submeter código sem testes

---

*Última atualização: 2026-03-28 — Versão inicial criada com a especificação do Anti-Vibe Coding (Akita Way).*
