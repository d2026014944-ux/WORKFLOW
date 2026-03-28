# Fase 3 — Segurança e Isolamento (AI-Jail)

> **Objetivo:** Proteger seu sistema, dados e configurações de execuções não controladas por agentes de IA.  
> Nunca execute a IA diretamente na sua máquina local sem sandboxing.

---

## Por Que o Isolamento é Essencial

Agentes de IA com acesso ao terminal podem, intencionalmente ou por alucinação:

- Deletar arquivos do sistema
- Vazar credenciais armazenadas localmente
- Executar comandos com efeitos colaterais irreversíveis
- Instalar dependências maliciosas
- Modificar configurações do sistema operacional

O modelo **AI-Jail** (sandboxing via Docker) elimina esses riscos ao restringir o agente a um ambiente controlado e descartável.

---

## Etapas

### 3.1 Configurar o Docker Container (AI-Jail)

Crie um `Dockerfile` dedicado para o ambiente de desenvolvimento com IA:

```dockerfile
# Exemplo de Dockerfile para AI-Jail
FROM ubuntu:22.04

# Instale apenas o necessário
RUN apt-get update && apt-get install -y \
    git \
    curl \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Usuário sem privilégios de root
RUN useradd -m -s /bin/bash developer
USER developer

WORKDIR /workspace
```

Execute o agente sempre dentro deste container:

```bash
docker run --rm -it \
  -v $(pwd):/workspace:rw \
  -e SOME_VAR=value \
  --network=none \  # Isole a rede se não for necessária
  ai-jail-image
```

### 3.2 Definir Modelo de Permissões

Ao usar agentes como Claude Code, Copilot Agent ou similares:

| Permissão | Recomendação |
|-----------|-------------|
| Leitura de arquivos | ✅ Permitir (apenas no workspace) |
| Escrita de arquivos | ✅ Permitir (apenas no workspace) |
| Execução de comandos | ⚠️ Permitir com monitoramento |
| Acesso à rede | ⚠️ Restringir ao mínimo necessário |
| Acesso ao sistema de arquivos do host | ❌ Nunca permitir |
| Acesso a variáveis de ambiente do host | ❌ Nunca permitir sem filtragem |

### 3.3 Monitorar Comandos Executados

Antes de permitir que a IA execute qualquer comando no terminal:

1. **Leia o comando completo** — entenda o que ele faz
2. **Verifique efeitos colaterais** — o comando modifica algo fora do workspace?
3. **Confirme explicitamente** — nunca deixe a execução automática sem revisão
4. **Registre comandos suspeitos** — se um comando parece incomum, questione a IA

### 3.4 Gestão de Credenciais e Segredos

- **Nunca** passe credenciais reais para o agente de IA
- Use variáveis de ambiente mockadas ou de ambiente de teste
- Configure o `.gitignore` para garantir que `.env` nunca seja commitado
- Audite o histórico de commits para confirmar que nenhum segredo foi exposto

```bash
# Verificar se há segredos no histórico do git
git log --all --full-history -- "*.env"
git grep -r "password\|secret\|api_key" $(git rev-list --all)
```

### 3.5 Ambiente Descartável

O grande benefício do Docker é que o ambiente é **descartável**:

- Se algo der errado, destrua o container e recrie do zero
- O estado do container nunca afeta sua máquina local
- Múltiplos agentes podem rodar em paralelo sem interferência

```bash
# Destruir o ambiente e recriar
docker rm -f ai-jail-container
docker run --rm -it ... ai-jail-image
```

---

## Checklist da Fase 3

- [ ] `Dockerfile` criado para o AI-Jail
- [ ] Agente executando **dentro** do container Docker
- [ ] Modelo de permissões definido e aplicado
- [ ] Monitoramento ativo de comandos executados pela IA
- [ ] Variáveis de ambiente reais **nunca** expostas ao agente
- [ ] `.gitignore` confirmado — nenhum `.env` será commitado
- [ ] Processo de destruição e recriação do ambiente documentado

---

## Erros Comuns a Evitar

| Erro | Consequência | Correção |
|------|-------------|----------|
| Rodar agente diretamente no host | Risco de danos irreversíveis ao sistema | Sempre use Docker |
| Passar credenciais reais ao agente | Exposição de dados sensíveis | Use credenciais mockadas ou de teste |
| Não monitorar comandos | Execução de comandos destrutivos sem revisão | Revise cada comando antes de aprovar |
| Dar acesso root ao container | Aumenta superfície de ataque | Use usuário sem privilégios |

---

*Fase anterior: [Fase 2 — Desenvolvimento com TDD](./phase-2-tdd.md)*  
*Próxima fase: [Fase 4 — Refatoração Multisserviço](./phase-4-refactoring.md)*
