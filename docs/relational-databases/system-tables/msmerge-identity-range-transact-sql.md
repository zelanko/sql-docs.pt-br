---
description: MSmerge_identity_range (Transact-SQL)
title: MSmerge_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4011fcc653e72327fbbd20b3b7d8ec1da135f4f9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463897"
---
# <a name="msmerge_identity_range-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_identity_range** é usada para rastrear os intervalos numéricos atribuídos às colunas de identidade para a assinatura em publicações em que a replicação está gerenciando automaticamente essas atribuições de intervalo. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|O número de identificação exclusivo para uma determinada assinatura.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**range_begin**|**numeric (38)**|O valor de identidade no início do intervalo atual.|  
|**range_end**|**numeric (38)**|O valor de identidade no fim do intervalo atual.|  
|**next_range_begin**|**numeric (38)**|O valor de identidade no início do próximo intervalo a ser atribuído.|  
|**next_range_end**|**numeric (38)**|O valor de identidade no fim do próximo intervalo a ser atribuído.|  
|**is_pub_range**|**bit**|Um valor de **1** se o intervalo de identidade for atribuído à publicação.|  
|**max_used**|**numeric (38)**|O valor de identidade máximo que pode ser atribuído.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
