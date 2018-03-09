---
title: MSdbms_map (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f470dc7c2733db9a7ecd9730ce634317b1702b55
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msdbmsmap-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdbms_map** tabela contém informações de tipo de dados de origem, bem como um link para informações de tipo de dados de destino padrão para os pares DBMS de origem e de destino. Essa tabela é armazenada no **msdb** banco de dados e é usado para publicação heterogênea.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|Identifica com exclusividade um mapeamento de tipo de dados.|  
|**src_dbms_id**|**int**|Identifica o DBMS de origem especificando seu **dbms_id** no [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) tabela.|  
|**dest_dbms_id**|**int**|Identifica o DBMS de destino especificando seu **dbms_id** no [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) tabela.|  
|**src_datatype_id**|**int**|Identifica o **datatype_id** do [MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md) tabela para o tipo de fonte de dados.|  
|**src_len_min**|**bigint**|O comprimento mínimo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**src_len_max**|**bigint**|O comprimento máximo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**src_prec_min**|**bigint**|A precisão mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**src_prec_max**|**bigint**|A precisão máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**src_scale_min**|**int**|A escala mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**src_scale_max**|**int**|A escala máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**src_nullable**|**bit**|Indica se a coluna de destino no mapeamento permite valores NULL, onde um valor de NULL significa que essa definição não é exigida.|  
|**default_datatype_mapping_id**|**int**|Identifica o mapeamento de tipo de dados padrão especificando seu **map_id** na tabela [MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
