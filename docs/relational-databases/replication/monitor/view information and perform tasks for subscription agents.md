---
title: "Exibir informa&#231;&#245;es e executar tarefas para os agentes associados a uma assinatura (Replication Monitor) | Microsoft Docs"
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
  - "agentes [replicação do SQL Server], exibindo informações"
  - "exibindo informações do agente de replicação"
  - "agentes [replicação do SQL Server], tarefas do Replication Monitor"
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibir informa&#231;&#245;es e executar tarefas para os agentes associados a uma assinatura (Replication Monitor)
  O Replication Monitor fornece duas guias que permitem acesso às informações sobre o(s) agente(s) associado(s) a uma assinatura:  
  
-   **Todas as Assinaturas**  
  
     Essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Lista de Observação da Assinatura**  
  
     Essa guia destina-se a exibir informações sobre as assinaturas de todas as publicações disponíveis no Publicador selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para exibir informações e executar tarefas para os agentes associados a uma assinatura (guia Todas as Assinaturas)  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique o **todas as assinaturas** guia para exibir informações sobre as assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **Exibir detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes que é iniciada dependem do tipo de assinatura: para assinaturas de instantâneo, a guia é **distribuidor para assinante histórico**; para assinaturas transacionais, as guias são **histórico do distribuidor do publicador para**, **histórico de assinante do distribuidor para**, e **comandos não distribuídos**; para assinaturas de mesclagem, a guia é **histórico de sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com botão direito a assinatura e, em seguida, clique em **Iniciar sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **reinicializar assinatura**.  
  
    -   Para validar uma única assinatura de mesclagem, clique com botão direito a assinatura e, em seguida, clique em **Validar assinatura**. Para validar todas as assinaturas para uma publicação de mesclagem, clique com botão direito na publicação e, em seguida, clique em **Validar todas as assinaturas**; para validar todas as assinaturas para uma publicação transacional, com o botão direito na publicação e, em seguida, clique em **validar assinaturas**.  
  
    -   Para gerenciar os perfis para o agente, clique o agente e, em seguida, clique em **perfil de agente**. Para obter mais informações, consulte [trabalhar com perfis do Replication Agent](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
### Para exibir as informações e executar tarefas nos agentes associados a uma assinatura (guia Lista de Observação da Assinatura)  
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.  
  
2.  Clique o **lista de observação da assinatura** guia para exibir informações sobre as assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **Exibir detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes que é iniciada dependem do tipo de assinatura: para assinaturas de instantâneo, a guia é **distribuidor para assinante histórico**; para assinaturas transacionais, as guias são **histórico do distribuidor do publicador para**, **histórico de assinante do distribuidor para**, e **desempenho**; para assinaturas de mesclagem, a guia é **histórico de sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com botão direito a assinatura e, em seguida, clique em **Iniciar sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com botão direito a assinatura e, em seguida, clique em **reinicializar assinatura**.  
  
    -   Para validar uma única assinatura de mesclagem, clique com botão direito a assinatura e, em seguida, clique em **Validar assinatura**. Para validar todas as assinaturas para uma publicação de mesclagem, clique com botão direito na publicação e, em seguida, clique em **Validar todas as assinaturas**; para validar todas as assinaturas para uma publicação transacional, com o botão direito na publicação e, em seguida, clique em **validar assinaturas**.  
  
    -   Para gerenciar os perfis para o agente, clique o agente e, em seguida, clique em **perfil de agente**. Para obter mais informações, consulte [trabalhar com perfis do Replication Agent](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
## Consulte também  
 [Exibir informações e executar tarefas para uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  