---
title: MSdynamicsnapshotjobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f717d5cf35349dcb99ec2022c5c0c92df5ea4286
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812704"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSdynamicsnapshotjobs** rastreia as informações de filtro de linha com parâmetros aplicadas para gerar um instantâneo de dados filtrado. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do trabalho de instantâneo de dados filtrado.|  
|**name**|**sysname**|O nome do trabalho de instantâneo de dados filtrado.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo desta publicação.|  
|**job_id**|**uniqueidentifier**|A ID do trabalho SQL Server Agent no Distribuidor.|  
|**agent_id**|**int**|A ID do SQL Server Agent.|  
|**dynamic_filter_login**|**sysname**|O valor usado para avaliar a função [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) em filtros de linha com parâmetros definidos para a publicação.|  
|**dynamic_filter_hostname**|**sysname**|O valor usado para avaliar a função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em filtros de linha com parâmetros definidos para a publicação.|  
|**dynamic_snapshot_location**|**nvarchar (255)**|O caminho da pasta onde os arquivos de instantâneo serão lidos se um instantâneo de dados filtrado for usado.|  
|**partition_id**|**int**|A ID da partição de dados à qual o trabalho pertence.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
