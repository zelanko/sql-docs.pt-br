---
title: MSreplication_monitordata (Transact-SQL) | Microsoft Docs
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
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 44e7914937378e7a33c30ba4bc635c972c0c7848
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013113"
---
# <a name="msreplicationmonitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_monitordata** tabela contém dados armazenados em cache usados pelo Monitor de replicação, com uma linha para cada assinatura monitorada. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|A data e a hora em que os dados do monitor foram atualizados.|  
|**computetime**|**Int**|O tempo (em segundos) decorrido para computar dados do monitor.|  
|**publication_id**|**Int**|A ID da publicação.|  
|**publisher**|**sysname**|O nome do publicador.|  
|**publisher_srvid**|**Int**|A ID de servidor do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**Publicação**|**sysname**|O nome da publicação.|  
|**publication_type**|**Int**|O tipo de publicação, que pode ter um destes valores:<br /><br /> **0** = publicação transacional<br /><br /> **1** = publicação de instantâneo<br /><br /> **2** = publicação de mesclagem|  
|**agent_type**|**Int**|O tipo de agente de replicação, que pode ter um destes valores.<br /><br /> **1** = o agente de instantâneo<br /><br /> **2** = o log Reader Agent<br /><br /> **3** = o agente de distribuição<br /><br /> **4** = o agente de mesclagem<br /><br /> **9** = queue Reader Agent|  
|**agent_id**|**Int**|A ID do agente de replicação.|  
|**agent_name**|**sysname**|O nome do trabalho do agente de replicação.|  
|**job_id**|**uniqueidentifier**|O GUID do trabalho do agente de replicação.|  
|**status**|**Int**|Status do agente de replicação, que pode ter um destes valores:<br /><br /> **1** = iniciado<br /><br /> **2** = foi bem-sucedida<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = repetir<br /><br /> **6** = falha|  
|**isagentrunningnow**|**bit**|Um sinalizador que indica se o trabalho do agente está sendo executado, onde um valor de **1** significa que o trabalho está em execução.|  
|**Aviso**|**Int**|Aviso de limite gerado por uma assinatura, que pode ser o resultado OR lógico de um ou mais destes valores.<br /><br /> **1** = expiration – uma assinatura para uma publicação transacional ultrapassou o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção.<br /><br /> **2** = latency – o tempo necessário para replicar dados de um publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration – uma assinatura para uma publicação de mesclagem ultrapassou o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção. 8 = mergefastrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão veloz de rede.<br /><br /> **16** = mergeslowrunduration - o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**last_distsync**|**datetime**|A última data e hora de execução do Distribution Agent.|  
|**agentstoptime**|**datetime**|A data e a hora em que o agente foi interrompido.|  
|**distdb**|**sysname**|Nome do banco de dados de distribuição para a assinatura.|  
|**retention**|**Int**|O período de retenção da publicação.|  
|**time_stamp**|**datetime**|Interno-somente para uso.|  
|**worst_latency**|**Int**|A latência mais alta, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**best_latency**|**Int**|A latência mais baixa, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**avg_latency**|**Int**|A latência média, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**cur_latency**|**Int**|A latência, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents durante a execução atual.|  
|**worst_runspeedPerf**|**Int**|O tempo mais longo de sincronização para a publicação de mesclagem|  
|**best_runspeedPerf**|**Int**|O tempo mais curto de sincronização para a publicação de mesclagem|  
|**average_runspeedPerf**|**Int**|O tempo médio de sincronização para a publicação de mesclagem|  
|**mergePerformance**|**Int**|Desempenho da última sincronização comparada com todas as sincronizações à assinatura, com base na taxa de entrega da última sincronização dividida pela média de todas as taxas de entrega anteriores.|  
|**mergelatestsessionrunduration**|**Int**|Duração da execução mais recente do Merge Agent.|  
|**mergelatestsessionrunspeed**|**float(53)**|Taxa de entrega da execução mais recente do Merge Agent.|  
|**mergelatestsessionconnectiontype**|**Int**|Conexão usada para a sessão mais recente do Merge Agent, que pode ser um dos seguintes valores:<br /><br /> **1** = rede local (LAN)<br /><br /> **2** = conexão de rede dial-up|  
|**retention_period_unit**|**tinyint**|Define a unidade usada ao definir retenção, que pode ter um destes valores:<br /><br /> **1** = semana<br /><br /> **2** = mês<br /><br /> **3** = ano|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replmonitorhelpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [sp_replmonitorhelppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [sp_replmonitorhelppublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [sp_replmonitorhelpmergesession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [sp_replmonitorhelppublicationthresholds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [sp_replmonitorhelpmergesessiondetail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
