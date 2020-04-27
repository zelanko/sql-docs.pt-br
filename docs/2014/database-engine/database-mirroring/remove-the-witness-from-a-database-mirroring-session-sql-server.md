---
title: Remover a testemunha de uma sessão de espelhamento de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], turning off
- witness [SQL Server], removing
- database mirroring [SQL Server], witness
ms.assetid: f3ce7afc-8936-4d35-80ce-d0f8fbc318d3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0fee60fa1a78c2d6d0becb63b2319105016adf1c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754672"
---
# <a name="remove-the-witness-from-a-database-mirroring-session-sql-server"></a>Remover a testemunha de uma sessão de espelhamento de banco de dados (SQL Server)
  Este tópico descreve como remover uma testemunha de uma sessão de espelhamento de banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em qualquer momento durante uma sessão de espelhamento de banco de dados, o proprietário do banco de dados pode desativar a testemunha da sessão de espelhamento de banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para Substituir, remova a testemunha, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de remover a testemunha](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-remove-the-witness"></a>Para remover a testemunha  
  
1.  Conecte-se à instância do servidor principal e, no painel **Pesquisador de Objetos** , clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e selecione o banco de dados cuja testemunha deseja remover.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Espelhar**. Isso abre a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  Para remover o servidor testemunha, exclua seu endereço de rede do campo **Testemunha** .  
  
    > [!NOTE]  
    >  Se você mudar do modo de alta segurança com failover automático para o modo de alto desempenho, o campo **Testemunha** será desmarcado automaticamente.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-remove-the-witness"></a>Para remover a testemunha  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] em qualquer instância de servidor de parceiro.  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Emita a seguinte instrução:  
  
     [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) *database_name* SET WITNESS OFF  
  
     em que *database_name* é o nome do banco de dados espelhado.  
  
     O exemplo a seguir remove a testemunha do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET WITNESS OFF ;  
    ```  
  
##  <a name="follow-up-after-removing-the-witness"></a><a name="FollowUp"></a>Acompanhamento: depois de remover a testemunha  
 A desativação da testemunha altera o [modo operacional](database-mirroring-operating-modes.md)conforme a configuração de segurança da transação:  
  
-   Se segurança de transação estiver definida como FULL (o padrão), a sessão usará o modo síncrono de alta proteção sem failover automático.  
  
-   Se a segurança de transação estiver definida como OFF, a sessão irá operar de modo assíncrono (em modo de alto desempenho) sem exigir quorum. Sempre que a segurança de transação estiver desativada, é recomendável desativar também a testemunha.  
  
> [!TIP]  
>  A configuração de segurança de transação do banco de dados é registrada em cada parceiro na exibição de catálogo [sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) nas colunas **mirroring_safety_level** e **mirroring_safety_level_desc**.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [Adicionar ou substituir uma testemunha de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Alterar a segurança da transação em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)   
 [Adicionar uma testemunha de espelhamento de banco de dados usando a autenticação do Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)   
 [Testemunha de espelhamento de banco de dados](database-mirroring-witness.md)  
  
  
