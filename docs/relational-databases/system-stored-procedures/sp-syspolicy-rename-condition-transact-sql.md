---
title: sp_syspolicy_rename_condition (Transact-SQL) | Microsoft Docs
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
- sp_syspolicy_rename_condition
- sp_syspolicy_rename_condition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_condition
ms.assetid: d9f3f9b1-701b-4fce-9b42-c282656caf84
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c44a683e247b8de88c1223f1320683486611d9c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33257495"
---
# <a name="spsyspolicyrenamecondition-transact-sql"></a>sp_syspolicy_rename_condition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Renomeia uma condição existente no Gerenciamento Baseado em Políticas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_rename_condition { [ @name = ] 'name' | [ @condition_id = ] condition_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@name=** ] **'***name***'**  
 É o nome da condição que você deseja renomear. *nome* é **sysname**e deve ser especificado se *condition_id* é NULL.  
  
 [  **@condition_id=** ] *condition_id*  
 É o identificador para a condição que você deseja renomear. *condition_id* é **int**e deve ser especificado se *nome* é NULL.  
  
 [ **@new_name=** ] **'***new_name***'**  
 É o novo nome da condição. *Novo_nome* é **sysname**e é necessário. Não pode ser NULL ou uma cadeia de caracteres vazia.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Você deve executar sp_syspolicy_rename_condition no contexto do banco de dados de sistema msdb.  
  
 Você deve especificar um valor para *nome* ou *condition_id*. Nenhum deles pode ser NULL. Para obter estes valores, consulte a exibição do sistema msdb.dbo.syspolicy_conditions.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que sejam confiáveis com controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir renomeia uma condição chamada 'Change Tracking Enabled'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_condition @name = N'Change Tracking Enabled'  
, @new_name = N'Verify Change Tracking Enabled';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
