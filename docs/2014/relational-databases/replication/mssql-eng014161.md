---
title: MSSQL_ENG014161 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014161 error
ms.assetid: 4b983e76-bb77-43c5-b44b-19919d3da619
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5624b58f95ca6a5f47af6269a2bd4cbc6a30033b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758188"
---
# <a name="mssqleng014161"></a>MSSQL_ENG014161
    
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
  
 Ao habilitar um aviso usando o Replication Monitor ou o [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql), você especifica um limite que determina quando um aviso é disparado. Quando esse limite é atingido ou excedido, um aviso é exibido no Replication Monitor e um evento é gravado no log de eventos do Windows. Ao atingir um limite, também é possível disparar um alerta do SQL Server Agent. Para obter mais informações, consulte [Definir limites e avisos no Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Monitorar a replicação de forma programática](monitor/monitoring-replication-overview.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Se uma assinatura exceder um limite de latência, será necessário determinar se há um problema de desempenho no sistema ou se o limite deve ser ajustado. Após configurar a replicação, desenvolva uma linha de base de desempenho, a qual permitirá determinar como a replicação se comporta com uma carga de trabalho típica para seus aplicativos e topologia. Inclua a latência nessa linha de base de forma que seja possível definir um valor apropriado para o limite.  
  
 Se o valor do limite for apropriado, mas estiver sendo excedido, será necessário determinar se há algum gargalo no desempenho do sistema. Para obter mais informações sobre como monitorar e solucionar problemas relacionados a desempenho de replicação, consulte os seguintes tópicos:  
  
-   [Medir a latência e validar as conexões para a replicação transacional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
-   [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
