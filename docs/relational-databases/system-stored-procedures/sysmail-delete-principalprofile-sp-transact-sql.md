---
title: sysmail_delete_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae63fabdca36e70daa6da28daa136a5dfcec8e1f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527778"
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove a permissão de um usuário do banco de dados ou função para usar um perfil público ou privado do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id` É a ID do usuário de banco de dados ou função na **msdb** banco de dados para associação a ser excluída. *principal_id* está **int**, com um padrão NULL. Para fazer um perfil público em um perfil privado, forneça a ID da entidade **0** ou o nome da entidade **'public'**. Qualquer um dos *principal_id* ou *principal_name* deve ser especificado.  
  
`[ @principal_name = ] 'principal_name'` É o nome do usuário de banco de dados ou função na **msdb** banco de dados para associação a ser excluída. *principal_name* está **sysname**, com um padrão NULL. Para fazer um perfil público em um perfil privado, forneça a ID da entidade **0** ou o nome da entidade **'public'**. Qualquer um dos *principal_id* ou *principal_name* deve ser especificado.  
  
`[ @profile_id = ] profile_id` É a ID do perfil da associação a ser excluída. *profile_id* está **int**, com um padrão NULL. Qualquer um dos *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'` É o nome do perfil da associação a ser excluída. *profile_name* está **sysname**, com um padrão NULL. Qualquer um dos *profile_id* ou *profile_name* deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Para fazer um perfil público em um perfil privado, forneça **'public'** para o nome da entidade ou **0** para a id da entidade.  
  
 Tenha cuidado ao remover permissões do perfil privado padrão para um usuário ou do perfil público padrão. Quando nenhum perfil padrão estiver disponível, **sp_send_dbmail** requer um nome de um perfil como um argumento. Portanto, a remoção de um perfil padrão pode causar chamadas para **sp_send_dbmail** falhe. Para obter mais informações, consulte [sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).  
  
 O procedimento armazenado **sysmail_delete_principalprofile_sp** está no **msdb** banco de dados e é de propriedade de **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão os membros de **sysadmin** função de servidor fixa.  
  
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
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
