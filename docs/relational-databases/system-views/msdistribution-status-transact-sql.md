---
description: MSdistribution_status (Transact-SQL)
title: MSdistribution_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_status_TSQL
- MSdistribution_status
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_status view
ms.assetid: 90d447de-3a4a-4f3e-aeab-e8fff6348361
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07acca59b78290d1cab5d0c528604a8a9616ece8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473088"
---
# <a name="msdistribution_status-transact-sql"></a>MSdistribution_status (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição **MSdistribution_status** expõe informações adicionais sobre os comandos de status no banco de dados de distribuição. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Identifica um artigo.|  
|**agent_id**|**int**|Identifica um agente de replicação.|  
|**UndelivCmdsInDistDB**|**int**|O número de comandos pendentes entregues aos Assinantes.|  
|**DelivCmdsInDistDB**|**int**|O número de comandos entregues aos Assinantes.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
