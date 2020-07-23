---
title: sys. dm_cluster_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe06d6b7c00fe60c44b19468f9ef0cc814d25e5d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913222"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys. dm_cluster_endpoints (Transact-SQL)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome do serviço exposto externamente em um cluster do SQL Big Data. Identificador exclusivo do ponto de extremidade. Chave para esta exibição. Não permite valor nulo. |  
|description|`nvarchar(4000)`|Descrição do serviço. Não permite valor nulo. |
|endpoint|`sysname`|URL do ponto de extremidade ou atributo de conexão. Não permite valor nulo. |
|protocol_desc|`sysname`|Descrição do protocolo de ponto de extremidade |

## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.

## <a name="see-also"></a>Consulte Também

[O que [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] são ](../../big-data-cluster/big-data-cluster-overview.md)?
