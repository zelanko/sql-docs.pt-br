---
title: SQL Server, Broker – objeto Transporte DBM | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: bf22e4f825d29a107f86fb486924b40da5af3752
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787329"
---
# <a name="sql-server-broker---dbm-transport-object"></a>Objeto SQL Server, Broker – DBM Transport
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto de desempenho **Broker / DBM Transport** contém contadores de desempenho que relatam informações sobre o sistema de rede do Service Broker e do espelhamento de banco de dados. A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Contador SQL Server Broker / DBM Transport|DESCRIÇÃO|  
|------------------------------------------------|-----------------|  
|**Bytes Atuais de E/S de Recebimento**|Esse contador informa o número de bytes a ser lido pelas operações de recebimento de transporte em execução.|  
|**Bytes Atuais de E/S de Envio**|Esse contador informa o número total de bytes de fragmentos de mensagens que estão no processo de envio pela rede.|  
|**Fragmentos de Mens. Atuais de E/S de Envio**|Esse contador informa o número total de fragmentos de mensagens que estão no processo de envio pela rede.|  
|**Envios de Fragmento de Mensagem P1/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 1 enviados pela rede por segundo.|  
|**Envios de Fragmento de Mensagem P2/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 2 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P3/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 3 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P4/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 4 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P5/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 5 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P6/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 6 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P7/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 7 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P8/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 8 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P9/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 9 enviados pela rede por segundo.|  
|**Envios de Fragmentos de Mensagem P10/s**|Esse contador informa o número de fragmentos de mensagem de prioridade 10 enviados pela rede por segundo.|  
|**Recebimentos de Fragmento de Mensagem/s**|Esse contador informa o número de fragmentos de mensagem recebidos pela rede por segundo.|   
|**Envios de Fragmentos de Mensagem/s**|Esse contador informa o número de fragmentos de mensagem de todas as prioridades enviados pela rede por segundo.|  
|**Tam. Méd. Receb. de Frag. de Mensagem**|Esse contador informa o tamanho médio dos fragmentos de mensagem recebidos pela rede.|  
|**Base do Tam. Méd. de Receb. de Frag. de Mensagem**|Apenas para uso interno.| 
|**Tam. Médio de Envios de Fragmento de Mensagem**|Esse contador informa o tamanho médio dos fragmentos de mensagem enviados pela rede.|  
|**Base do Tam. Méd. de Envios de Frag. de Mensagem**|Apenas para uso interno.|
|**Contagem de Conexão Aberta**|Esse contador informa o número de conexões de rede abertas no Service Broker.|  
|**Bytes Pend. de E/S de Recebimento**|Esse contador informa o número de bytes contidos nos fragmentos de mensagem que foram recebidos pela rede mas que ainda não foram colocados em fila nem descartados.|  
|**Bytes Pendentes de E/S de Envio**|Esse contador informa o número total de bytes em fragmentos de mensagens que estão prontos para serem enviados pela rede.|  
|**Frag. de Mens. Pend. de E/S de Envio**|Esse contador informa o número de fragmentos de mensagem que foram recebidos pela rede mas que ainda não foram colocados em fila nem descartados.|  
|**Fragmentos de Mens. Pend. de E/S de Envio**|Esse contador informa o número total de fragmentos de mensagens que estão prontos para serem enviados pela rede.|  
|**Bytes de E/S de recebimento/s**|Esse contador informa o número total de bytes por segundo recebidos pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|  
|**Total de Bytes de E/S de Recebimento**|Esse contador informa o número total de bytes recebidos pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|  
|**Tam. Médio de E/S de Recebimento**|Esse contador informa o número médio de bytes de uma operação de recebimento de transporte.|  
|**Base do Tam. Méd. de E/S de Recebimento**|Apenas para uso interno.|
|**E/Ss de Recebimento/s**|Esse contador informa o número de operações de E/S de recebimento de transporte por segundo que a camada de transporte do Service Broker / DBM concluiu. Observe que uma operação de recebimento de transporte pode conter mais de um fragmento de mensagem.|  
|**Bytes de Cópias de Buffer de E/S de Receb./s**|A taxa na qual as operações de E/S de recebimento de transporte tiveram de mover os fragmentos de buffer na memória.|
|**Contagem de Cópias de Buffer de E/S de Recebimento**|O número de vezes que as operações de E/S de recebimento de transporte tiveram de mover fragmentos de buffer na memória.| 
|**Bytes de E/S de Envio/s**|Esse contador informa o número total de bytes por segundo enviados pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.|   
|**Total de Bytes de E/S de Envio**|Esse contador informa o número total de bytes enviados pela rede pelos terminais do Service Broker e do Espelhamento de Banco de Dados.| 
|**Tamanho Médio de E/S de Envio**|Esse contador informa o tamanho médio em bytes de cada operação de envio de transporte. Observe que uma operação de envio de transporte pode conter mais de um fragmento de mensagem.|  
|**Base do Tam. Médio de E/S de Envio**|Apenas para uso interno.|
|**E/S de Envio/s**|Esse contador informa o número de operações de E/S de envio de transporte por segundo que foram concluídas. Observe que uma operação de envio de transporte pode conter mais de um fragmento de mensagem.|  
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
