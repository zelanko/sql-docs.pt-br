---
title: Tarefa Atualização de Estatísticas (Plano de manutenção) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.statistics.f1
helpviewer_keywords:
- Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 486ef2da96785ed200900f497435117ef6437cb5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023865"
---
# <a name="update-statistics-task-maintenance-plan"></a>Tarefa Atualização de Estatísticas (Plano de manutenção)
  Use a caixa de diálogo **Tarefa Atualizar Estatísticas** para atualizar informações do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre os dados nas tabelas e nos índices. Essa tarefa cria uma nova amostra das estatísticas de distribuição de cada índice criado em tabelas de usuário no banco de dados. As estatísticas de distribuição são usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para otimizar a navegação em tabelas durante o processamento de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para construir as estatísticas de distribuição automaticamente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz uma amostra periódica dos dados na tabela correspondente para cada índice. O tamanho da amostra tem como base o número de linhas na tabela e a frequência de modificação dos dados. Use essa opção para executar uma amostragem adicional usando a porcentagem de dados especificada nas tabelas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa estas informações para criar planos de consulta melhores.  
  
 Essa tarefa executa a instrução UPDATE STATISTICS.  
  
## <a name="options"></a>Opções  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Novo**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Bancos de dados**  
 Especifique os bancos de dados afetados por essa tarefa.  
  
-   **Todos os bancos de dados**  
  
     Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto tempdb.  
  
-   **Todos os bancos de dados do sistema**  
  
     Gera um plano de manutenção que execute tarefas de manutenção em cada banco de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto o tempdb. Nenhuma tarefa de manutenção é executada nos bancos de dados criados pelo usuário.  
  
-   **Todos os bancos de dados de usuários**  
  
     Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados criados por usuários. Nenhuma tarefa de manutenção é executada com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Estes bancos de dados específicos**  
  
     Gere um plano de manutenção que execute tarefas de manutenção somente nos bancos de dados selecionados. Pelo menos um banco de dados da lista deverá ser selecionado se esta opção for escolhida.  
  
 **Observação** Planos de manutenção são executados somente em bancos de dados definidos com nível de compatibilidade 80 ou superior. Os bancos de dados definidos para o nível de compatibilidade 70 ou inferior não são exibidos.  
  
 **Objeto**  
 Limita a grade **Seleção** para exibir tabelas, exibições ou ambas.  
  
 **Seleção**  
 Especifique as tabelas ou índices afetados por esta tarefa. Não disponível quando **Tabelas e Exibições** estiver selecionado na caixa Objeto.  
  
 **Todas as estatísticas existentes**  
 Atualize as estatísticas de colunas e índices.  
  
 **Somente estatísticas de coluna**  
 Atualiza apenas as estatísticas de coluna.  
  
 **Somente estatísticas do índice**  
 Só atualiza estatísticas do índice.  
  
 **Tipo de exame**  
 Tipo de exame usado para coletar estatísticas atualizadas.  
  
 **Exame completo**  
 Lê todas as linhas na tabela ou exibição para coletar as estatísticas.  
  
 **Amostra por**  
 Especifique a porcentagem da tabela ou exibição indexada ou o número de linhas de amostragem ao coletar estatísticas de tabelas ou exibições maiores.  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## <a name="new-connection-dialog-box"></a>Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **Atualizar**  
 Atualize a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] com a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  
