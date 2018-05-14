---
title: MSSQL_ENG014161 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014161 error
ms.assetid: 4b983e76-bb77-43c5-b44b-19919d3da619
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e06b9d0eb7f6249d6f386fb256845fe44fcef4ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mssqleng014161"></a>MSSQL_ENG014161
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14161|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O limite [%s:%s] da publicação [%s] foi definido. Verifique se o leitor de log e os agentes de distribuição estão em execução e atendem ao requisito de latência.|  
  
## <a name="explanation"></a>Explicação  
 A replicação permite habilitar avisos para várias condições. Isso inclui exceder uma latência especificada para assinaturas transacionais. Latência é o período entre a confirmação de uma alteração de dados no Publicador e a confirmação da alteração correspondente no Assinante.  
  
 Ao habilitar um aviso usando o Replication Monitor ou o [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), você especifica um limite que determina quando um aviso é disparado. Quando esse limite é atingido ou excedido, um aviso é exibido no Replication Monitor e um evento é gravado no log de eventos do Windows. Ao atingir um limite, também é possível disparar um alerta do SQL Server Agent. Para obter mais informações, consulte [Definir limites e avisos no Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Monitorar a replicação de forma programática](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Se uma assinatura exceder um limite de latência, será necessário determinar se há um problema de desempenho no sistema ou se o limite deve ser ajustado. Após configurar a replicação, desenvolva uma linha de base de desempenho, a qual permitirá determinar como a replicação se comporta com uma carga de trabalho típica para seus aplicativos e topologia. Inclua a latência nessa linha de base de forma que seja possível definir um valor apropriado para o limite.  
  
 Se o valor do limite for apropriado, mas estiver sendo excedido, será necessário determinar se há algum gargalo no desempenho do sistema. Para obter mais informações sobre como monitorar e solucionar problemas relacionados a desempenho de replicação, consulte os seguintes tópicos:  
  
-   [Measure Latency and Validate Connections for Transactional Replication](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
-   [Monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
