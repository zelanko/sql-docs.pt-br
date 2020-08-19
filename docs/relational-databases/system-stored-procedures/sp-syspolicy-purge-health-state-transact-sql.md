---
description: sp_syspolicy_purge_health_state (Transact-SQL)
title: sp_syspolicy_purge_health_state (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_purge_health_state_TSQL
- sp_syspolicy_purge_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_purge_health_state
ms.assetid: 4ba4aa91-4c19-41c7-b70d-5fd9d0e89a5e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a01ee9be75223a081d19a9b71eb4d69ec150235c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446742"
---
# <a name="sp_syspolicy_purge_health_state-transact-sql"></a>sp_syspolicy_purge_health_state (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui os estados de integridade de política no Gerenciamento Baseado em Políticas. Os estados de integridade de política são indicadores visuais (um símbolo de rolagem com um "X" vermelho) dentro do Pesquisador de Objetos que permitem que você determine os nós que apresentaram falha em uma avaliação de política.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_purge_health_state [ @target_tree_root_with_id = ] 'target_tree_root_with_id'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @target_tree_root_with_id = ] 'target_tree_root_with_id'` Representa o nó no Pesquisador de objetos em que você deseja limpar o estado de integridade. *target_tree_root_with_id* é **nvarchar (400)**, com um padrão de NULL.  
  
 Você pode especificar valores da coluna target_query_expression_with_id da exibição do sistema msdb.dbo.syspolicy_system_health_state.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_purge_health_state no contexto do banco de dados de sistema msdb.  
  
 Se você executar esse procedimento armazenado sem qualquer parâmetro, o estado de integridade do sistema será excluído para todos os nós do Pesquisador de Objetos.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que são confiáveis com o controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui os estados de integridade de um nó específico do Pesquisador de Objetos.  
  
```  
EXEC msdb.dbo.sp_syspolicy_purge_health_state @target_tree_root_with_id = 'Server/Database[@ID=7]';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
