---
title: "Configurar alertas de replicação predefinidos (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fdd1352c4f7f6c62c8adfc5fcf9b2932568c12d1
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>Configurar alertas de replicação predefinidos (SQL Server Management Studio)
  A replicação oferece os seguintes alertas predefinidos que podem ser configurados para responder aos eventos de replicação:  
  
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
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó do servidor.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Usar Alertas para eventos do Agente de Replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  

