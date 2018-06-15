---
title: IHpublishercolumnindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6d54f286215d34974f1ca10ecd08d3eb7413c95c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33000783"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHpublishercolumnindexes** tabela do sistema mapeia as colunas de uma publicação não SQL Server no [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) para índices de tabela do sistema de [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)tabela do sistema. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**Int**|Identifica a coluna de [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) com um índice associado.|  
|**publisherindex_id**|**Int**|Identifica um índice a partir de [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) associada à coluna de tabela.|  
|**indid**|**Int**|Indica posição da coluna na tabela publicada.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
