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
ms.openlocfilehash: 1f488c50518f0a1dd06d72532f1e9edad865e26a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783664"
---
# <a name="sysmail_update_principalprofile_sp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Atualiza as informações de uma associação entre uma entidade e um perfil.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id`A ID do usuário de banco de dados ou função no banco de dados **msdb** para a associação a ser alterada. *principal_id* é **int**, com um padrão de NULL. O *principal_id* ou *principal_name* deve ser especificado.  
  
`[ @principal_name = ] 'principal_name'`O nome do usuário do banco de dados ou da função no banco de dados **msdb** para a associação a ser atualizada. *principal_name* é **sysname**, com um padrão de NULL. *Principal_id* ou *principal_name* pode ser especificado.  
  
`[ @profile_id = ] profile_id`A ID do perfil para a associação a ser alterada. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'`O nome do perfil para a associação a ser alterada. *profile_name* é **sysname**, com um padrão de NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @is_default = ] 'is_default'`É se esse perfil é o perfil padrão para o usuário do banco de dados. Um usuário de banco de dados pode ter somente um perfil padrão. *is_default* é **bit**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Este procedimento armazenado será alterado se o perfil especificado for o padrão para o usuário do banco de dados. Um usuário de banco de dados pode ter somente um perfil privado padrão.  
  
 Quando o nome principal da associação for **público** ou a ID da entidade de segurança for **0**, esse procedimento armazenado alterará o perfil público. Pode haver somente um perfil público padrão.  
  
 Quando ** \@ is_default** for '**1**' e a entidade de segurança estiver associada a mais de um perfil, o perfil especificado se tornará o perfil padrão para a entidade de segurança. O perfil que anteriormente era o padrão ainda estará associado à entidade, mas não mais será o perfil padrão.  
  
 O procedimento armazenado **sysmail_update_principalprofile_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 **A. Definindo um perfil para ser o perfil público padrão para um banco de dados**  
  
 O exemplo a seguir define o perfil `General Use Profile` como o perfil público padrão para usuários no banco de dados **msdb** .  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. Definindo um perfil para ser o perfil privado padrão para um usuário**  
  
 O exemplo a seguir define o perfil `AdventureWorks Administrator` como o perfil padrão para a entidade de segurança `ApplicationUser` no banco de dados **msdb** . O perfil já deve estar associado à entidade. O perfil que anteriormente era o padrão ainda estará associado à entidade, mas não mais será o perfil padrão.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
