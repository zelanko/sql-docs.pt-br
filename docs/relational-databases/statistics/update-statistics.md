---
title: "Atualizar estatísticas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating statistics
- statistics [SQL Server], updating
ms.assetid: 4b97c0b4-03ff-4cfb-9c3f-3b33290b7a2c
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fca31288577f6905b99ac2c76e018ed134f10171
ms.lasthandoff: 04/11/2017

---
# <a name="update-statistics"></a>Atualização de Estatísticas
  Você pode atualizar estatísticas de otimização de consulta em uma tabela ou exibição indexada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por padrão, o otimizador de consulta já atualiza estatísticas conforme necessário para melhorar o plano de consulta; em alguns casos, é possível melhorar o desempenho de consulta usando UPDATE STATISTICS ou o procedimento armazenado `sp_updatestats` para atualizar estatísticas com mais frequência do que as atualizações padrão.  
  
 A atualização de estatísticas assegura que as consultas sejam compiladas com estatísticas atualizadas. Porém, a atualização de estatísticas faz com que as consultas sejam recompiladas. É recomendável não atualizar estatísticas com muita frequência porque existe uma compensação de desempenho entre o aprimoramento dos planos de consulta e o tempo necessário para recompilar consultas. As compensações específicas dependem do seu aplicativo. UPDATE STATISTICS pode usar tempdb para classificar o exemplo de linhas para compilação de estatísticas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para atualizar um objeto de estatísticas, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se você estiver usando UPDATE STATISTICS ou fazendo alterações por meio de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], isso exigirá a permissão ALTER na tabela ou exibição. Se você estiver usando `sp_updatestats`, isso exigirá a associação na função de servidor fixa **sysadmin** ou a propriedade do banco de dados (**dbo**).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-update-a-statistics-object"></a>Para atualizar um objeto de estatísticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o banco de dados no qual você deseja atualizar a estatística.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja atualizar a estatística.  
  
4.  Clique no sinal de adição para expandir a pasta **Estatísticas** .  
  
5.  Clique com o botão direito do mouse no objeto de estatísticas que você deseja atualizar e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Propriedades de Estatísticas –***statistics_name* , marque a caixa de seleção **Atualizar estatísticas destas colunas** e clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-update-a-specific-statistics-object"></a>Para atualizar um objeto de estatísticas específico  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example updates the statistics for the AK_SalesOrderDetail_rowguid index of the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;   
    GO  
    ```  
  
#### <a name="to-update-all-statistics-in-a-table"></a>Para atualizar todas as estatísticas em uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all indexes on the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail;   
    GO  
    ```  
  
 Para obter mais informações, veja [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md).  
  
#### <a name="to-update-all-statistics-in-a-database"></a>Para atualizar todas as estatísticas em um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all tables in the database.   
    EXEC sp_updatestats;  
    ```  
  
 Para obter mais informações, veja [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md).  
  
  
