# WORKFLOW
SIGUIR ESSE CHECKLIST ANTES DE QUALQUER REALIZAÇÃO OPERACIONAL


Skill: Engenharia de Prompt e Desenvolvimento "Anti-Vibe Coding" (Akita Way)
Esta técnica foca em como um engenheiro de software deve interagir com uma IA para construir sistemas, tratando a IA como um colaborador técnico e não como um oráculo gerador de código pronto. O objetivo é evitar o "vibe coding" (aceitar cegamente sugestões) e manter o controle total da arquitetura e da qualidade.
Princípios Fundamentais
Disciplina > Intuição: Não confie na intuição da IA. Use a sua disciplina técnica para estruturar o problema antes de solicitar qualquer código.
O "Anti-Vibe Coding": Nunca aceite uma resposta da IA sem antes analisar, validar e entender se ela faz sentido dentro do contexto do seu sistema.
Planejamento Antes da Execução: A IA deve ser usada para acelerar a implementação, mas o design da arquitetura, a definição dos serviços e os requisitos devem ser feitos pelo humano.
O Fluxo de Trabalho (Akita Way)
Para aplicar esta técnica, siga este fluxo rigoroso de desenvolvimento:
Fase 1: Fundação e Estrutura
Arquitetura e Domínio: Defina o domínio do problema. Saiba exatamente quais componentes você precisa (DB, APIs externas, serviços).
CLAUDE.MD (A Spec que Evolui): Crie um arquivo de especificação (CLAUDE.MD) dentro do seu projeto. Documente nele:
Stack tecnológica, variáveis de ambiente e estrutura de diretórios.
A responsabilidade de cada serviço e modelo.
Importante: Abuse da memória desse arquivo. Insira nele todas as decisões de design e regras de negócio conforme elas evoluem.
Fase 2: Desenvolvimento com TDD
TDD como Rede de Segurança: Com IA, o TDD é mais importante, não menos.
Exija Testes Primeiro: Antes de pedir para a IA escrever qualquer implementação, solicite a criação dos testes unitários/integrados para aquela feature.
Recusa Ativa: Se a IA tentar sugerir uma implementação sem os respectivos testes, recuse e exija os testes. O código só é aceito se passar nos testes escritos antes dele.
Mão na Massa: Se a IA alucinar ou divergir, tome o controle: pare a IA, desative a sugestão automática (code completion) e edite o código manualmente no editor.
Fase 3: Segurança e Isolamento
AI-Jail (Sandboxing): Nunca execute a IA diretamente na sua máquina local de forma desenfreada. Utilize Docker Containers para isolar o ambiente de execução da IA, protegendo seu sistema de arquivos e configurações sensíveis.
Modelo de Permissões: Ao usar agentes (como Claude Code), certifique-se de restringir os acessos e monitorar cada comando que a IA tenta executar no terminal.
Fase 4: Refatoração Multisserviço
Contexto Compartilhado: Use uma estrutura de Monorepo. Isso permite que a IA tenha uma visão global de todos os seus serviços, facilitando refatorações que afetam múltiplos pontos do sistema.
Execução de Testes Cruzados: Utilize testes de integração para validar a comunicação entre serviços. Se um serviço altera a estrutura de dados, o teste de integração entre o consumidor e o provedor deve falhar imediatamente.
Dicas para o Sucesso
Não busque atalhos: A técnica não é sobre "criar um SaaS em 10 minutos". É sobre construir um sistema robusto e manutenível.
O "One-Shot Prompt" é um mito: Esqueça a ideia de que um único prompt mágico resolverá tudo. O processo é iterativo: Planejamento -> Documentação -> TDD -> Implementação -> Refatoração -> Deploy.
Documentação é Código: Se algo mudou na arquitetura, atualize o CLAUDE.MD antes de prosseguir com a IA. Isso mantém a IA "alinhada" com a realidade do projeto.
