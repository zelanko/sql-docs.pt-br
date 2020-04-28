---
title: MSreplmonthresholdmetrics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: stevestein
ms.author: sstein
ms.openlocfilehash: b3e8b9c2443a6fa74e113dc1a3f25880ac753dc0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68079938"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSreplmonthresholdmetrics** define as métricas fornecidas para o monitoramento da replicação. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Identifica uma métrica de desempenho de replicação, e pode ser um dos seguintes valores:<br /><br /> **1** = expiração<br /><br /> **2** = latência<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|O nome da métrica de desempenho da replicação.|  
|**warningbitstatus**|**int**|O identificador bit a bit usado para fornecer um aviso de uma violação de limite para uma das métricas seguintes:<br /><br /> **1** = expiração-uma assinatura para uma publicação transacional excedeu o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção.<br /><br /> **2** = latência-o tempo necessário para replicar dados de um Publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration-uma assinatura para uma publicação de mesclagem excedeu o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção.<br /><br /> **8** = mergefastrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**alertmessageid**|**int**|A ID da mensagem de erro que é exibida quando a condição de aviso de limite ocorre.|  
|**ndescrição**|**nvarchar (3000)**|A descrição da métrica de desempenho da replicação|  
|**default_value**|**sql_variant**|Um valor padrão para a métrica de desempenho da replicação.|  
|**min_value**|**sql_variant**|O valor mínimo para uma métrica de desempenho de replicação associada.|  
|**max_value**|**sql_variant**|O valor máximo para uma métrica de desempenho de replicação associada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
