---
title: Msdistribuition_status (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5942bf485673ad484a58edc43176da4ae5c95965
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756719"
---
# <a name="msdistributionstatus-transact-sql"></a>MSdistribution_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **Msdistribuition_status** exibição expõe informações adicionais sobre os comandos de status no banco de dados de distribuição. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Identifica um artigo.|  
|**agent_id**|**int**|Identifica um agente de replicação.|  
|**UndelivCmdsInDistDB**|**int**|O número de comandos pendentes entregues aos Assinantes.|  
|**DelivCmdsInDistDB**|**int**|O número de comandos entregues aos Assinantes.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
