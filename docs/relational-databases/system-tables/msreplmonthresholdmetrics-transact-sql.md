---
title: MSreplmonthresholdmetrics (Transact-SQL) | Microsoft Docs
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
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c72fccdc6c23e65bd94d3ae7ab5a5b0ab0e4eaa9
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101364"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplmonthresholdmetrics** tabela define as métricas fornecidas para monitorar a replicação. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Identifica uma métrica de desempenho de replicação, e pode ser um dos seguintes valores:<br /><br /> **1** = expiration<br /><br /> **2** = latência<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|O nome da métrica de desempenho da replicação.|  
|**warningbitstatus**|**int**|O identificador bit a bit usado para fornecer um aviso de uma violação de limite para uma das métricas seguintes:<br /><br /> **1** = expiration – uma assinatura para uma publicação transacional ultrapassou o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção.<br /><br /> **2** = latency – o tempo necessário para replicar dados de um publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration – uma assinatura para uma publicação de mesclagem ultrapassou o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção.<br /><br /> **8** = mergefastrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem falhou em manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem falhou em manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**alertmessageid**|**int**|A ID da mensagem de erro que é exibida quando a condição de aviso de limite ocorre.|  
|**Descrição**|**nvarchar(3000)**|A descrição da métrica de desempenho da replicação|  
|**default_value**|**sql_variant**|Um valor padrão para a métrica de desempenho da replicação.|  
|**MIN_VALUE**|**sql_variant**|O valor mínimo para uma métrica de desempenho de replicação associada.|  
|**MAX_VALUE**|**sql_variant**|O valor máximo para uma métrica de desempenho de replicação associada.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
