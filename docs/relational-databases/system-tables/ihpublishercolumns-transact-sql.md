---
title: IHpublishercolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4bd15161e658348ea68c2f87c1468ede00bac5e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHpublishercolumns** tabela do sistema representa metadados armazenados no publicador. Esta tabela contém uma linha para cada coluna replicada de não - editores do SQL Server usando o distribuidor atual. Informações de tipo de dados **IHpublishercolumns** é específico para o sistema de gerenciamento de banco de dados do SQL Server (DBMS) do qual os dados são publicados. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**Int**|Identifica uma coluna publicada.|  
|**table_id**|**Int**|Identifica a tabela de origem [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) ao qual a coluna pertence.|  
|**publisher_id**|**smallint**|Identifica o publicador não SQL Server do qual a coluna está sendo publicada.|  
|**name**|**sysname**|O nome da coluna publicada.|  
|**column_ordinal**|**Int**|Identifica a coluna por ordem.|  
|**type**|**varchar(255)**|O tipo de dados de coluna da coluna de origem no Publicador.|  
|**comprimento**|**bigint**|O comprimento da coluna de origem no Publicador.|  
|**prec**|**Int**|A precisão da coluna de origem no Publicador.|  
|**scale**|**Int**|A escala da coluna de origem no Publicador.|  
|**isnullable**|**bit**|Indica se a coluna aceita valores NULL, onde **1** significa que valores NULL são aceitos.|  
|**iscaptured**|**bit**|Indica se um gatilho existe ou não na coluna, que pode existir mesmo se a coluna não for publicada em um artigo. Um valor de **1** significa que o gatilho existe na coluna.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
