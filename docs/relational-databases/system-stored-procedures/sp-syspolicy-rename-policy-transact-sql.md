---
description: sp_syspolicy_rename_policy (Transact-SQL)
title: sp_syspolicy_rename_policy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_policy_TSQL
- sp_syspolicy_rename_policy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_policy
ms.assetid: ce2b07f5-23b1-4f49-8e7b-c18cf3f3d45b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 782128b1d41f94c63f4e9de22e618378c4ec6e6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481004"
---
# <a name="sp_syspolicy_rename_policy-transact-sql"></a>sp_syspolicy_rename_policy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Renomeia uma política existente no Gerenciamento Baseado em Políticas.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_rename_policy { [ @name = ] 'name' | [ @policy_id = ] policy_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` É o nome da política que você deseja renomear. *Name* é **sysname**e deve ser especificado se *policy_id* for NULL.  
  
`[ @policy_id = ] policy_id` É o identificador da política que você deseja renomear. *policy_id* é **int**e deverá ser especificado se *Name* for NULL.  
  
`[ @new_name = ] 'new_name'` É o novo nome da política. *new_name* é **sysname**e é obrigatório. Não pode ser NULL ou uma cadeia de caracteres vazia.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_rename_policy no contexto do banco de dados de sistema msdb.  
  
 Você deve especificar um valor para o *nome* ou *policy_id*. Nenhum deles pode ser NULL. Para obter estes valores, consulte a exibição do sistema msdb.dbo.syspolicy_policies.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que são confiáveis com o controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte renomeia uma política chamada 'Test Policy 1' para 'Test Policy 2'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_policy @name = N'Test Policy 1'  
, @new_name = N'Test Policy 2';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
