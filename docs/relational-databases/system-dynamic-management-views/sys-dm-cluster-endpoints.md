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
ms.openlocfilehash: 95f251db2efe471455d18f4735be99ecee962a7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717505"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys. dm_cluster_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/applies-to-version/sqlserver2019.md)]

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome do serviço exposto externamente em um cluster do SQL Big Data. Identificador exclusivo do ponto de extremidade. Chave para esta exibição. Não permite valor nulo. |  
|descrição|`nvarchar(4000)`|Descrição do serviço. Não permite valor nulo. |
|endpoint|`sysname`|URL do ponto de extremidade ou atributo de conexão. Não permite valor nulo. |
|protocol_desc|`sysname`|Descrição do protocolo de ponto de extremidade |

## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.

## <a name="see-also"></a>Consulte Também

[O que [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] são ](../../big-data-cluster/big-data-cluster-overview.md)?
