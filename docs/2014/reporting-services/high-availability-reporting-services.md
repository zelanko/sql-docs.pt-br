---
title: Alta disponibilidade (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: e1d11b2b53499b12a6a8a7dca262bc26ae777825
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010361"
---
# <a name="high-availability-reporting-services"></a>Alta disponibilidade (Reporting Services)
  Um servidor de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é um servidor sem monitoração de estado que armazena dados de aplicativo, conteúdo, propriedades e informações de sessão em dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Como tal, a melhor maneira de garantir a disponibilidade de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] funcionalidade é fazer o seguinte:  
  
-   Use os recursos de alta disponibilidade a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] para maximizar o tempo de funcionamento dos bancos de dados de servidor de relatório. Se você configurar um [!INCLUDE[ssDE](../includes/ssde-md.md)] da instância para executar em um cluster de failover, você pode selecionar que instância quando você cria um banco de dados do servidor de relatório.  
  
-   Use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)] com os bancos de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e para fontes de dados, como for possível. Para obter mais informações, confira [Reporting Services com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Configure vários servidores de relatório para serem executados em uma implantação de expansão, onde todos os servidores compartilham um único banco de dados do servidor de relatório. A implantação de várias instâncias do servidor de relatório, de preferência em servidores diferentes, em uma implantação de expansão pode ajudar a fornecer serviço ininterrupto caso uma das instâncias deixe de funcionar.  
  
 Uma implantação de expansão fornece um meio de compartilhar um banco de dados. Se um servidor de relatório deixar de funcionar, outros servidores na mesma implantação continuarão funcionando.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte a cluster. A implantação de expansão propriamente dita não fornece balanceamento de carga; ela não detecta as cargas de processamento em um servidor de relatório e roteia as novas solicitações de processamento para o servidor menos ocupado. As solicitações de processamento que falharam antes da conclusão não são roteadas novamente. Para obter os recursos de balanceamento, configure o balanceamento de carga para os servidores da Web que hospedam os servidores de relatório e, em seguida, configure os servidores de relatório em uma implantação de expansão para que compartilhem o mesmo banco de dados de servidor de relatório.  
  
 O serviço Web e o serviço Windows do servidor de relatório são integrados e executados juntos como uma única instância do servidor de relatório. Você não pode configurar a disponibilidade separadamente para cada serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Configurar uma implantação de expansão do servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  