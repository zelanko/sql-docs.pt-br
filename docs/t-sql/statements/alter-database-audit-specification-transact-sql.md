---
description: ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
title: ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_AUDIT_SPECIFICATION_TSQL
- ALTER DATABASE AUDIT SPECIFICATION
- ALTER_DATABASE_AUDIT_TSQL
- ALTER DATABASE AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE AUDIT SPECIFICATION statement
ms.assetid: 85f4e7e6-a330-4de0-9048-64f386ccc314
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 98ac18629fc8765c314abd799364fd542e25c5da
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128123"
---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera um objeto de especificação de auditoria de banco de dados usando o recurso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ALTER DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } (   
           { <audit_action_specification> | audit_action_group_name }   
                )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      <action_specification>[ ,...n ] ON [ class :: ] securable   
     BY principal [ ,...n ]   
}  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *audit_specification_name*  
 O nome da especificação de auditoria.  
  
 *audit_name*  
 O nome da auditoria à qual essa especificação se aplica.  
  
 *audit_action_specification*  
 Nome de uma ou mais ações auditáveis em nível de banco de dados. Para obter uma lista de grupos de ações de auditoria, consulte [Ações e grupos de ações de auditoria do SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *audit_action_group_name*  
 Nome de um ou mais grupos de ações auditáveis em nível de banco de dados. Para obter uma lista de grupos de ações de auditoria, consulte [Ações e grupos de ações de auditoria do SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *class*  
 Nome de classe (se aplicável) no protegível.  
  
 *securable*  
 Tabela, exibição ou outro objeto protegível no banco de dados no qual aplicar a ação de auditoria ou grupo de ações de auditoria. Para obter mais informações, consulte [Securables](../../relational-databases/security/securables.md).  
  
 *column*  
 Nome da coluna (se aplicável) no protegível.  
  
 *principal*  
 Nome da entidade  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual aplicar a ação de auditoria ou grupo de ações de auditoria. Para obter mais informações, consulte [Entidades de segurança &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
 WITH **(** STATE **=** { ON | OFF } **)**  
 Habilita ou desabilita a auditoria de registros de coleta para essa especificação de auditoria. As alterações no estado da especificação de auditoria devem ser feitas fora de uma transação de usuário e não pode haver outras alterações na mesma instrução quando a transição é de ON para OFF.  
  
## <a name="remarks"></a>Comentários  
 As especificações de auditoria de banco de dados são objetos não protegidos que residem em um determinado banco de dados. É necessário definir o estado de uma especificação de auditoria com a opção OFF para fazer alterações em uma especificação de auditoria de banco de dados. Se ALTER DATABASE AUDIT SPECIFICATION for executada quando uma auditoria estiver habilitada com qualquer opção diferente de STATE=OFF, você receberá uma mensagem de erro. Para obter mais informações, confira [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
## <a name="permissions"></a>Permissões  
 Os usuários com a permissão ALTER ANY DATABASE AUDIT podem alterar especificações de auditoria de banco de dados e associá-las a qualquer auditoria.  
  
 Após a criação de uma especificação de auditoria de banco de dados, ela pode ser exibida por entidades de segurança com as permissões CONTROL SERVER ou ALTER ANY DATABASE AUDIT, com a conta sysadmin ou com entidades de segurança que têm acesso explícito à auditoria.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera uma especificação de auditoria de banco de dados denominada `HIPAA_Audit_DB_Specification` que audita as instruções `SELECT` pelo usuário `dbo`, para uma auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada `HIPAA_Audit`.  
  
```sql  
ALTER DATABASE AUDIT SPECIFICATION HIPAA_Audit_DB_Specification  
FOR SERVER AUDIT HIPAA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 Para obter um exemplo completo de como criar uma auditoria, consulte [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  
