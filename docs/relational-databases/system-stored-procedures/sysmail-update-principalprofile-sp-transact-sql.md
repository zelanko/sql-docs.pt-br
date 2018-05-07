---
title: sysmail_update_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a86fc4775ee1096d72451ace855bb19a1094c3c5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
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
 [ **@principal_id** = ] *principal_id*  
 A ID do usuário de banco de dados ou da função no **msdb** banco de dados para associação a ser alterada. *principal_id* é **int**, com um padrão NULL. O *principal_id* ou *principal_name* deve ser especificado.  
  
 [ **@principal_name** =] **'***principal_name***'**  
 O nome do usuário de banco de dados ou da função no **msdb** banco de dados para a associação atualizar. *principal_name* é **sysname**, com um padrão NULL. O *principal_id* ou *principal_name* pode ser especificado.  
  
 [ **@profile_id** =] *profile_id*  
 A ID do perfil da associação a ser alterada. *profile_id* é **int**, com um padrão NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
 [ **@profile_name** =] **'***profile_name***'**  
 O nome do perfil da associação a ser alterada. *profile_name* é **sysname**, com um padrão NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
 [ **@is_default** = ] **'***is_default***'**  
 Se este é o perfil padrão para o usuário do banco de dados. Um usuário de banco de dados pode ter somente um perfil padrão. *is_default* é **bit**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Este procedimento armazenado será alterado se o perfil especificado for o padrão para o usuário do banco de dados. Um usuário de banco de dados pode ter somente um perfil privado padrão.  
  
 Quando o nome da entidade para a associação é **pública** ou a id da entidade para a associação é **0**, esse procedimento armazenado alterará o perfil público. Pode haver somente um perfil público padrão.  
  
 Quando **@is_default** é '**1**' e a entidade de segurança está associada a mais de um perfil, o perfil especificado torna-se o perfil padrão para a entidade de segurança. O perfil que anteriormente era o padrão ainda estará associado à entidade, mas não mais será o perfil padrão.  
  
 O procedimento armazenado **sysmail_update_principalprofile_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Definindo um perfil para ser o perfil público padrão para um banco de dados**  
  
 O exemplo a seguir define o perfil `General Use Profile` para ser o perfil público padrão para os usuários a **msdb** banco de dados.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. Definindo um perfil para ser o perfil privado padrão para um usuário**  
  
 O exemplo a seguir define o perfil `AdventureWorks Administrator` para ser o perfil padrão para a entidade de segurança `ApplicationUser` no **msdb** banco de dados. O perfil já deve estar associado à entidade. O perfil que anteriormente era o padrão ainda estará associado à entidade, mas não mais será o perfil padrão.  
  
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
  
  
