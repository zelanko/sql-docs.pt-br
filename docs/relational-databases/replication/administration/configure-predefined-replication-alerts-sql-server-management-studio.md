---
title: Configurar alertas de replicação predefinidos (SSMS)
description: Saiba como configurar alertas de replicação predefinidos usando o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1dd36895604f81e378b37d2d711c814251ee7cd7
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892416"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>Configurar alertas de replicação predefinidos (SQL Server Management Studio)
[!INCLUDE[applies-to-version/_ssnoversion.md](../../../includes/applies-to-version/sqlserver.md)]
  A replicação oferece os seguintes alertas predefinidos que podem ser configurados para responder aos eventos de replicação:  
  
-   **Replicação: êxito do agente**  
  
-   **Replicação: falha do agente**  
  
-   **Replicação: repetição do agente**  
  
-   **Replicação: assinatura expirada cancelada**  
  
-   **Replicação: assinatura reinicializada após falha de validação**  
  
-   **Replicação: falha na validação de dados do assinante**  
  
-   **Replicação: o assinante foi aprovado na validação de dados**  
  
-   **Replicação: desligamento personalizado do agente**  
  
 Configure esses alertas na pasta **Alertas** no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou na guia **Avisos** no Replication Monitor. Para obter mais informações sobre como acessar esta guia, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Além desses alertas, o Replication Monitor fornece um conjunto de avisos e alertas relacionado ao status e ao desempenho. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). Também é possível definir alertas para outros eventos de replicação por meio da infraestrutura de alerta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Criar um evento definido pelo usuário](../../../ssms/agent/create-a-user-defined-event.md).  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Para configurar um alerta de replicação predefinido no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e então, expanda a pasta **Alertas** .  
  
3.  Clique com o botão direito do mouse em um alerta de replicação e então clique em **Propriedades**.  
  
4.  Defina as opções na caixa de diálogo **Propriedades do alerta \<AlertName>** :  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
         Se o alerta for **Replicação: o assinante foi reprovado na validação de dados**, você poderá especificar o trabalho de resposta que a replicação fornecerá para este alerta: Selecione **Executar trabalho** e clique no botão Procurar ( **...** ). Na caixa de diálogo **Localizar trabalho** , clique em **Procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>Para configurar um alerta para um limite no Replication Monitor  
  
1.  Na guia **Avisos** clique em **Configurar Alertas**.  
  
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.  
  
3.  Defina as opções na caixa de diálogo **Propriedades do alerta \<AlertName>** :  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
         Se o alerta for **Replicação: o assinante foi reprovado na validação de dados**, você poderá especificar o trabalho de resposta que a replicação fornecerá para este alerta: Selecione **Executar trabalho** e clique no botão Procurar ( **...** ). Na caixa de diálogo **Localizar trabalho** , clique em **Procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **fechar**  
  
## <a name="see-also"></a>Consulte Também  
 [Usar Alertas para eventos do Agente de Replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
