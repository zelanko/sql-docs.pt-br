---
title: sp_syspolicy_rename_condition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_condition
- sp_syspolicy_rename_condition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_condition
ms.assetid: d9f3f9b1-701b-4fce-9b42-c282656caf84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4109b122f37c12cb9c01be2ceb36d185b9d6418c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651858"
---
# <a name="sp_syspolicy_rename_condition-transact-sql"></a>sp_syspolicy_rename_condition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Renomeia uma condição existente no Gerenciamento Baseado em Políticas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_rename_condition { [ @name = ] 'name' | [ @condition_id = ] condition_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`É o nome da condição que você deseja renomear. *Name* é **sysname**e deve ser especificado se *condition_id* for NULL.  
  
`[ @condition_id = ] condition_id`É o identificador da condição que você deseja renomear. *condition_id* é **int**e deverá ser especificado se *Name* for NULL.  
  
`[ @new_name = ] 'new_name'`É o novo nome da condição. *new_name* é **sysname**e é obrigatório. Não pode ser NULL ou uma cadeia de caracteres vazia.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_rename_condition no contexto do banco de dados de sistema msdb.  
  
 Você deve especificar um valor para o *nome* ou *condition_id*. Nenhum deles pode ser NULL. Para obter estes valores, consulte a exibição do sistema msdb.dbo.syspolicy_conditions.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que são confiáveis com o controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir renomeia uma condição chamada 'Change Tracking Enabled'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_condition @name = N'Change Tracking Enabled'  
, @new_name = N'Verify Change Tracking Enabled';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
