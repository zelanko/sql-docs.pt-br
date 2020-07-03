---
title: syspolicy_policy_execution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_TSQL
- syspolicy_policy_execution_history
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history view
ms.assetid: b13c44a7-6d49-4d50-abe1-e657fc52bb05
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9e6f8200b1c49bfe5e4977dc1e8f093537fc950e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900577"
---
# <a name="syspolicy_policy_execution_history-transact-sql"></a>syspolicy_policy_execution_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe a hora quando foram executadas as políticas, o resultado de cada execução e os detalhes sobre erros, se houver. A tabela a seguir descreve as colunas na exibição syspolicy_policy_execution_history.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|history_id|**bigint**|Identificador deste registro. Cada registro indica uma política e uma vez que ela foi iniciada.|  
|policy_id|**int**|Identificador da política.|  
|start_date|**datetime**|Data e hora em que esta política tentou executar.|  
|end_date|**datetime**|Hora em que esta política parou de executar.|  
|result|**bit**|Êxito ou falha da política. 0 = Falha, 1 = Êxito.|  
|exception_message|**nvarchar(max)**|Mensagem gerada pela exceção, se houver.|  
|exception|**nvarchar(max)**|Descrição da exceção, se houver.|  
  
## <a name="remarks"></a>Comentários  
 A exibição [syspolicy_policy_execution_history_details](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-details-transact-sql.md) contém detalhes relacionados sobre os destinos da política e as expressões de condição testadas.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
