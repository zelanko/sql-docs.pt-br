---
title: "Obter informações sobre gatilhos DML | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [SQL Server], triggers
- viewing DML triggers
- DML triggers, metadata
- displaying DML triggers
- status information [SQL Server], triggers
- DML triggers, viewing
ms.assetid: 37574aac-181d-4aca-a2cc-8abff64237dc
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8583bd2597f5107398a65df65dbe7f7eef53f4d
ms.lasthandoff: 04/11/2017

---
# <a name="get-information-about-dml-triggers"></a>Obter informações sobre gatilhos DML
  Este tópico descreve como obter informações sobre os gatilhos DML no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Essas informações podem incluir os tipos de gatilhos em uma tabela, o nome de um gatilho, seu proprietário e a data em que foi criado ou modificado. Se o gatilho não tiver sido criptografado quando foi criado, você obterá a definição do gatilho. A definição ajudará a entender como um gatilho afeta a tabela na qual está definido. Além disso, você pode descobrir os objetos que um gatilho específico usa. Com essas informações, você pode identificar os objetos que afetam o gatilho se eles são alterados ou excluídos do banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para obter informações os gatilhos DML, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 **sys.sql.modules**, **sys.object**, **sys.triggers**, **sys.events**, **sys.trigger_events**  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 OBJECT_DEFINITION, OBJECTPROPERTY, **sp_helptext**  
 Requer associação à função **pública** . A definição de objetos de usuário é visível ao proprietário do objeto e aos que possuírem qualquer uma das seguintes permissões: ALTER, CONTROL, TAKE OWNERSHIP ou VIEW DEFINITION. Estas permissões são mantidas implicitamente por membros das funções fixas de banco de dados **db_owner**, **db_ddladmin**e **db_securityadmin** .  
  
 **sys.sql_expression_dependencies**  
 Requer permissão VIEW DEFINITION no banco de dados e permissão SELECT em **sys.sql_expression_dependencies** para o banco de dados. Por padrão, a permissão SELECT é concedida somente a membros da função de banco de dados fixa **db_owner** . Quando são concedidas permissões SELECT e VIEW DEFINITION a outro usuário, o usuário autorizado pode exibir todas as dependências no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>Para exibir a definição de um gatilho DML  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda o banco de dados desejado, expanda **Tabelas**e expanda a tabela que contém o gatilho para o qual você quer exibir a definição.  
  
3.  Expanda **Gatilhos**, clique com o botão direito do mouse no gatilho desejado e clique em **Modificar**. A definição do gatilho DML aparece na janela de consulta.  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>Para exibir as dependências de um gatilho DML  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda o banco de dados desejado, expanda **Tabelas**e expanda a tabela que contém o gatilho e suas dependências que você quer exibir.  
  
3.  Expanda **Gatilhos**, clique com o botão direito do mouse no gatilho desejado e clique em **Exibir Dependências**.  
  
4.  Na janela **Dependências de objeto**, para exibir os objetos que dependem do gatilho DML, selecione **Objetos que dependem de \<nome do gatilho DML>**. Os objetos aparecem na área **Dependências** .  
  
     Para exibir os objetos dos quais o DML depende, selecione **Objetos que dependem de \<nome do gatilho DML>**. Os objetos aparecem na área **Dependências** . Expanda cada nó para ver todos os objetos.  
  
5.  Para obter informações sobre um objeto que aparece na área **Dependências** , clique no objeto. No campo **Objeto selecionado** , as informações são fornecidas nas caixas **Nome**, **Tipo**e **Tipo de dependência** .  
  
6.  Para fechar a janela **Dependências do Objeto** , clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>Para exibir a definição de um gatilho DML  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**. Cada exemplo mostra como você pode exibir a definição do gatilho `iuPerson` .  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT definition   
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID(N'Person.iuPerson');   
GO  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.iuPerson')) AS ObjectDefinition;   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
EXEC sp_helptext 'Person.iuPerson'  
GO  
  
```  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>Para exibir as dependências de um gatilho DML  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**. Cada exemplo mostra como você pode exibir as dependências do gatilho `iuPerson` .  
  
```  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,   
    referenced_server_name, referenced_database_name, referenced_schema_name,   
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,   
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Person.iuPerson');   
GO  
  
```  
  
#### <a name="to-view-information-about-dml-triggers-in-the-database"></a>Para exibir informações sobre os gatilhos DML no banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**. Cada exemplo mostra como você pode exibir informações sobre os gatilhos DML (`TR`) no banco de dados.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT  name, parent_id, create_date, modify_date, is_instead_of_trigger  
FROM sys.triggers  
WHERE type = 'TR';   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT  name, object_id, schema_id, parent_object_id, type_desc, create_date, modify_date, is_published  
FROM sys.objects  
WHERE type = 'TR';   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'Person.iuPerson'), 'ExecIsInsteadOfTrigger');   
GO  
  
```  
  
#### <a name="to-view-information-about-events-that-fire-a-dml-trigger"></a>Para exibir informações sobre os eventos que acionam um gatilho DML  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**. Cada exemplo mostra como você pode exibir os eventos que disparam o gatilho `iuPerson` .  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT object_id, type, type_desc, is_trigger_event, event_group_type, event_group_type_desc   
FROM sys.events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
```tsql  
USE AdventureWorks2012;   
GO   
SELECT object_id, type,is_first, is_last  
FROM sys.trigger_events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
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
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
  
