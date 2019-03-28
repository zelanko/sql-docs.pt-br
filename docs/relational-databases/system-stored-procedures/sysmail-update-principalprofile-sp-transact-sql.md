---
title: sysmail_update_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a2af55b8c5354dd90e80a0a2a9d149f56abdef27
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533856"
---
# <a name="sysmailupdateprincipalprofilesp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza as informações de uma associação entre uma entidade e um perfil.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id` A ID do usuário de banco de dados ou função na **msdb** banco de dados para associação a ser alterada. *principal_id* está **int**, com um padrão NULL. Qualquer um dos *principal_id* ou *principal_name* deve ser especificado.  
  
`[ @principal_name = ] 'principal_name'` O nome do usuário de banco de dados ou função na **msdb** banco de dados para associação a ser excluída. *principal_name* está **sysname**, com um padrão NULL. Qualquer um dos *principal_id* ou *principal_name* pode ser especificado.  
  
`[ @profile_id = ] profile_id` A id do perfil da associação a ser alterada. *profile_id* está **int**, com um padrão NULL. Qualquer um dos *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'` O nome do perfil da associação a ser alterada. *profile_name* está **sysname**, com um padrão NULL. Qualquer um dos *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @is_default = ] 'is_default'` É se esse perfil é o perfil padrão para o usuário de banco de dados. Um usuário de banco de dados pode ter somente um perfil padrão. *is_default* está **bit**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 Este procedimento armazenado será alterado se o perfil especificado for o padrão para o usuário do banco de dados. Um usuário de banco de dados pode ter somente um perfil privado padrão.  
  
 Quando o nome da entidade para a associação está **pública** ou a id da entidade para a associação é **0**, esse procedimento armazenado alterará o perfil público. Pode haver somente um perfil público padrão.  
  
 Quando **@is_default** é '**1**' e a entidade está associada a mais de um perfil, o perfil especificado torna-se o perfil padrão para a entidade de segurança. O perfil que anteriormente era o padrão ainda estará associado à entidade, mas não mais será o perfil padrão.  
  
 O procedimento armazenado **sysmail_update_principalprofile_sp** está no **msdb** banco de dados e é de propriedade de **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão os membros de **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Definindo um perfil para ser o perfil público padrão para um banco de dados**  
  
 O exemplo a seguir define o perfil `General Use Profile` ser o perfil público do padrão para usuários em de **msdb** banco de dados.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. Definindo um perfil para ser o perfil privado do padrão para um usuário**  
  
 O exemplo a seguir define o perfil `AdventureWorks Administrator` ser o perfil padrão para a entidade de segurança `ApplicationUser` na **msdb** banco de dados. O perfil já deve estar associado à entidade. O perfil que anteriormente era o padrão ainda estará associado à entidade, mas não mais será o perfil padrão.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
