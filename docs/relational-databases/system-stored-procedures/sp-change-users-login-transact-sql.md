---
title: sp_change_users_login (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 79a0e1807b517c900dfc29bc41c24cc7c223291f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spchangeuserslogin-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mapeia um usuário de banco de dados existente para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) em vez disso.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @Action=] '*ação*'  
 Descreve a ação a ser executada pelo procedimento. *ação* é **varchar (10)**. *ação* pode ter um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Auto_Fix**|Vincula uma entrada de usuário na exibição do catálogo de sistema sys.database_principals no banco de dados atual a um logon de nome igual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se ainda não existir um logon com o mesmo nome, ele será criado. Examine o resultado do **Auto_Fix** instrução para confirmar que o vínculo correto foi realmente estabelecido. Evite usar **Auto_Fix** em situações confidenciais de segurança.<br /><br /> Quando você usa **Auto_Fix**, você deve especificar *usuário* e *senha* se o logon não existir, caso contrário, você deve especificar *usuário*mas *senha* será ignorado. *logon* deve ser NULL. *usuário* deve ser um usuário válido no banco de dados atual. Não pode haver outro usuário mapeado para o logon.|  
|**Relatório**|Lista os usuários e o SID (identificador de segurança) correspondentes no banco de dados atual que não estão vinculados a nenhum logon. *usuário*, *login*, e *senha* deve ser NULL ou não especificado.<br /><br /> Para substituir a opção de relatório por uma consulta usando as tabelas do sistema, compare as entradas em **sys. server_prinicpals** com as entradas em **database_principals**.|  
|**Update_One**|Vincula especificado *usuário* no banco de dados atual a um existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *logon*. *usuário* e *login* deve ser especificado. *senha* deve ser NULL ou não especificado.|  
  
 [ @UserNamePattern=] '*usuário*'  
 É o nome de um usuário no banco de dados atual. *usuário* é **sysname**, com um padrão NULL.  
  
 [ @LoginName=] '*login*'  
 E o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* é **sysname**, com um padrão de NULL.  
  
 [ @Password=] '*senha*'  
 É a senha atribuída a um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon é criado especificando **Auto_Fix**. Se já existir um logon correspondente, o usuário e logon serão mapeados e *senha* será ignorado. Se não existir um logon correspondente, sp_change_users_login criará um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon e atribui *senha* como a senha para o novo logon. *senha* é **sysname**, e não deve ser NULL.  
  
> **IMPORTANTE:** Sempre use um [senha forte!](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|Nome do usuário do banco de dados.|  
|UserSID|**varbinary(85)**|O identificador de segurança do usuário.|  
  
## <a name="remarks"></a>Remarks  
 Use sp_change_users_login para vincular um usuário do banco de dados atual a um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o logon do usuário for alterado, use sp_change_users_login para vinculá-lo ao novo logon sem perder as permissões de usuário. O novo *login* não pode ser sa e o *usuário*não pode ser dbo, convidado ou um usuário do INFORMATION_SCHEMA.  
  
 Não é possível usar sp_change_users_login para mapear os usuários do banco de dados para entidades do nível do Windows, certificados ou chaves assimétricas.  
  
 sp_change_users_login não pode ser usado com um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de uma entidade do Windows ou com um usuário criado pelo uso de CREATE USER WITHOUT LOGIN.  
  
 Não é possível executar sp_change_users_login em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner. Somente membros da função de servidor fixa sysadmin podem especificar o **Auto_Fix** opção.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. Mostrando um relatório do usuário atual para mapeamentos de logon  
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
 O exemplo a seguir mostra como usar `Auto_Fix` para mapear um usuário existente para um logon com o mesmo nome ou como criar o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Mary` com a senha `B3r12-3x$098f6` se o logon `Mary` não existir.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
