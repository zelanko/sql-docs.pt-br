---
title: Reduzir a tarefa do banco de dados (plano de manutenção) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Shrink Database Task
- Shrink Database(s) Task
- sql13.swb.maint.shrink.f1
helpviewer_keywords:
- Shrink Database Task dialog box
ms.assetid: a9874cac-cded-4145-9c38-8aafd267dbee
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 14cb53bcc9022fd2b960e2a7da481a02f6092a70
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="shrink-database-task-maintenance-plan"></a>Tarefa reduzir banco de dados (Plano de Manutenção)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a caixa de diálogo da **Tarefa Reduzir Banco de Dados** para criar uma tarefa que tenta reduzir o tamanho dos bancos de dados selecionados. Use as opções abaixo para determinar a quantidade de espaço não usado que permanecerá no banco de dados depois de ele ser reduzido (quanto maior a porcentagem, menos o banco de dados poderá ser reduzido). O valor é baseado na porcentagem dos dados reais no banco de dados. Por exemplo, se você reduzir um banco de dados de 100 MB contendo 60 MB de dados e 40 MB de espaço livre, com uma porcentagem de espaço livre de 50%, você ficará com 60 MB de dados e 30 MB de espaço livre (pois 50% de 60 MB são 30 MB). Somente o espaço em excesso no banco de dados é eliminado. Os valores válidos são de 0 a 100.  
  
 A redução de arquivos de dados recupera espaço com a movimentação de páginas de dados do final do arquivo para o espaço desocupado mais próximo à frente do arquivo. Quando espaço livre suficiente é criado no final do arquivo, as páginas de dados no final do arquivo podem ser desalocadas e retornadas para o sistema de arquivos.  
  
> [!WARNING]  
>  Os dados movidos para reduzir um arquivo podem ser espalhados para qualquer local disponível no arquivo. Isso provoca uma fragmentação do índice e pode reduzir a velocidade do desempenho de consultas que pesquisam um intervalo do índice. Para eliminar a fragmentação, considere a recompilação dos índices no arquivo após a redução.  
  
 Essa tarefa executa a instrução DBCC SHRINKDATABASE.  
  
## <a name="options"></a>Opções  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Nova**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Bancos de dados**  
 Especifique os bancos de dados afetados por essa tarefa.  
  
-   **Todos os bancos de dados**  
  
     Gere um plano de manutenção que executa tarefas de manutenção em todos os bancos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto tempdb.  
  
-   **Todos os bancos de dados do sistema**  
  
     Gera um plano de manutenção que execute tarefas de manutenção em cada banco de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto o tempdb. Nenhuma tarefa de manutenção é executada nos bancos de dados criados pelo usuário.  
  
-   **Todos os bancos de dados de usuários**  
  
     Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados criados por usuários. Nenhuma tarefa de manutenção é executada com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Estes bancos de dados**  
  
     Gere um plano de manutenção que execute tarefas de manutenção somente nos bancos de dados selecionados. Pelo menos um banco de dados da lista deverá ser selecionado se esta opção for escolhida.  
  
    > [!NOTE]  
    >  Os planos de manutenção são executados somente em bancos de dados definidos com nível de compatibilidade 80 ou superior. Os bancos de dados definidos para o nível de compatibilidade 70 ou inferior não são exibidos.  
  
 **Reduzir o banco de dados quando ele ultrapassar**  
 Especifique o tamanho em megabytes que faz a tarefa ser executada.  
  
 **Espaço livre após a redução**  
 Deixe de reduzir quando o espaço livre nos arquivos de banco de dados alcançar esse tamanho.  
  
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
  
 **Usar segurança Integrada do Windows NT**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] com a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção não está disponível.  
  
 **User name**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
  
  
