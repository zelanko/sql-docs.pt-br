---
title: "Executar trabalhos de manuten&#231;&#227;o de replica&#231;&#227;o (SQL Server Management Studio) | Microsoft Docs"
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
  - "trabalhos [replica&amp;#231;&amp;#227;o do SQL Server]"
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Executar trabalhos de manuten&#231;&#227;o de replica&#231;&#227;o (SQL Server Management Studio)
  A replicação usa os seguintes trabalhos de manutenção:  
  
-   **Reinicializar assinaturas com falha na validação de dados**  
  
-   **Limpeza de histórico de agente: distribuição**  
  
-   **Atualizador de monitoramento de replicação para distribuição.**  
  
-   **Verificação de agentes de replicação**  
  
-   **Limpeza de distribuição: distribuição**  
  
-   **Limpeza de assinaturas expiradas**  
  
 Iniciar e interromper esses trabalhos do **trabalhos** pasta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e o **agentes** guia no Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md). Exibir e modificar propriedades de cada trabalho de **Propriedades do trabalho - \< trabalho>** caixa de diálogo, que está disponível na mesma pasta e guia.  
  
### Para iniciar ou parar um trabalho de manutenção de replicação no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Um trabalho de atalho e, em seguida, clique em **Iniciar trabalho** ou **Parar trabalho**.  
  
### Para iniciar ou parar um trabalho de manutenção de replicação no Replication Monitor  
  
1.  Expanda um Grupo do publicador no Replication Monitor e, então, selecione um Publicador.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique em um trabalho na grade e clique em **Iniciar trabalho** ou **Parar trabalho**.  
  
### Para exibir e modificar propriedades de um trabalho de manutenção de replicação no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Um trabalho de atalho e, em seguida, clique em **propriedades**.  
  
4.  No **Propriedades do trabalho - \< trabalho>** caixa de diálogo, modifique as propriedades se necessário e, em seguida, clique em **OK**.  
  
### Para exibir e modificar propriedades de um trabalho de manutenção de replicação no Replication Monitor  
  
1.  Expanda um Grupo do publicador no Replication Monitor e, então, selecione um Publicador.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique em um trabalho na grade e clique em **propriedades**.  
  
4.  No **Propriedades do trabalho - \< trabalho>** caixa de diálogo, modifique as propriedades se necessário e, em seguida, clique em **OK**.  
  
## Consulte também  
 [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Exibir informações e executar tarefas para um publicador & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  