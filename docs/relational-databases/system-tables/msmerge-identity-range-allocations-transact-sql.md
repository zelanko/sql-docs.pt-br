---
description: MSmerge_identity_range_allocations (Transact-SQL)
title: MSmerge_identity_range_allocations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aba2d603c53827f63ceb39fdfdaae7819e4e1bff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545634"
---
# <a name="msmerge_identity_range_allocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_identity_range_allocations** é usada para acompanhar o histórico de atribuições de intervalo de identidade, para Publicadores e assinantes, para artigos publicados. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do Publicador.|  
|**publisher_db**|**nvarchar(128)**|O nome do banco de dados de publicação.|  
|**documento**|**nvarchar(128)**|O nome da publicação.|  
|**artigo**|**nvarchar(128)**|O nome do artigo.|  
|**farão**|**nvarchar(128)**|O nome do Assinante.|  
|**subscriber_db**|**nvarchar(128)**|O nome do banco de dados de assinatura.|  
|**is_pub_range**|**bit**|Lista se o intervalo de identidade é ou não atribuído a um Publicador.|  
|**ranges_allocated**|**tinyint**|O número de intervalos de identidade atribuídos.|  
|**range_begin**|**numeric (38)**|O valor inicial do intervalo.|  
|**range_end**|**numeric (38)**|O último valor no intervalo.|  
|**next_range_begin**|**numeric (38)**|O valor inicial do próximo intervalo a ser atribuído.|  
|**next_range_end**|**numeric (38)**|O valor final do próximo intervalo a ser atribuído.|  
|**max_used**|**numeric (38)**|O valor de identidade mais alto usado.|  
|**time_of_allocation**|**datetime**|A hora em que a atribuição foi feita.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
