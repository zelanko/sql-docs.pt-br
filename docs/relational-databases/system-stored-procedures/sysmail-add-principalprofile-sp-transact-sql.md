---
title: sysmail_add_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: fedc7e0dd7fe71feb0b0da1f00f2a7f996c6129c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305057"
---
# <a name="sysmail_add_principalprofile_sp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permissão para uma entidade de banco de dados msdb usar um perfil de Database Mail. A entidade de segurança do banco de dados deve ser mapeada para um usuário de autenticação SQL Server, um usuário do Windows ou um grupo do Windows.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id` a ID do usuário de banco de dados ou função no banco de dados **msdb** para a associação. *principal_id* é **int**, com um padrão de NULL. *Principal_id* ou *principal_name* deve ser especificado. Um *principal_id* de **0** torna esse perfil um perfil público, concedendo acesso a todas as entidades de segurança no banco de dados.  
  
`[ @principal_name = ] 'principal_name'` o nome do usuário do banco de dados ou da função no banco de dados **msdb** para a associação. *principal_name* é **sysname**, com um padrão de NULL. *Principal_id* ou *principal_name* deve ser especificado. Uma *principal_name* de **' Public '** torna esse perfil um perfil público, concedendo acesso a todas as entidades no banco de dados.  
  
`[ @profile_id = ] profile_id` a ID do perfil para a associação. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou o *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'` o nome do perfil para a associação. o *profile_name* é **sysname**, sem padrão. O *profile_id* ou o *profile_name* deve ser especificado.  
  
`[ @is_default = ] is_default` especifica se esse perfil é o perfil padrão para a entidade de segurança. Uma entidade de segurança deve ter exatamente um perfil padrão. *is_default* é **bit**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Para tornar um perfil público, especifique um **\@principal_id** de **0** ou um **\@principal_name** de **público**. Um perfil público está disponível para todos os usuários no banco de dados **msdb** , embora os usuários também devam ser membros de **DatabaseMailUserRole** para executar **sp_send_dbmail**.  
  
 Um usuário de banco de dados pode ter somente um perfil padrão. Quando **\@is_default** for '**1**' e o usuário já estiver associado a um ou mais perfis, o perfil especificado se tornará o perfil padrão para o usuário. O perfil que anteriormente era o padrão permanecerá associado ao usuário, mas deixará de ser o perfil padrão.  
  
 Quando **\@is_default** for '**0**' e nenhuma outra associação existir, o procedimento armazenado retornará um erro.  
  
 O procedimento armazenado **sysmail_add_principalprofile_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 **A. Criando uma associação, definindo o perfil padrão @ no__t-0  
  
 O exemplo a seguir cria uma associação entre o perfil chamado `AdventureWorks Administrator Profile` e o usuário do banco de dados **msdb** `ApplicationUser`. O perfil é o perfil padrão para o usuário.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. Criando um perfil do perfil público padrão @ no__t-0  
  
 O exemplo a seguir torna o perfil `AdventureWorks Public Profile` o perfil público padrão para usuários no banco de dados **msdb** .  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos &#40;armazenados TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
