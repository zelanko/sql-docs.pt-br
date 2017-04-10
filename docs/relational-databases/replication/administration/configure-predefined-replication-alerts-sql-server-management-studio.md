---
title: "Configurar alertas de replica&#231;&#227;o predefinidos (SQL Server Management Studio) | Microsoft Docs"
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
  - "alertas [replicação do SQL Server]"
  - "alertas de replicação predefinidos [replicação do SQL Server]"
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Configurar alertas de replica&#231;&#227;o predefinidos (SQL Server Management Studio)
  A replicação oferece os seguintes alertas predefinidos que podem ser configurados para responder aos eventos de replicação:  
  
-   **Replicação: êxito do agente**  
  
-   **Replicação: falha do agente**  
  
-   **Replicação: repetição do agente**  
  
-   **Replicação: assinatura expirada cancelada**  
  
-   **Replicação: assinatura reinicializada após falha de validação**  
  
-   **Replicação: falha na validação de dados do assinante**  
  
-   **Replicação: êxito na validação de dados do assinante**  
  
-   **Replicação: desligamento personalizado do agente**  
  
 Configure esses alertas no **alertas** pasta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou **avisos** guia no Replication Monitor. Para obter mais informações sobre como acessar essa guia, consulte [Exibir informações e executar tarefas para uma assinatura e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md).  
  
 Além desses alertas, o Replication Monitor fornece um conjunto de avisos e alertas relacionado ao status e ao desempenho. Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). Também é possível definir alertas para outros eventos de replicação por meio da infraestrutura de alerta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [criar um evento definido pelo usuário](../../../ssms/agent/create-a-user-defined-event.md).  
  
### Para configurar um alerta de replicação predefinido no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e então, expanda a pasta **Alertas** .  
  
3.  Clique com botão direito um alerta de replicação e, em seguida, clique em **propriedades**.  
  
4.  Definir opções no **\< AlertName> Propriedades de alerta** caixa de diálogo:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Sobre o **resposta** especifique se deve ser enviado um email e/ou um trabalho deve ser executado.  
  
         Se o alerta for **replicação: assinante Falha na validação de dados**, você pode especificar o trabalho de resposta que a replicação fornece para este alerta: selecione **Executar trabalho**, e, em seguida, clique no botão Procurar (**...**). Na caixa de diálogo **Localizar trabalho** , clique em **Procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para configurar um alerta para um limite no Replication Monitor  
  
1.  Na guia **Avisos** clique em **Configurar Alertas**.  
  
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.  
  
3.  Definir opções no **\< AlertName> Propriedades de alerta** caixa de diálogo:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Sobre o **resposta** especifique se deve ser enviado um email e/ou um trabalho deve ser executado.  
  
         Se o alerta for **replicação: assinante Falha na validação de dados**, você pode especificar o trabalho de resposta que a replicação fornece para este alerta: selecione **Executar trabalho**, e, em seguida, clique no botão Procurar (**...**). Na caixa de diálogo **Localizar trabalho** , clique em **Procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **Fechar**.  
  
## Consulte também  
 [Usar Alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  