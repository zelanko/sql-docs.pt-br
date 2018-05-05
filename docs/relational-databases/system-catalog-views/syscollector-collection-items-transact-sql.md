---
title: syscollector_collection_items (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d93bc0a177d5b6aceff813fb0bf225f8b92d492
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre um item em um conjunto de coleta.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**Int**|Identifica o conjunto de coleta. Não permite valor nulo.|  
|**collection_item_id**|**Int**|Identifica um item no conjunto de coleta. Não permite valor nulo.|  
|**collector_type_uid**|**uniqueidentifier**|GUID usado para identificar o tipo de coletor. Não permite valor nulo.|  
|**name**|**nvarchar(4000)**|Nome do conjunto de coleta. Permite valor nulo.|  
|**Frequência**|**Int**|Frequência com que os dados são coletados por um item de coleta. Não permite valor nulo.|  
|**parameters**|**xml**|Descreve a parametrização para o tipo de coletor associado ao item de coleta. O esquema XML para este item de coleta é validado com o esquema XML (XSD) armazenados na **parameter_schema** para um determinado tipo de coletor. Permite valor nulo. Para obter mais informações, consulte [syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
