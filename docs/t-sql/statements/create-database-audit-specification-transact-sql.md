---
title: CREATE DATABASE AUDIT SPECIFICATION
description: Crie um objeto de especificação de auditoria do banco de dados usando o recurso de auditoria do SQL Server.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 01/03/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE DATABASE AUDIT
- DATABASE_AUDIT_SPECIFICATION_TSQL
- DATABASE AUDIT SPECIFICATION
- CREATE_DATABASE_AUDIT_SPECIFICATION_TSQL
- CREATE_DATABASE_AUDIT_TSQL
- CREATE DATABASE AUDIT SPECIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- database audit specification
- CREATE DATABASE AUDIT SPECIFICATION statement
ms.assetid: 0544da48-0ca3-4a01-ba4c-940e23dc315b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3d34a4b7913baa074ba3cc5aaca44c87e8c8ff75
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895470"
---
# <a name="create-database-audit-specification-transact-sql"></a>CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria um objeto de especificação de auditoria de banco de dados usando o recurso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
CREATE DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    FOR SERVER AUDIT audit_name   
        [ { ADD ( { <audit_action_specification> | audit_action_group_name } )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      action [ ,...n ]ON [ class :: ] securable BY principal [ ,...n ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *audit_specification_name*  
 É o nome da especificação de auditoria do servidor.  
  
 *audit_name*  
 É o nome da auditoria à qual esta especificação é aplicada.  
  
 *audit_action_specification*  
 A especificação de ações em protegíveis por entidades que devem ser registradas na auditoria.  
  
 *action*  
 O nome de um ou mais ações auditáveis em nível de banco de dados. Para obter uma lista de ações de auditoria, consulte [Ações e grupos de ação do SQL Server Audit](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *audit_action_group_name*  
 O nome de um ou mais grupos de ações auditáveis em nível de banco de dados. Para obter uma lista de grupos de ações de auditoria, consulte [Ações e grupos de ações de auditoria do SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *class*  
 O nome da classe (se aplicável) no protegível.  
  
 *securable*  
 A tabela, exibição ou outro objeto protegível no banco de dados no qual aplicar a ação de auditoria ou o grupo de ações de auditoria. Para obter mais informações, consulte [Securables](../../relational-databases/security/securables.md).  
  
 *principal*  
 É o nome da entidade de segurança do banco de dados na qual aplicar a ação de auditoria ou o grupo de ações de auditoria. Para auditar todas as entidades de segurança do banco de dados, use a entidade de segurança do banco de dados `public`. Para obter mais informações, consulte [Entidades de segurança &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
 WITH ( STATE = { ON | OFF } )  
 Habilita ou desabilita a auditoria de registros de coleta para essa especificação de auditoria.  
  
## <a name="remarks"></a>Comentários  
 As especificações de auditoria de banco de dados são objetos não protegidos que residem em um determinado banco de dados. Quando uma especificação de auditoria de banco de dados é criada, ela fica em um estado desabilitado.  
  
## <a name="permissions"></a>Permissões  
 Os usuários com a permissão `ALTER ANY DATABASE AUDIT` podem criar especificações de auditoria de banco de dados e associá-las a qualquer auditoria.  
  
 Após a criação de uma especificação de auditoria de banco de dados, ela pode ser exibida pelas entidades de segurança com as permissões `CONTROL SERVER`, `ALTER ANY DATABASE AUDIT` ou a conta `sysadmin`.  
  
## <a name="examples"></a>Exemplos

### <a name="a-audit-select-and-insert-on-a-table-for-any-database-principal"></a>a. Auditar SELECT e INSERT em uma tabela para qualquer entidade de segurança do banco de dados 
 O exemplo a seguir cria uma auditoria de servidor chamada `Payrole_Security_Audit` e, em seguida, uma especificação de auditoria de banco de dados chamada `Payrole_Security_Audit` que audita instruções `SELECT` e `INSERT` pelo usuário `dbo`, para a tabela `HumanResources.EmployeePayHistory` no banco de dados `AdventureWorks2012`.  
  
```  
USE master ;  
GO  
-- Create the server audit.  
CREATE SERVER AUDIT Payrole_Security_Audit  
    TO FILE ( FILEPATH =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;  
GO  
-- Enable the server audit.  
ALTER SERVER AUDIT Payrole_Security_Audit   
WITH (STATE = ON) ;  
GO  
-- Move to the target database.  
USE AdventureWorks2012 ;  
GO  
-- Create the database audit specification.  
CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
FOR SERVER AUDIT Payrole_Security_Audit  
ADD (SELECT , INSERT  
     ON HumanResources.EmployeePayHistory BY dbo )  
WITH (STATE = ON) ;  
GO  
``` 

### <a name="b-audit-any-dml-insert-update-or-delete-on-_all_-objects-in-the-_sales_-schema-for-a-specific-database-role"></a>B. Faça a auditoria de qualquer DML (INSERT, UPDATE ou DELETE) em _todos_ os objetos no esquema _vendas_ para uma função de banco de dados específica  
 O exemplo a seguir cria uma auditoria de servidor denominada `DataModification_Security_Audit` e, em seguida, uma especificação de auditoria de banco de dados chamada `Audit_Data_Modification_On_All_Sales_Tables` que audita instruções `INSERT`, `UPDATE` e `DELETE` por usuários em uma nova função de banco de dados `SalesUK`, para todos os objetos no esquema `Sales` no banco de dados `AdventureWorks2012`.  
  
```  
USE master ;  
GO  
-- Create the server audit.
-- Change the path to a path that the SQLServer Service has access to. 
CREATE SERVER AUDIT DataModification_Security_Audit  
    TO FILE ( FILEPATH = 
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ; 
GO  
-- Enable the server audit.  
ALTER SERVER AUDIT DataModification_Security_Audit   
WITH (STATE = ON) ;  
GO  
-- Move to the target database.  
USE AdventureWorks2012 ;  
GO  
CREATE ROLE SalesUK
GO
-- Create the database audit specification.  
CREATE DATABASE AUDIT SPECIFICATION Audit_Data_Modification_On_All_Sales_Tables  
FOR SERVER AUDIT DataModification_Security_Audit  
ADD ( INSERT, UPDATE, DELETE  
     ON Schema::Sales BY SalesUK )  
WITH (STATE = ON) ;    
GO  
```  


## <a name="see-also"></a>Consulte Também  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
