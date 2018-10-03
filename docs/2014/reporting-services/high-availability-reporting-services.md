---
title: Alta disponibilidade (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2c71fd13052c02b36c7b725e4058fd827076d6a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058346"
---
# <a name="high-availability-reporting-services"></a>Alta disponibilidade (Reporting Services)
  Um servidor de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é um servidor sem monitoração de estado que armazena dados de aplicativo, conteúdo, propriedades e informações de sessão em dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Como tal, a melhor maneira de garantir a disponibilidade de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] funcionalidade é fazer o seguinte:  
  
-   Use os recursos de alta disponibilidade a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] para maximizar o tempo de atividade dos bancos de dados de servidor de relatório. Se você configurar um [!INCLUDE[ssDE](../includes/ssde-md.md)] da instância para ser executado em um cluster de failover, você pode selecionar que instância quando você cria um banco de dados do servidor de relatório.  
  
-   Use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)] com os bancos de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e para fontes de dados, como for possível. Para obter mais informações, confira [Reporting Services com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Configure vários servidores de relatório para serem executados em uma implantação de expansão, onde todos os servidores compartilham um único banco de dados do servidor de relatório. A implantação de várias instâncias do servidor de relatório, de preferência em servidores diferentes, em uma implantação de expansão pode ajudar a fornecer serviço ininterrupto caso uma das instâncias deixe de funcionar.  
  
 Uma implantação de expansão fornece um meio de compartilhar um banco de dados. Se um servidor de relatório deixar de funcionar, outros servidores na mesma implantação continuarão funcionando.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá suporte a cluster. A implantação de expansão propriamente dita não fornece balanceamento de carga; ela não detecta as cargas de processamento em um servidor de relatório e roteia as novas solicitações de processamento para o servidor menos ocupado. As solicitações de processamento que falharam antes da conclusão não são roteadas novamente. Para obter os recursos de balanceamento, configure o balanceamento de carga para os servidores da Web que hospedam os servidores de relatório e, em seguida, configure os servidores de relatório em uma implantação de expansão para que compartilhem o mesmo banco de dados de servidor de relatório.  
  
 O serviço Web e o serviço Windows do servidor de relatório são integrados e executados juntos como uma única instância do servidor de relatório. Você não pode configurar a disponibilidade separadamente para cada serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Configurar uma implantação de expansão do servidor de relatório do modo nativo &#40;Configuration Manager do SSRS&#41;](install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
