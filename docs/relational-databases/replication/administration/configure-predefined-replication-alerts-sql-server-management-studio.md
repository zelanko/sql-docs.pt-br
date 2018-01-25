---
title: "Configurar alertas de replicação predefinidos (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a88d254d198f88a04ad99f987d4641abc575505d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>Configurar alertas de replicação predefinidos (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A replicação oferece os seguintes alertas predefinidos que podem ser configurados para responder aos eventos de replicação:  
  
-   **Replicação: êxito do agente**  
  
-   **Replicação: falha do agente**  
  
-   **Replicação: repetição do agente**  
  
-   **Replicação: assinatura expirada cancelada**  
  
-   **Replicação: assinatura reinicializada após falha de validação**  
  
-   **Replicação: falha na validação de dados do assinante**  
  
-   **Replicação: êxito na validação de dados do assinante**  
  
-   **Replicação: desligamento personalizado do agente**  
  
 Configure esses alertas na pasta **Alertas** no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou na guia **Avisos** no Replication Monitor. Para obter mais informações sobre como acessar essa guia, consulte [Exibir informações e executar tarefas para uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md).  
  
 Além desses alertas, o Replication Monitor fornece um conjunto de avisos e alertas relacionado ao status e ao desempenho. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). Também é possível definir alertas para outros eventos de replicação por meio da infraestrutura de alerta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Criar um evento definido pelo usuário](http://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879).  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Para configurar um alerta de replicação predefinido no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e então, expanda a pasta **Alertas** .  
  
3.  Clique com o botão direito do mouse em um alerta de replicação e então clique em **Propriedades**.  
  
4.  Defina opções na caixa de diálogo **Propriedades do alerta \<AlertName>**:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
         Se o alerta for **Replicação: falha na validação de dados do assinante**, você poderá especificar o trabalho de resposta que a replicação fornecerá a esse alerta: selecione **Executar trabalho**e, então, clique no botão de busca (**…**). Na caixa de diálogo **Localizar trabalho** , clique em **Procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>Para configurar um alerta para um limite no Replication Monitor  
  
1.  Na guia **Avisos** clique em **Configurar Alertas**.  
  
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.  
  
3.  Defina opções na caixa de diálogo **Propriedades do alerta \<AlertName>**:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
         Se o alerta for **Replicação: falha na validação de dados do assinante**, você poderá especificar o trabalho de resposta que a replicação fornecerá a esse alerta: selecione **Executar trabalho**e, então, clique no botão de busca (**…**). Na caixa de diálogo **Localizar trabalho** , clique em **Procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar Alertas para eventos do Agente de Replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  
