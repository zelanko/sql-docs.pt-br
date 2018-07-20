---
title: MSmerge_identity_range_allocations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df286fcd67db26ac149bd56d3635425453d78405
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102784"
---
# <a name="msmergeidentityrangeallocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_identity_range_allocations** tabela é usada para controlar o histórico de identidade atribuições de intervalo para Publicadores e assinantes para artigos publicados. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**nvarchar(128)**|O nome do banco de dados de publicação.|  
|**publicação**|**nvarchar(128)**|O nome da publicação.|  
|**article**|**nvarchar(128)**|O nome do artigo.|  
|**Assinante**|**nvarchar(128)**|O nome do Assinante.|  
|**subscriber_db**|**nvarchar(128)**|O nome do banco de dados de assinatura.|  
|**is_pub_range**|**bit**|Lista se o intervalo de identidade é ou não atribuído a um Publicador.|  
|**ranges_allocated**|**tinyint**|O número de intervalos de identidade atribuídos.|  
|**range_begin**|**numeric(38)**|O valor inicial do intervalo.|  
|**range_end**|**numeric(38)**|O último valor no intervalo.|  
|**next_range_begin**|**numeric(38)**|O valor inicial do próximo intervalo a ser atribuído.|  
|**next_range_end**|**numeric(38)**|O valor final do próximo intervalo a ser atribuído.|  
|**max_used**|**numeric(38)**|O valor de identidade mais alto usado.|  
|**time_of_allocation**|**datetime**|A hora em que a atribuição foi feita.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
