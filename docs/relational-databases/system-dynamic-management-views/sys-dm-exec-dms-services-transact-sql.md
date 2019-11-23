---
title: sys.dm_exec_dms_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DMS_SERVICES_TSQL
- SYS.DM_EXEC_DMS_SERVICES_TSQL
- DM_EXEC_DMS_SERVICES
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_services management view
- sys.dm_exec_dms_services management view
ms.assetid: 6ac47eef-4293-46b8-8555-07a614837504
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11e353af23c2331cd8f2bef5b439c967512e7323
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532933"
---
# <a name="sysdm_exec_dms_services-transact-sql"></a>sys.dm_exec_dms_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os serviços DMS em execução nos nós de computação do polybase. Ele lista uma linha por instância de serviço.  
  
|Column Name|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|`int`|ID numérica exclusiva associada ao núcleo DMS. Chave para esta exibição.|ID exclusiva.|  
|compute_node_id|`int`|ID do nó no qual este serviço DMS está em execução|Consulte *compute_node_id* em [Sys. DM_EXEC_COMPUTE_NODES &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|status|`nvarchar(32)`|Status atual do serviço DMS||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

## <a name="see-also"></a>Consulte também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições &#40;de gerenciamento dinâmico relacionadas ao banco de dados TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
