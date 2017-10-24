---
title: "ALTERAR a especificação de auditoria de banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06d58a9ecce3175e021e7db484aeadbe41f3b372
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera um objeto de especificação de auditoria de banco de dados usando o recurso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
  
## <a name="arguments"></a>Argumentos  
 *audit_specification_name*  
 O nome da especificação de auditoria.  
  
 *audit_name*  
 O nome da auditoria à qual essa especificação se aplica.  
  
 *audit_action_specification*  
 Nome de uma ou mais ações auditáveis em nível de banco de dados. Para obter uma lista de grupos de ação de auditoria, consulte [ações e grupos de ação de auditoria do SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *audit_action_group_name*  
 Nome de um ou mais grupos de ações auditáveis em nível de banco de dados. Para obter uma lista de grupos de ação de auditoria, consulte [ações e grupos de ação de auditoria do SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *classe*  
 Nome de classe (se aplicável) no protegível.  
  
 *protegível*  
 Tabela, exibição ou outro objeto protegível no banco de dados no qual aplicar a ação de auditoria ou grupo de ações de auditoria. Para obter mais informações, consulte [Securables](../../relational-databases/security/securables.md).  
  
 *coluna*  
 Nome da coluna (se aplicável) no protegível.  
  
 *entidade de segurança*  
 Nome da entidade  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual aplicar a ação de auditoria ou grupo de ações de auditoria. Para obter mais informações, consulte [entidades &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
 COM **(** ESTADO  **=**  {ON | OFF} **)**  
 Habilita ou desabilita a auditoria de registros de coleta para essa especificação de auditoria. As alterações no estado da especificação de auditoria devem ser feitas fora de uma transação de usuário e não pode haver outras alterações na mesma instrução quando a transição é de ON para OFF.  
  
## <a name="remarks"></a>Comentários  
 As especificações de auditoria de banco de dados são objetos não protegidos que residem em um determinado banco de dados. Você deve definir o estado de uma especificação de auditoria para a opção OFF para fazer alterações em um banco de dados a especificação de auditoria. Se ALTER DATABASE AUDIT SPECIFICATION for executada quando uma auditoria estiver habilitada com qualquer opção diferente de STATE=OFF, você receberá uma mensagem de erro. Para obter mais informações, confira [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
## <a name="permissions"></a>Permissões  
 Os usuários com a permissão ALTER ANY DATABASE AUDIT podem alterar especificações de auditoria de banco de dados e associá-las a qualquer auditoria.  
  
 Depois que uma especificação de auditoria de banco de dados é criada, ela pode ser exibida por entidades com o servidor de controle, ou permissões ALTER ANY DATABASE AUDIT, a conta sysadmin ou entidades que tenham acesso explícito à auditoria.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera uma especificação de auditoria de banco de dados denominada `HIPPA_Audit_DB_Specification` que audita as instruções `SELECT` pelo usuário `dbo`, para uma auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada `HIPPA_Audit`.  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPPA_Audit_DB_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 Para obter um exemplo completo sobre como criar uma auditoria, consulte [SQL Server Audit &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [Criar especificação de auditoria de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [Remova a especificação de auditoria de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys. fn_get_audit_file &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [server_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys. server_file_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [server_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys. database_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [database_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.DM server_audit_status &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.DM audit_actions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  

