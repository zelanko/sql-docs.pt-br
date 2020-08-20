---
description: sp_delete_targetservergroup (Transact-SQL)
title: sp_delete_targetservergroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetservergroup_TSQL
- sp_delete_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetservergroup
ms.assetid: d8dd838e-64aa-419f-9ccb-ff04908cf3e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c35c95e7140de0ce3da453a8063cb849625639af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469588"
---
# <a name="sp_delete_targetservergroup-transact-sql"></a>sp_delete_targetservergroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui o grupo de servidores de destino especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_targetservergroup [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` O nome do grupo de servidores de destino a ser removido. o *nome* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o grupo de servidores de destino `Servers Processing Customer Orders`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetservergroup  
    @name = N'Servers Processing Customer Orders';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_targetservergroup ](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_targetservergroup ](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_targetservergroup ](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
  
  
