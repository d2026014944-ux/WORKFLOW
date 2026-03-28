# Fase 2 — Desenvolvimento com TDD

> **Objetivo:** Garantir que todo código gerado — por humano ou IA — seja validado por testes escritos previamente.  
> Com IA no processo, TDD é **mais importante**, não menos.

---

## Por Que TDD é Inegociável com IA

A IA pode gerar código que:
- Compila sem erros mas produz resultados incorretos
- Funciona para o caso de teste do prompt mas quebra em casos reais
- Parece correto mas viola regras de negócio documentadas

Testes escritos **antes** da implementação são a rede de segurança que captura esses problemas automaticamente.

---

## O Ciclo Red → Green → Refactor

```
RED    → Escreva o teste. Ele deve FALHAR (o código ainda não existe).
GREEN  → Implemente o mínimo de código para o teste PASSAR.
REFACTOR → Melhore o código mantendo todos os testes VERDES.
```

**Regra:** Nunca aceite um passo "Green" sem ter passado pelo "Red" primeiro.

---

## Etapas

### 2.1 Solicitar Testes Antes da Implementação

Ao usar a IA para desenvolver uma feature, o prompt deve ser:

```
"Crie os testes unitários e de integração para [feature X], 
considerando os seguintes casos de uso: [lista de casos].
NÃO implemente a feature ainda."
```

**Recuse Ativamente:** Se a IA sugerir implementação antes dos testes, recuse explicitamente e exija os testes primeiro.

### 2.2 Validar os Testes (Fase Red)

Antes de qualquer implementação:

1. Execute os testes recém-criados
2. Confirme que **todos falham** (se algum passar, o teste não está testando nada útil)
3. Analise se os testes cobrem os casos de uso definidos no `CLAUDE.MD`

### 2.3 Solicitar a Implementação

Com os testes validados em estado Red, solicite a implementação:

```
"Agora implemente [feature X] para que os testes escritos anteriormente passem.
Siga as regras de negócio documentadas no CLAUDE.MD."
```

### 2.4 Validar a Implementação (Fase Green)

1. Execute os testes
2. Confirme que **todos passam**
3. Analise o código gerado — entenda cada linha antes de aceitar
4. Verifique se a implementação segue a arquitetura definida no `CLAUDE.MD`

### 2.5 Refatorar (Fase Refactor)

Com todos os testes verdes:

1. Identifique duplicações, complexidade desnecessária ou violações de padrões
2. Solicite ou faça manualmente a refatoração
3. Execute os testes novamente para confirmar que continuam verdes

### 2.6 Intervenção Manual

Se a IA alucinar, divergir do contexto ou gerar código inconsistente:

1. **Pare a IA** — não continue o diálogo no mesmo contexto
2. **Desative o autocomplete** (code completion) no editor
3. **Edite manualmente** as partes incorretas
4. Documente o que aconteceu no `CLAUDE.MD` para orientar futuras interações

---

## Tipos de Testes

| Tipo | Quando Usar | O Que Valida |
|------|-------------|-------------|
| **Unitário** | Para cada função/método isolado | Lógica interna, casos de borda |
| **Integração** | Para interação entre módulos ou serviços | Contratos de dados, fluxos completos |
| **E2E** | Para fluxos críticos do usuário | Comportamento do sistema como um todo |

---

## Checklist da Fase 2

- [ ] Testes solicitados e escritos **antes** de qualquer implementação
- [ ] Testes executados e confirmados em estado Red
- [ ] Implementação solicitada com referência ao `CLAUDE.MD`
- [ ] Implementação executada e todos os testes em estado Green
- [ ] Código analisado e entendido antes de ser aceito
- [ ] Refatoração realizada com testes ainda verdes

---

## Erros Comuns a Evitar

| Erro | Consequência | Correção |
|------|-------------|----------|
| Aceitar implementação sem testes | Código sem validação, bugs silenciosos | Exija sempre os testes primeiro |
| Não verificar o estado Red | Testes que sempre passam não testam nada | Execute antes de implementar |
| Confiar no código sem ler | IA pode gerar código que parece correto mas viola regras | Leia e entenda cada linha |
| Ignorar alucinações | Contexto corrompido leva a mais alucinações | Pare, reinicie e edite manualmente |

---

*Fase anterior: [Fase 1 — Fundação e Estrutura](./phase-1-foundation.md)*  
*Próxima fase: [Fase 3 — Segurança e Isolamento](./phase-3-security.md)*
