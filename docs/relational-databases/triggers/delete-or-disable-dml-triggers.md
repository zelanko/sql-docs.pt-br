---
title: Excluir ou desabilitar gatilhos DML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: triggers
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DML triggers, disabling
- removing DML triggers
- disabling DML triggers
- dropping DML triggers
- deleting DML triggers
- DML triggers, removing
ms.assetid: 0f97f953-33c5-4b26-afeb-db2a26ce38b4
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bca0580d442c30bc41d46340b3317cbe15515309
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="delete-or-disable-dml-triggers"></a>Excluir ou desabilitar gatilhos DML
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] Este tópico descreve como excluir ou desabilitar um gatilho DML no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para excluir ou desabilitar um gatilho DML, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Quando um gatilho é excluído, ele é descartado do banco de dados atual. A tabela e os dados nos quais está baseada não são afetados. Excluir uma tabela exclui automaticamente todos os gatilhos da tabela.  
  
-   Um gatilho é habilitado por padrão quando é criado.  
  
-   Ao desabilitar um gatilho, você não o descarta. O gatilho ainda existe como um objeto no banco de dados atual. Porém, o gatilho não será acionado quando qualquer instrução INSERT, UPDATE ou DELETE, em que ele tenha sido programado, for executada. Os gatilhos desabilitados podem ser habilitados novamente. A habilitação de um disparador não recria o mesmo. O gatilho é acionado da mesma forma como foi criado.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A exclusão de um gatilho DML requer permissão ALTER na tabela ou exibição na qual o gatilho está definido.  
  
 Para desabilitar ou habilitar um gatilho DML, no mínimo, um usuário deve ter a permissão ALTER na tabela ou exibição na qual o gatilho foi criado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-dml-trigger"></a>Para excluir um gatilho DML  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda o banco de dados que você quer, expanda **Tabelas**e expanda a tabela que contém o gatilho que você quer excluir.  
  
3.  Expanda **Gatilhos**, clique com o botão direito do mouse no gatilho para excluí-lo e clique em **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objeto** , verifique o gatilho a ser excluído e clique em **OK**.  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>Para desabilitar e habilitar um gatilho DML  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda o banco de dados que você quer, expanda **Tabelas**e expanda a tabela que contém o gatilho que você quer desabilitar.  
  
3.  Expanda **Gatilhos**, clique com o botão direito do mouse no gatilho para desabilitá-lo e clique em **Desabilitar**.  
  
4.  Para habilitar o gatilho, clique em **Habilitar**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-dml-trigger"></a>Para excluir um gatilho DML  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta. Execute a instrução [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) para criar o gatilho `Sales.bonus_reminder` . Para excluir o gatilho, execute a instrução [DROP TRIGGER](../../t-sql/statements/drop-trigger-transact-sql.md) .  
  
```sql  
--Create the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```sql  
--Delete the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('Sales.bonus_reminder', 'TR') IS NOT NULL  
   DROP TRIGGER Sales.bonus_reminder;  
GO  
  
```  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>Para desabilitar e habilitar um gatilho DML  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta. Execute a instrução [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) para criar o gatilho `Sales.bonus_reminder` . Para desabilitar e habilitar o gatilho, execute as instruções [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) e [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md) , respectivamente.  
  
```sql  
--Create the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```sql  
--Disable the trigger.  
USE AdventureWorks2012;  
GO  
DISABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
  
```  
  
```sql  
--Enable the trigger.  
USE AdventureWorks2012;  
GO  
ENABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Obter informações sobre gatilhos DML](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  
