---
title: "Atualizar dados no Replication Monitor | Microsoft Docs"
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
  - "atualizando dados"
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Atualizar dados no Replication Monitor
  No Replication Monitor, a janela principal e a janela de detalhes (as janelas abertas na janela principal) podem ser atualizadas automaticamente e manualmente. Para atualizar uma janela manualmente, pressione F5. Por padrão, a janela principal é atualizada a cada cinco segundos automaticamente; a taxa pode ser personalizada para cada Publicador.  
  
 Os dados exibidos no Replication Monitor são consultados de um cache; Para obter informações sobre a relação entre o cache e atualizando o Replication Monitor, consulte [cache, atualização e monitorar o desempenho da replicação](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md). Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para definir as opções de atualização para o Replication Monitor  
  
1.  Clique com botão direito um publicador no painel esquerdo do Replication Monitor e, em seguida, clique em **configurações do publicador**.  
  
2.  No **configurações do publicador** caixa de diálogo, defina a **atualização automática** e **taxa de atualização** Opções. O **atualização automática** configuração afeta a janela principal do Replication Monitor. O **taxa de atualização** configuração também afeta todas as janelas detalhes que são definidas para serem atualizadas automaticamente (alterações na configuração afetam apenas as janelas de detalhes abertas depois da alteração).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para especificar que uma janela de detalhe deverá atualizar automaticamente  
  
1.  Abra uma janela de detalhe no Replication Monitor. Por exemplo:  
  
    1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
    2.  Clique na guia **Todas as Assinaturas** .  
  
    3.  Clique em uma assinatura e, em seguida, clique em **Exibir detalhes**.  
  
2.  No **assinatura \< SubscriptionName>** janela de detalhes, clique em **ação**, e, em seguida, clique em **atualização automática**. A taxa de atualização é determinada pelo **taxa de atualização** definindo no **configurações do publicador** caixa de diálogo.  
  
## Consulte também  
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  