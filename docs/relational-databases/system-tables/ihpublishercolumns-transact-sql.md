---
title: IHpublishercolumns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs: TSQL
helpviewer_keywords: IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94804f224c1807d709efb75960b6b677a068dda4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHpublishercolumns** tabela do sistema representa metadados armazenados no publicador. Esta tabela contém uma linha para cada coluna replicada de não - editores do SQL Server usando o distribuidor atual. Informações de tipo de dados **IHpublishercolumns** é específico para o sistema de gerenciamento de banco de dados do SQL Server (DBMS) do qual os dados são publicados. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica uma coluna publicada.|  
|**table_id**|**int**|Identifica a tabela de origem [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) ao qual a coluna pertence.|  
|**publisher_id**|**smallint**|Identifica o publicador não SQL Server do qual a coluna está sendo publicada.|  
|**name**|**sysname**|O nome da coluna publicada.|  
|**column_ordinal**|**int**|Identifica a coluna por ordem.|  
|**tipo**|**varchar (255)**|O tipo de dados de coluna da coluna de origem no Publicador.|  
|**comprimento**|**bigint**|O comprimento da coluna de origem no Publicador.|  
|**prec**|**int**|A precisão da coluna de origem no Publicador.|  
|**escala**|**int**|A escala da coluna de origem no Publicador.|  
|**IsNullable**|**bit**|Indica se a coluna aceita valores NULL, onde **1** significa que valores NULL são aceitos.|  
|**iscaptured**|**bit**|Indica se um gatilho existe ou não na coluna, que pode existir mesmo se a coluna não for publicada em um artigo. Um valor de **1** significa que o gatilho existe na coluna.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40; Exibição do sistema &#41; &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
