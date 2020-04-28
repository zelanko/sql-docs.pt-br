---
title: sp_change_users_login (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b0c847215d31bd2064467c3edbce42ba957c2e78
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79448336"
---
# <a name="sp_change_users_login-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mapeia um usuário de banco de dados existente para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
 > [!IMPORTANT]
 > [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) .  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @Action= ] '*ação*'  
 Descreve a ação a ser executada pelo procedimento. a *ação* é **varchar (10)**. a *ação* pode ter um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Auto_Fix**|Vincula uma entrada de usuário na exibição do catálogo de sistema sys.database_principals no banco de dados atual a um logon de nome igual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se ainda não existir um logon com o mesmo nome, ele será criado. Examine o resultado da instrução **Auto_Fix** para confirmar se o link correto foi feito de fato. Evite usar **Auto_Fix** em situações sensíveis à segurança.<br /><br /> Ao usar **Auto_Fix**, você deverá especificar *usuário* e *senha* se o logon ainda não existir, caso contrário, você deverá especificar o *usuário* , mas a *senha* será ignorada. o *logon* deve ser nulo. o *usuário* deve ser um usuário válido no banco de dados atual. Não pode haver outro usuário mapeado para o logon.|  
|**Relatório**|Lista os usuários e o SID (identificador de segurança) correspondentes no banco de dados atual que não estão vinculados a nenhum logon. *usuário*, *logon*e *senha* devem ser nulos ou não especificados.<br /><br /> Para substituir a opção de relatório por uma consulta usando as tabelas do sistema, compare as entradas em **Sys. server_prinicpals** com as entradas em **Sys. database_principals**.|  
|**Update_One**|Vincula o *usuário* especificado no banco de dados atual a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *logon*existente. o *usuário* e o *logon* devem ser especificados. a *senha* deve ser nula ou não especificada.|  
  
 [ @UserNamePattern= ] '*usuário*'  
 É o nome de um usuário no banco de dados atual. o *usuário* é **sysname**, com um padrão de NULL.  
  
 [ @LoginName= ] '*logon*'  
 E o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* é **sysname**, com um padrão de NULL.  
  
 [ @Password= ] '*senha*'  
 É a senha atribuída a um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon que é criado especificando **Auto_Fix**. Se um logon correspondente já existir, o usuário e o logon serão mapeados e a *senha* será ignorada. Se um logon correspondente não existir, o sp_change_users_login criará um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] novo logon e atribuirá a *senha* como a senha para o novo logon. a *senha* é **sysname**e não deve ser nula.  
  
> **IMPORTANTE:** Sempre use uma [senha forte!](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|Nome do usuário do banco de dados.|  
|UserSID|**varbinary (85)**|O identificador de segurança do usuário.|  
  
## <a name="remarks"></a>Comentários  
 Use sp_change_users_login para vincular um usuário do banco de dados atual a um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o logon do usuário for alterado, use sp_change_users_login para vinculá-lo ao novo logon sem perder as permissões de usuário. O novo *logon* não pode ser SA e o *usuário* não pode ser dbo, guest ou um usuário INFORMATION_SCHEMA.  
  
 Não é possível usar sp_change_users_login para mapear os usuários do banco de dados para entidades do nível do Windows, certificados ou chaves assimétricas.  
  
 sp_change_users_login não pode ser usado com um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de uma entidade do Windows ou com um usuário criado pelo uso de CREATE USER WITHOUT LOGIN.  
  
 Não é possível executar sp_change_users_login em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner. Somente os membros da função de servidor fixa sysadmin podem especificar a opção **Auto_Fix** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>a. Mostrando um relatório do usuário atual para mapeamentos de logon  
 O exemplo a seguir produz um relatório dos usuários do banco de dados atual e seus identificadores de segurança (SIDs).  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. Mapeando um usuário de banco de dados para um novo logon do SQL Server  
 No exemplo a seguir, um usuário de banco de dados é associado a um novo logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O usuário de banco de dados `MB-Sales`, que inicialmente está mapeado para outro logon, é remapeado para o logon `MaryB`.  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. Mapeando automaticamente um usuário para um logon, criando um novo logon se necessário  
 O exemplo a seguir mostra como usar `Auto_Fix` para mapear um usuário existente para um logon com o mesmo nome ou como criar o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`Mary` com a senha `B3r12-3x$098f6` se o logon `Mary` não existir.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CRIAR logon &#40;&#41;Transact-SQL](../../t-sql/statements/create-login-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helplogins](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
