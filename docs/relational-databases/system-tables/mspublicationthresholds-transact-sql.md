---
title: MSpublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cec59e0b5cb933822790a1f2497ca1bd5a3cbb2e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794158"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSpublicationthresholds** tabela é usada para controlar métricas de desempenho de replicação para uma publicação, com uma linha para cada valor de limite que está sendo monitorado. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|Identifica a publicação para a qual um limite foi definido.|  
|**metric_id**|**int**|Identifica uma métrica de desempenho de replicação sendo monitorada como definida na [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) tabela do sistema.|  
|**value**|**sql_variant**|O valor de limite da métrica que está sendo monitorada.|  
|**shouldalert**|**bit**|Um valor de **1** indica que um alerta deve ser gerado quando a métrica excede o limite definido.|  
|**IsEnabled**|**bit**|Um valor de **1** indica que o monitoramento está habilitado para esta métrica de desempenho de replicação.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
