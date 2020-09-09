---
description: MSpublicationthresholds (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f43705f8fec92e39e55a4fa4f62cf24aa9f25be
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540286"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSpublicationthresholds** é usada para rastrear as métricas de desempenho de replicação de uma publicação, com uma linha para cada valor de limite que está sendo monitorado. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|Identifica a publicação para a qual um limite foi definido.|  
|**metric_id**|**int**|Identifica uma métrica de desempenho de replicação que está sendo monitorada conforme definido na tabela do sistema [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) .|  
|**value**|**sql_variant**|O valor de limite da métrica que está sendo monitorada.|  
|**shouldalert**|**bit**|Um valor de **1** indica que um alerta deve ser gerado quando a métrica excede o limite definido.|  
|**IsEnabled**|**bit**|Um valor de **1** indica que o monitoramento está habilitado para essa métrica de desempenho de replicação.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
