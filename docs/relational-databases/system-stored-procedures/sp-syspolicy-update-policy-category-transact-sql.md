---
title: sp_syspolicy_update_policy_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_syspolicy_update_policy_category_TSQL
- sp_syspolicy_update_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_update_policy_category
ms.assetid: 6b6413c2-7a3b-4eff-91d9-5db2011869d6
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8d5aa359a3ee224941d52795590d7ff61d58326
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spsyspolicyupdatepolicycategory-transact-sql"></a>sp_syspolicy_update_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza se uma categoria de política é definida para designar assinaturas de banco de dados. Se a assinatura for designada, a categoria de política se aplicará a todos os bancos de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_update_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
    , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@name=** ] **'***name***'**  
 É o nome da categoria de política. *nome* é **sysname**e deve ser especificado se *policy_category_id* é NULL.  
  
 [  **@policy_category_id=** ] *policy_category_id*  
 É o identificador da categoria de política. *policy_category_id* é **int**e deve ser especificado se *nome* é NULL.  
  
 [  **@mandate_database_subscriptions=** ] *mandate_database_subscriptions*  
 Determina se assinatura de banco de dados é designada para a categoria de política. *mandate_database_subscriptions* é um **bit** valor, com um padrão NULL. Você pode usar qualquer um dos seguintes valores:  
  
-   0 = Não designado  
  
-   1 = Designado  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Você deve executar sp_syspolicy_update_policy_category no contexto do banco de dados de sistema msdb.  
  
 Você deve especificar um valor para *nome* ou *policy_category_id*. Nenhum deles pode ser NULL. Para obter esses valores, consulte a exibição do sistema msdb.dbo.syspolicy_policy_categories.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que sejam confiáveis com controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte atualiza a categoria 'Finanças' para designar assinaturas de banco de dados.  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category @name = N'Finance'  
, @mandate_database_subscriptions = 1;  
  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)   
 [sp_syspolicy_rename_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-category-transact-sql.md)  
  
  
