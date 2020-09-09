---
description: sysmail_delete_principalprofile_sp (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e5cfe34ff4bebc2e21517e6515b5ea2ebee3a37f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538456"
---
# <a name="sysmail_delete_principalprofile_sp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove a permissão de um usuário do banco de dados ou função para usar um perfil público ou privado do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id` É a ID do usuário do banco de dados ou da função no banco de dados **msdb** para a associação a ser excluída. *principal_id* é **int**, com um padrão de NULL. Para criar um perfil público em um perfil particular, forneça a ID da entidade de segurança **0** ou o nome da entidade de segurança **' pública '**. O *principal_id* ou *principal_name* deve ser especificado.  
  
`[ @principal_name = ] 'principal_name'` É o nome do usuário do banco de dados ou da função no banco de dados **msdb** para a associação a ser excluída. *principal_name* é **sysname**, com um padrão de NULL. Para criar um perfil público em um perfil particular, forneça a ID da entidade de segurança **0** ou o nome da entidade de segurança **' pública '**. O *principal_id* ou *principal_name* deve ser especificado.  
  
`[ @profile_id = ] profile_id` É a ID do perfil para a associação a ser excluída. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'` É o nome do perfil para a associação a ser excluída. *profile_name* é **sysname**, com um padrão de NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Para criar um perfil público em um perfil particular, forneça **' público '** para o nome da entidade de segurança ou **0** para a ID da entidade de segurança.  
  
 Tenha cuidado ao remover permissões do perfil privado padrão para um usuário ou do perfil público padrão. Quando nenhum perfil padrão está disponível, **sp_send_dbmail** requer o nome de um perfil como um argumento. Portanto, a remoção de um perfil padrão pode causar a falha de chamadas para **sp_send_dbmail** . Para obter mais informações, consulte [sp_send_dbmail &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).  
  
 O procedimento armazenado **sysmail_delete_principalprofile_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a exclusão da associação entre o administrador do perfil **AdventureWorks** e o **ApplicationUser** de logon no banco de dados **msdb** .  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
