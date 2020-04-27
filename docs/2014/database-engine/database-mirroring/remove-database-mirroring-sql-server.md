---
title: Remover o Espelhamento de Banco de Dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d398c2c9d8439025c7ff5ec7a8e4295b24d337
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754685"
---
# <a name="remove-database-mirroring-sql-server"></a>Remover o espelhamento de banco de dados (SQL Server)
  Este tópico descreve como remover o espelhamento de um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  A qualquer momento, o proprietário do banco de dados poderá interromper manualmente uma sessão de espelhamento de banco de dados ao remover o espelhamento de banco de dados.  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-remove-database-mirroring"></a>Para remover o espelhamento de banco de dados  
  
1.  Durante uma sessão de espelhamento de banco de dados, faça a conexão com a instância do servidor principal e, no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e selecione o banco de dados.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Espelhar**. Isso abre a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  No painel **Selecionar uma Página** , clique em **Espelhamento**.  
  
5.  Para remover o espelhamento, clique em **Remover Espelhamento**. Um prompt solicita confirmação. Se você clicar em **Sim**, a sessão será interrompida e o espelhamento, removido do banco de dados.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Para remover o espelhamento de banco de dados, use **Propriedades do Banco de Dados**. Use a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
#### <a name="to-remove-database-mirroring"></a>Para remover o espelhamento de banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] de qualquer um dos parceiros de espelhamento.  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Emita a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     em que *database_name* é o banco de dados espelhado cuja sessão você deseja remover.  
  
     O exemplo a seguir remove o espelhamento de banco de dados do banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="follow-up-removing-database-mirroring"></a><a name="FollowUp"></a> Acompanhamento: removendo o espelhamento de banco de dados  
  
> [!NOTE]  
>  Para obter informações sobre o impacto da remoção de espelhamentos, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
-   **Se você pretender reiniciar o espelhamento no banco de dados**  
  
     Todos os backups de logs efetuados no banco de dados principal depois que o espelhamento for removido deverão ser aplicados ao banco de dados espelho antes que o espelhamento de banco de dados possa ser reinicializado.  
  
-   **Se você não pretender reiniciar o espelhamento**  
  
     Opcionalmente, você pode recuperar o banco de dados espelho anterior. Na instância de servidor que era o servidor espelho, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  Se você recuperar este banco de dados, dois bancos de dados divergentes com o mesmo nome estarão online. Portanto, você precisa garantir que os clientes possam acessar somente um deles – geralmente o banco de dados principal mais recente.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Pausar ou retomar uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [Remover a testemunha de uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
-   [Exemplo: configurando o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server de espelhamento de banco de dados &#40;&#41;](database-mirroring-sql-server.md)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
