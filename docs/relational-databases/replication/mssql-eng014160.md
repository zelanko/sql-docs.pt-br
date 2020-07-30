---
title: MSSQL_ENG014160 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014160 error
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 61ad945ab4635430631ac2b05691a117ac4215f5
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363126"
---
# <a name="mssql_eng014160"></a>MSSQL_ENG014160
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14160|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O limite [%s:%s] da publicação [%s] foi definido. Uma ou mais assinaturas nesta publicação expiraram.|  
  
## <a name="explanation"></a>Explicação  
 A replicação permite habilitar avisos para várias condições. Isso inclui expiração de assinatura iminente. As assinaturas podem expirar se não forem sincronizadas em um *período de retenção*especificado. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Ao habilitar um aviso usando o Replication Monitor ou o [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), você especifica um limite que determina quando um aviso é disparado. Quando esse limite é atingido ou excedido, um aviso é exibido no Replication Monitor e um evento é gravado no log de eventos do Windows. Ao atingir um limite, também é possível disparar um alerta do SQL Server Agent. Para obter mais informações, consulte [Definir limites e avisos no Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Monitorar a replicação de forma programática](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## <a name="user-action"></a>Ação do usuário  
 A solução desse problema depende do motivo pelo qual o aviso foi gerado:  
  
-   Se o limite foi excedido, mas a assinatura ainda não expirou, sincronize a assinatura. Para obter mais informações, consulte [Sincronizar dados](../../relational-databases/replication/synchronize-data.md).  
  
-   Se o agente estiver em execução, mas não estiver replicando alterações corretamente, isso pode fazer com que a assinatura expire. Para replicação transacional, certifique-se de que o Distribution Agent e o Log Reader Agent estão em execução. Para replicação de mesclagem, certifique-se de que o Merge Agent está em execução. Para obter informações sobre como iniciar esses agentes, consulte [iniciar e parar um Replication Agent &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do agente de replicação](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Se a assinatura tiver expirado, será necessário reiniciar ou descartar e recriar a assinatura, dependendo do tipo de assinatura e há quanto tempo expirou. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
