---
title: "MSSQL_ENG014160 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG014160"
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG014160
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14160|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O limite [%s:%s] da publicação [%s] foi definido. Uma ou mais assinaturas nesta publicação expiraram.|  
  
## Explicação  
 A replicação permite habilitar avisos para várias condições. Isso inclui expiração de assinatura iminente. As assinaturas podem expirar se não forem sincronizadas dentro de um especificado *período de retenção*. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Quando você habilita um aviso usando o Monitor de replicação ou [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), especifique um limite que determina quando um aviso for disparado. Quando esse limite é atingido ou excedido, um aviso é exibido no Replication Monitor e um evento é gravado no log de eventos do Windows. Ao atingir um limite, também é possível disparar um alerta do SQL Server Agent. Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## Ação do usuário  
 A solução desse problema depende do motivo pelo qual o aviso foi gerado:  
  
-   Se o limite foi excedido, mas a assinatura ainda não expirou, sincronize a assinatura. Para obter mais informações, consulte [sincronizar dados](../../relational-databases/replication/synchronize-data.md).  
  
-   Se o agente estiver em execução, mas não estiver replicando alterações corretamente, isso pode fazer com que a assinatura expire. Para replicação transacional, certifique-se de que o Distribution Agent e o Log Reader Agent estão em execução. Para replicação de mesclagem, certifique-se de que o Merge Agent está em execução. Para obter informações sobre como iniciar esses agentes, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Se a assinatura tiver expirado, será necessário reiniciar ou descartar e recriar a assinatura, dependendo do tipo de assinatura e há quanto tempo expirou. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  