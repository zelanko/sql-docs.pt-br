---
title: Modificar ou renomear gatilhos DML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 824ea1587955884f10a53579865d2029cc63eefc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62473217"
---
# <a name="modify-or-rename-dml-triggers"></a>Modificar ou renomear gatilhos DML
  Este tópico descreve como modificar um gatilho DML no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para modificar ou renomear um gatilho DML usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Quando você renomeia um gatilho, o gatilho deve estar no banco de dados atual e o novo nome deve seguir as regras para [identificadores](../databases/database-identifiers.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Recomendamos que você não use o procedimento armazenado [sp_rename](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql) para renomear um gatilho. A alteração de qualquer parte de um nome de objeto pode quebrar scripts e procedimentos armazenados. Renomear um gatilho não altera o nome do objeto correspondente na coluna de definição da exibição de catálogo [sys.sql_modules](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql) . Nós recomendamos que você remova e recrie o gatilho.  
  
-   Se você alterar o nome de um objeto referenciado por um gatilho DML, é preciso modificar o gatilho para que seu texto reflita o novo nome. Portanto, antes de renomear um objeto, exiba primeiramente as dependências do objeto para determinar se algum gatilho foi afetado pela mudança proposta.  
  
-   Um gatilho DML também pode ser modificado para criptografar sua definição.  
  
-   Para exibir as dependências de um gatilho, você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou a função e as exibições de catálogo a seguir:  
  
    -   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
    -   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
    -   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A alteração de um gatilho DML exige permissão ALTER na tabela ou exibição na qual o gatilho está definido.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-dml-trigger"></a>Para modificar um gatilho DML  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda o banco de dados que você quer, expanda **Tabelas**e expanda a tabela que contém o gatilho que você quer modificar.  
  
3.  Expanda **Gatilhos**, clique com o botão direito do mouse no gatilho a ser modificado e clique em **Modificar**.  
  
4.  Modifique o gatilho e clique em **Executar**.  
  
#### <a name="to-rename-a-dml-trigger"></a>Para renomear um gatilho DML  
  
1.  [Exclua o gatilho](../triggers/dml-triggers.md) que você deseja renomear.  
  
2.  [Recrie o gatilho](../triggers/create-dml-triggers.md), especificando o novo nome.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>Para modificar um gatilho usando ALTER TRIGGER  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os seguintes exemplos na consulta. Execute o primeiro exemplo para criar um gatilho DML que imprime uma mensagem definida pelo usuário para o cliente quando um usuário tenta adicionar ou alterar dados na tabela `SalesPersonQuotaHistory` . Execute a instrução [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) para modificar o gatilho a ser disparado apenas nas atividades `INSERT` . Esse gatilho é útil porque lembra ao usuário que atualiza ou insere linhas nessa tabela que também notifique o departamento `Compensation` .  
  
```sql  
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
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>Para renomear um gatilho usando DROP TRIGGER e ALTER TRIGGER  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa as instruções [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) e [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) para renomear o gatilho `Sales.bonus_reminder` como `Sales.bonus_reminder_2`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [Obter informações sobre gatilhos DML](../triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
  
