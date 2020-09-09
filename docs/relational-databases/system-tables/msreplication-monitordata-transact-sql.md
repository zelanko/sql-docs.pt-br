---
description: MSreplication_monitordata (Transact-SQL)
title: MSreplication_monitordata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dde16569f96619778a3a3cd6a246f58482b9947d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540855"
---
# <a name="msreplication_monitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSreplication_monitordata** contém dados armazenados em cache usados pelo Replication Monitor, com uma linha para cada assinatura monitorada. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|A data e a hora em que os dados do monitor foram atualizados.|  
|**computetime**|**int**|O tempo (em segundos) decorrido para computar dados do monitor.|  
|**publication_id**|**int**|A ID da publicação.|  
|**programa**|**sysname**|O nome do Publicador.|  
|**publisher_srvid**|**int**|A ID de servidor do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**documento**|**sysname**|O nome da publicação.|  
|**publication_type**|**int**|O tipo de publicação, que pode ter um destes valores:<br /><br /> **0** = publicação transacional<br /><br /> **1** = publicação de instantâneo<br /><br /> **2** = publicação de mesclagem|  
|**agent_type**|**int**|O tipo de agente de replicação, que pode ter um destes valores.<br /><br /> **1** = agente de instantâneo<br /><br /> **2** = agente de leitor de log<br /><br /> **3** = agente de distribuição<br /><br /> **4** = agente de mesclagem<br /><br /> **9** = Queue Reader Agent|  
|**agent_id**|**int**|A ID do agente de replicação.|  
|**agent_name**|**sysname**|O nome do trabalho do agente de replicação.|  
|**job_id**|**uniqueidentifier**|O GUID do trabalho do agente de replicação.|  
|**status**|**int**|Status do agente de replicação, que pode ter um destes valores:<br /><br /> **1** = iniciado<br /><br /> **2** = com êxito<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = repetindo<br /><br /> **6** = com falha|  
|**isagentrunningnow**|**bit**|Um sinalizador que indica se o trabalho do agente está em execução no momento, em que um valor de **1** significa que o trabalho está em execução.|  
|**warning**|**int**|Aviso de limite gerado por uma assinatura, que pode ser o resultado OR lógico de um ou mais destes valores.<br /><br /> **1** = expiração-uma assinatura para uma publicação transacional excedeu o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção.<br /><br /> **2** = latência-o tempo necessário para replicar dados de um Publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration-uma assinatura para uma publicação de mesclagem excedeu o período de retenção por mais do que o limite permitido, como uma porcentagem do período de retenção. 8 = mergefastrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão veloz de rede.<br /><br /> **16** = mergeslowrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**last_distsync**|**datetime**|A última data e hora de execução do Distribution Agent.|  
|**agentstoptime**|**datetime**|A data e a hora em que o agente foi interrompido.|  
|**distdb**|**sysname**|Nome do banco de dados de distribuição para a assinatura.|  
|**políticas**|**int**|O período de retenção para a publicação.|  
|**time_stamp**|**datetime**|Interno-somente uso.|  
|**worst_latency**|**int**|A latência mais alta, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**best_latency**|**int**|A latência mais baixa, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**avg_latency**|**int**|A latência média, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**cur_latency**|**int**|A latência, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents durante a execução atual.|  
|**worst_runspeedPerf**|**int**|O tempo mais longo de sincronização para a publicação de mesclagem|  
|**best_runspeedPerf**|**int**|O tempo mais curto de sincronização para a publicação de mesclagem|  
|**average_runspeedPerf**|**int**|O tempo médio de sincronização para a publicação de mesclagem|  
|**mergePerformance**|**int**|Desempenho da última sincronização comparada com todas as sincronizações à assinatura, com base na taxa de entrega da última sincronização dividida pela média de todas as taxas de entrega anteriores.|  
|**mergelatestsessionrunduration**|**int**|Duração da execução mais recente do Merge Agent.|  
|**mergelatestsessionrunspeed**|**float(53)**|Taxa de entrega da execução mais recente do Merge Agent.|  
|**mergelatestsessionconnectiontype**|**int**|Conexão usada para a sessão mais recente do Merge Agent, que pode ser um dos seguintes valores:<br /><br /> **1** = rede local (LAN)<br /><br /> **2** = conexão de rede dial-up|  
|**retention_period_unit**|**tinyint**|Define a unidade usada ao definir retenção, que pode ter um destes valores:<br /><br /> **1** = semana<br /><br /> **2** = mês<br /><br /> **3** = ano|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar a replicação de forma programática](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replmonitorhelpsubscription ](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replmonitorhelppublication ](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replmonitorhelppublisher ](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replmonitorhelpmergesession ](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replmonitorhelppublicationthresholds ](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replmonitorhelpmergesessiondetail ](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
