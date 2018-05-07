---
title: sp_syspolicy_add_policy_category_subscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_add_policy_category_subscription
- sp_syspolicy_add_policy_category_subscription_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category_subscription
ms.assetid: 4284f550-9a3f-4726-8181-15e407fbf08f
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c3e5f4079a75fca4112da1185a941b3a77e6b85
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spsyspolicyaddpolicycategorysubscription-transact-sql"></a>sp_syspolicy_add_policy_category_subscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Acrescenta uma assinatura de categoria de política ao banco de dados especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_add_policy_category_subscription [ @target_type = ] 'target_type'  
    , [ @target_object = ] 'target_object'  
    , [ @policy_category = ] 'policy_category'  
    [ , [ @policy_category_subscription_id = ] policy_category_subscription_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@target_type=** ] **'***target_type***'**  
 É o tipo de destino da assinatura da categoria. *target_type* é **sysname**, é necessário e deve ser definido como 'DATABASE'.  
  
 [  **@target_object=** ] **'***target_object***'**  
 É o nome do banco de dados que assinará a categoria. *target_object* é **sysname**e é necessário.  
  
 [  **@policy_category=** ] **'***policy_category***'**  
 É o nome da categoria de política para assinar. *policy_category* é **sysname**e é necessário.  
  
 Para obter valores *policy_category*, consultar o syspolicy_policy_categories do sistema.  
  
 [  **@policy_category_subscription_id=** ] *policy_category_subscription_id*  
 É o identificador da assinatura da categoria. *policy_category_subscription_id* é **int**e é retornada como OUTPUT.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Você deve executar sp_syspolicy_add_policy_category_subscription no contexto do banco de dados de sistema msdb.  
  
 Se você especificar uma categoria de política que não existe, uma nova categoria de política será criada e a assinatura será designada para todos os bancos de dados quando você executar o procedimento armazenado. Se você desmarcar a assinatura designada para a nova categoria, a assinatura só se aplicará ao banco de dados que você especificou como *target_object*. Para obter mais informações sobre como alterar uma configuração de assinatura designada, veja [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado é executado no contexto de seu proprietário atual.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir configura o banco de dados especificado para assinar uma categoria de política chamada 'Políticas de Nomeação de Tabela'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
, @target_object = N'AdventureWorks2012'  
, @policy_category = N'Table Naming Policies';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
