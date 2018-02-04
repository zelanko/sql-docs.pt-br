---
title: sysmail_delete_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 204daab0d90b050237d864c23729cf2544d68fe4
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove a permissão de um usuário do banco de dados ou função para usar um perfil público ou privado do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@principal_id** = ] *principal_id*  
 É a ID do usuário de banco de dados ou da função no **msdb** banco de dados para associação a ser excluída. *principal_id* é **int**, com um padrão NULL. Para fazer um perfil público em um perfil privado, forneça a ID da entidade **0** ou o nome da entidade **'public'**. O *principal_id* ou *principal_name* deve ser especificado.  
  
 [ **@principal_name** = ] **'***principal_name***'**  
 É o nome do usuário de banco de dados ou da função no **msdb** banco de dados para associação a ser excluída. *principal_name* é **sysname**, com um padrão NULL. Para fazer um perfil público em um perfil privado, forneça a ID da entidade **0** ou o nome da entidade **'public'**. O *principal_id* ou *principal_name* deve ser especificado.  
  
 [ **@profile_id** = ] *profile_id*  
 É a ID do perfil da associação a ser excluída. *profile_id* é **int**, com um padrão NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 É o nome do perfil da associação a ser excluída. *profile_name* é **sysname**, com um padrão NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Para fazer um perfil público em um perfil privado, forneça **'public'** para o nome da entidade ou **0** para a id da entidade.  
  
 Tenha cuidado ao remover permissões do perfil privado padrão para um usuário ou do perfil público padrão. Quando nenhum perfil padrão estiver disponível, **sp_send_dbmail** requer o nome de um perfil como um argumento. Portanto, a remoção de um perfil padrão pode causar chamadas para **sp_send_dbmail** falha. Para obter mais informações, consulte [sp_send_dbmail &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).  
  
 O procedimento armazenado **sysmail_delete_principalprofile_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a exclusão da associação entre o perfil **AdventureWorks Administrator** e o logon **ApplicationUser** no **msdb** banco de dados.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Armazenados do Database Mail procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
