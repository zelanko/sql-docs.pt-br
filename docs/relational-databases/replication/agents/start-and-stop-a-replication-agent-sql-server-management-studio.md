---
title: Iniciar ou parar um agente de replicação (SSMS)
description: Saiba como iniciar e parar um agente de replicação no SQL Server Management Studio e no Replication Monitor.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 01d44e823ef11a1e4bb481d7a7c710ffb95f76fb
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920604"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>Iniciar e interromper um Agente de Replicação (SQL Server Management Studio)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Inicie e pare os agentes nas pastas **Trabalhos** e **Replicação** do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e do Replication Monitor. Inicie e pare os seguintes agentes e trabalhos:  
  
-   O Agente de Instantâneo, que é usado por todas as publicações.  
  
-   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
-   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
-   O Agente de Distribuição que sincroniza as assinaturas para publicações transacionais e de instantâneo.  
  
-   O Agente de Mesclagem que sincroniza as assinaturas para publicações de mesclagem.  
  
-   Trabalhos de manutenção de replicação.  
  
 Para obter mais informações sobre como iniciar o Agente de Mesclagem e o Agente de Distribuição, consulte [Sincronizar uma assinatura push](../../../relational-databases/replication/synchronize-a-push-subscription.md) e [Sincronizar uma assinatura pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md). Para mais informações sobre trabalhos de manutenção, consulte [Executar trabalhos de manutenção de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>Para iniciar e parar um Agente de Instantâneo ou Agente de Leitor de Log a partir do Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor e a pasta **Replicação** .  
  
2.  Expanda a pasta **Publicações Locais** e clique com o botão direito do mouse em uma publicação.  
  
3.  Clique em **Exibir Status do Agente de Instantâneo** ou **Exibir Status do Agente de Leitor de Log**.  
  
4.  Clique em **Iniciar** ou em **Parar**.  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>Para iniciar e parar um Agente de Leitor de Fila a partir do Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito no trabalho para o agente e, então, clique em **Iniciar Trabalho** ou **Parar Trabalho**. O nome do trabalho para o Queue Reader Agent está no formato **[\<Distributor>].\<integer>** .  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>Para iniciar e parar um Agente de Instantâneo, Agente de Leitor de Log ou Agente de Leitor de Fila a partir do Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique com o botão direito em um agente e, então, clique em **Iniciar Agente** ou **Parar Agente**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Conceitos dos executáveis do Agente de Replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Visão geral dos agentes de replicação](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
