---
title: "Exibir informa&#231;&#245;es e executar tarefas para um Publicador (Replication Monitor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Publicadores [replicação do SQL Server], tarefas do Replication Monitor"
  - "exibindo informações do Publicador"
  - "Publicadores [replicação do SQL Server], exibindo informações"
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Exibir informa&#231;&#245;es e executar tarefas para um Publicador (Replication Monitor)
  O Replication Monitor fornece as seguintes guias que exibem informações sobre o Publicador selecionado:  
  
-   **Publicações**  
  
     Essa guia exibe informações sobre todas as publicações no Publicador selecionado.  
  
-   **Lista de Observação da Assinatura**  
  
     Essa guia destina-se a exibir informações sobre as assinaturas de todas as publicações disponíveis no Publicador selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   **Agentes** guia  
  
     Essa guia exibe informações detalhadas sobre os agentes e trabalhos usados por todos os tipos de replicação. A guia também permite que você inicie e interrompa cada agente e trabalho.  
  
 Para exibir mais informações sobre as opções em cada guia, clique na guia no painel à direita e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para exibir informações e executar tarefas para um Publicador  
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.  
  
2.  Para exibir informações sobre todas as publicações, clique o **publicações** guia.  
  
3.  Para exibir informações sobre assinaturas, clique na guia **Lista de Observação da Assinatura** . Você também pode acessar informações mais detalhadas e realizar tarefas a partir dessa guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **Exibir detalhes**.  
  
    -   Para exibir as propriedades de uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **propriedades**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito e, em seguida, clique em **Iniciar sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **reinicializar assinatura**.  
  
4.  Para exibir informações sobre agentes, clique o **agentes** guia. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre um agente (como mensagens informativas e mensagens de erro), clique o agente e, em seguida, clique em **Exibir detalhes**.  
  
    -   Para exibir informações detalhadas sobre o trabalho que executa o agente (como a agenda, detalhes de etapa de trabalho e assim por diante), o agente de atalho e, em seguida, clique em **propriedades**.  
  
    -   Para gerenciar os perfis para o agente, clique o agente e, em seguida, clique em **perfil de agente**. Para obter mais informações, consulte [trabalhar com perfis do Replication Agent](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Para iniciar um agente não está em execução, clique o agente e, em seguida, clique em **Iniciar agente**.  
  
    -   Para interromper um agente está em execução, clique o agente e, em seguida, clique em **Parar agente**.  
  
## Consulte também  
 [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  