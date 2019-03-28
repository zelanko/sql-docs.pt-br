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
manager: craigg
ms.openlocfilehash: cf12b97028d3d98f7d5cc5ab034db95411d913dc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528498"
---
# <a name="sysmailaddprincipalprofilesp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permissão para um usuário ou função de banco de dados usarem um perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id` A ID do usuário de banco de dados ou função na **msdb** banco de dados para a associação. *principal_id* está **int**, com um padrão NULL. Qualquer um dos *principal_id* ou *principal_name* deve ser especificado. Um *principal_id* dos **0** faz desse perfil um perfil público, concedendo acesso a todas as entidades no banco de dados.  
  
`[ @principal_name = ] 'principal_name'` O nome do usuário de banco de dados ou função na **msdb** banco de dados para a associação. *principal_name* está **sysname**, com um padrão NULL. Qualquer um dos *principal_id* ou *principal_name* deve ser especificado. Um *principal_name* dos **'public'** faz desse perfil um perfil público, concedendo acesso a todas as entidades no banco de dados.  
  
`[ @profile_id = ] profile_id` A id do perfil da associação. *profile_id* está **int**, com um padrão NULL. Qualquer um dos *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'` O nome do perfil para a associação. *profile_name* está **sysname**, sem padrão. Qualquer um dos *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @is_default = ] is_default` Especifica se este perfil é o perfil padrão para a entidade de segurança. Uma entidade de segurança deve ter exatamente um perfil padrão. *is_default* está **bit**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Para tornar um perfil público, especifique um **@principal_id** de **0** ou um **@principal_name** de **público**. Um perfil público está disponível a todos os usuários a **msdb** do banco de dados, embora os usuários também devem ser um membro da **DatabaseMailUserRole** para executar **sp_send_dbmail**.  
  
 Um usuário de banco de dados pode ter somente um perfil padrão. Quando **@is_default** é '**1**' e o usuário já está associado um ou mais perfis, o perfil especificado se torna o perfil padrão para o usuário. O perfil que anteriormente era o padrão permanecerá associado ao usuário, mas deixará de ser o perfil padrão.  
  
 Quando **@is_default** é '**0**' e nenhuma outra associação existe, o procedimento armazenado retornará um erro.  
  
 O procedimento armazenado **sysmail_add_principalprofile_sp** está no **msdb** banco de dados e é de propriedade de **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão os membros de **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Criando uma associação, definindo o perfil padrão**  
  
 O exemplo a seguir cria uma associação entre o perfil denominado `AdventureWorks Administrator Profile` e o **msdb** usuário de banco de dados `ApplicationUser`. O perfil é o perfil padrão para o usuário.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. Tornando um perfil o perfil público padrão**  
  
 O exemplo a seguir torna o perfil `AdventureWorks Public Profile` o perfil público do padrão para usuários em de **msdb** banco de dados.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
