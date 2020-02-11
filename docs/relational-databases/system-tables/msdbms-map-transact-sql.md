---
title: MSdbms_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: fffa30d0e252392c41cee34c1875b12b5b7a53b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907495"
---
# <a name="msdbms_map-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSdbms_map** contém informações de tipo de dados de origem, bem como um link para informações de tipo de dados de destino padrão para pares DBMS de origem e de destino. Essa tabela é armazenada no banco de dados **msdb** e é usada para publicação heterogênea.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|Identifica com exclusividade um mapeamento de tipo de dados.|  
|**src_dbms_id**|**int**|Identifica o DBMS de origem especificando seu **dbms_id** na tabela [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) .|  
|**dest_dbms_id**|**int**|Identifica o DBMS de destino especificando seu **dbms_id** na tabela [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) .|  
|**src_datatype_id**|**int**|Identifica o **datatype_id** da tabela [MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md) para o tipo de dados de origem.|  
|**src_len_min**|**bigint**|O comprimento mínimo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**src_len_max**|**bigint**|O comprimento máximo do tipo de dados no DBMS de origem, onde um valor NULL indica que o comprimento não é usado.|  
|**src_prec_min**|**bigint**|A precisão mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**src_prec_max**|**bigint**|A precisão máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a precisão não é usada.|  
|**src_scale_min**|**int**|A escala mínima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**src_scale_max**|**int**|A escala máxima do tipo de dados no DBMS de origem, onde um valor NULL indica que a escala não é usada.|  
|**src_nullable**|**bit**|Indica se a coluna de destino no mapeamento permite valores NULL, onde um valor de NULL significa que essa definição não é exigida.|  
|**default_datatype_mapping_id**|**int**|Identifica o mapeamento de tipo de dados padrão especificando seu **map_id** na tabela [MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
