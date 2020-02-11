---
title: sp_syspolicy_delete_policy_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_category_TSQL
- sp_syspolicy_delete_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_category
ms.assetid: e09d0d50-94d5-48fd-b284-445ddea6dfcd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 635b8c085885c6c8b8c80767f56b58da4cf8774b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997370"
---
# <a name="sp_syspolicy_delete_policy_category-transact-sql"></a>sp_syspolicy_delete_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui uma categoria de política do Gerenciamento Baseado em Políticas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_delete_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`É o nome da categoria de política. *Name* é **sysname**e deve ser especificado se *policy_category_id* for NULL.  
  
`[ @policy_category_id = ] policy_category_id`É o identificador para a categoria de política. *policy_category_id* é **int**e deverá ser especificado se *Name* for NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_delete_policy_category no contexto do banco de dados de sistema msdb.  
  
 Você deve especificar um valor para *nome* ou para *policy_category_id*. Nenhum deles pode ser NULL. Para obter esses valores, consulte a exibição do sistema msdb.dbo.syspolicy_policy_categories.  
  
 Para excluir uma categoria de política, a categoria não deve ser referenciada por nenhuma política.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que são confiáveis com o controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui uma categoria de política chamada 'Finance'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_category @name = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syspolicy_add_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syspolicy_update_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)  
  
  
