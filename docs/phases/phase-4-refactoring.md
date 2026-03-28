# Fase 4 — Refatoração Multisserviço

> **Objetivo:** Manter a coerência e qualidade do sistema à medida que ele cresce e evolui através de múltiplos serviços.  
> Usar a IA de forma segura para refatorações que afetam múltiplos pontos do sistema.

---

## Por Que a Refatoração Estruturada é Essencial

Em sistemas multisserviço, uma mudança em um serviço pode quebrar contratos com outros serviços de forma silenciosa. Sem uma estrutura adequada:

- Mudanças de schema de banco de dados quebram consumidores silenciosamente
- APIs alteradas causam falhas apenas em produção
- A IA propõe refatorações parciais que deixam o sistema em estado inconsistente

A combinação de **monorepo + testes de integração** captura esses problemas automaticamente.

---

## Etapas

### 4.1 Estrutura de Monorepo

Organize todos os serviços em um único repositório:

```
projeto/
├── CLAUDE.MD
├── services/
│   ├── service-a/
│   │   ├── src/
│   │   ├── tests/
│   │   └── package.json (ou equivalente)
│   ├── service-b/
│   │   ├── src/
│   │   ├── tests/
│   │   └── package.json
│   └── shared/
│       └── types/          ← Tipos/contratos compartilhados
├── integration-tests/
│   ├── service-a-b.test.ts
│   └── e2e/
└── docker-compose.yml
```

**Benefícios:**
- A IA tem visibilidade global de todos os serviços
- Refatorações cruzadas podem ser solicitadas em uma única sessão
- Contratos compartilhados ficam em um lugar centralizado

### 4.2 Definir Contratos Entre Serviços

Antes de qualquer refatoração, documente os contratos de dados entre serviços no `CLAUDE.MD`:

```markdown
## Contratos de Serviços

### Service A → Service B
- Endpoint: POST /api/events
- Payload: { userId: string, eventType: string, timestamp: ISO8601 }
- Resposta: { eventId: string, status: "accepted" | "rejected" }
```

### 4.3 Testes de Integração Entre Serviços

Escreva testes que validam a comunicação entre serviços:

```typescript
// Exemplo: integration-tests/service-a-b.test.ts
describe('Service A → Service B integration', () => {
  it('should accept valid event payload', async () => {
    const response = await serviceA.sendEvent({
      userId: 'user-123',
      eventType: 'purchase',
      timestamp: new Date().toISOString()
    });
    
    expect(response.status).toBe('accepted');
    expect(response.eventId).toBeDefined();
  });

  it('should reject invalid payload', async () => {
    const response = await serviceA.sendEvent({
      userId: 'user-123',
      // eventType ausente — deve falhar
    });
    
    expect(response.status).toBe('rejected');
  });
});
```

**Regra:** Se um serviço alterar sua estrutura de dados, os testes de integração com seus consumidores **devem falhar imediatamente**.

### 4.4 Fluxo de Refatoração com IA

Ao solicitar uma refatoração multisserviço à IA:

1. **Atualize o CLAUDE.MD** com a nova estrutura desejada
2. **Solicite os novos testes de integração** que refletem o estado final desejado
3. **Execute os testes** e confirme que estão em estado Red
4. **Solicite a refatoração** referenciando o CLAUDE.MD atualizado
5. **Execute todos os testes** (unitários + integração) e confirme Green
6. **Revise as mudanças** em todos os serviços afetados antes de aceitar

### 4.5 Execução de Testes Cruzados

Configure um comando para executar todos os testes do monorepo:

```bash
# Exemplo com npm workspaces
npm run test --workspaces

# Ou com um script customizado
./scripts/test-all.sh
```

Esse comando deve ser executado antes de qualquer merge ou deploy.

### 4.6 Documentação de Mudanças de Contrato

Toda mudança de contrato entre serviços deve:

1. Ser documentada no `CLAUDE.MD` como um novo ADR
2. Incluir a versão anterior e a versão nova
3. Listar todos os serviços impactados

---

## Checklist da Fase 4

- [ ] Estrutura de monorepo configurada
- [ ] Contratos entre serviços documentados no `CLAUDE.MD`
- [ ] Testes de integração escritos para cada par de serviços que se comunicam
- [ ] Comando de testes globais configurado e funcionando
- [ ] Mudanças de contrato documentadas como ADRs
- [ ] Todos os serviços impactados identificados antes de cada refatoração
- [ ] Testes cruzados executados e verdes antes de cada merge

---

## Erros Comuns a Evitar

| Erro | Consequência | Correção |
|------|-------------|----------|
| Usar múltiplos repositórios | IA perde contexto global, refatorações parciais | Migre para monorepo |
| Não ter testes de integração | Quebras de contrato chegam silenciosamente à produção | Escreva testes de integração |
| Refatorar sem atualizar o CLAUDE.MD | IA propõe mudanças baseadas em uma realidade desatualizada | Sempre atualize antes de refatorar |
| Aceitar refatoração sem revisar todos os serviços | Serviços esquecidos ficam com código inconsistente | Liste todos os impactados antes de começar |

---

*Fase anterior: [Fase 3 — Segurança e Isolamento](./phase-3-security.md)*  
*Voltar ao início: [README](../../README.md)*
