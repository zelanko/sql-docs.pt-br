---
title: sp_syspolicy_rename_policy_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_policy_category_TSQL
- sp_syspolicy_rename_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_policy_category
ms.assetid: 8a9c4a3a-91e8-435e-b721-e0293c92be3e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 2705451273849e6eb3e7158c410590b6c9031c41
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733694"
---
# <a name="spsyspolicyrenamepolicycategory-transact-sql"></a>sp_syspolicy_rename_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Renomeia uma categoria de política existente no Gerenciamento Baseado em Políticas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_rename_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] **'***nome***'**  
 É o nome da categoria de política que você deseja renomear. *nome da* está **sysname**e deve ser especificado se *policy_category_id* é NULL.  
  
 [  **@policy_category_id=** ] *policy_category_id*  
 É o identificador da categoria de política que você deseja renomear. *policy_category_id* está **int**e deve ser especificado se *nome* é NULL.  
  
 [ **@new_name=** ] **'***new_name***'**  
 É o novo nome para a categoria de política. *new_name* está **sysname**e é necessária. Não pode ser NULL ou uma cadeia de caracteres vazia.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_rename_policy_category no contexto do banco de dados de sistema msdb.  
  
 Você deve especificar um valor para *nome* ou *policy_category_id*. Nenhum deles pode ser NULL. Para obter esses valores, consulte a exibição do sistema msdb.dbo.syspolicy_policy_categories.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente para usuários que sejam confiáveis no controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte renomeia uma categoria de política chamada 'Test Category 1' para 'Test Category 2'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_policy_category @name = N'Test Category 1'  
, @new_name = N'Test Category 2';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)   
 [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)  
  
  
