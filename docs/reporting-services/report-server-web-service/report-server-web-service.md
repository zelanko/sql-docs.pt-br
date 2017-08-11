---
title: "Serviço Web do servidor de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 10769f49396bcf32d437e4bee9b04cbc2a3c8d9c
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-web-service"></a>serviço Web Servidor de Relatórios
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece acesso à funcionalidade completa do servidor de relatório por meio do serviço Web servidor de relatório. O serviço Web Servidor de Relatórios é um serviço Web XML com uma API SOAP. Usa o SOAP sobre HTTP e age como uma interface de comunicações entre programas cliente e o servidor de relatório. O serviço Web oferece dois pontos de extremidade - um para a execução de relatórios e outro para o gerenciamento de relatórios - com métodos que exibem a funcionalidade do servidor de relatório e permitem que você crie ferramentas personalizadas para qualquer parte do ciclo e vida.  
  
 Há três modos principais de desenvolver [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativos com base no serviço da Web. Você pode:  
  
-   Desenvolver aplicativos usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Para obter mais informações sobre como usar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para criar aplicativos de serviço Web, consulte [criando aplicativos que usam o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
-   Desenvolver aplicativos usando o **rs** utilitário (RS.exe), o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ambiente de script. Com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] scripts, você pode executar qualquer uma das operações de serviço Web servidor de relatório. Para obter mais informações sobre scripts no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [utilitário e o serviço Web de Script com o rs.exe](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
-   Desenvolver aplicativos usando qualquer conjunto de ferramentas de desenvolvimento habilitado para SOAP. Para obter mais informações, consulte [The Role of SOAP no Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md).  
  
## <a name="programming-diagram"></a>Diagrama de programação  
 ![Opções de desenvolvimento de serviço Web do servidor de relatório](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "opções de desenvolvimento de serviço Web servidor de relatório")  
Opções de desenvolvimento disponíveis para serviço Web do Reporting Services  
  
## <a name="in-this-section"></a>Nesta seção  
 [Métodos de Serviço Web do Servidor de Relatório](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 Descreve os recursos e os métodos de cada serviço Web Servidor de Relatórios.  
  
 [A função de SOAP no Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 Oferece uma visão geral de SOAP e como ele é usado nos serviços Web Servidor de Relatório.  
  
 [Acessar a API SOAP](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 Descreve o WSDL (Web Service Description Language) e fornece as URLs para acessar um arquivo do WSDL do Reporting Services.  
  
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Contém informações sobre como desenvolver aplicativos e serviços Web que chamam a API SOAP do Reporting Services.  
  
 [Script com o utilitário rs.exe e o serviço Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 Oferece uma visão geral do ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Referência técnica &#40; SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
 Contém material de referência específico dos métodos e dos tipos complexos correspondentes dos serviços Web Servidor de Relatório.  
  
## <a name="user-requirements-for-web-service-development"></a>Requisitos de usuário para o desenvolvimento de serviço Web  
 Para desenvolver aplicativos usando o serviço Web Servidor de Relatórios, você precisa:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]Internet Explorer 5.5 ou posterior instalado em um computador com uma conexão de Internet para e de acesso ao servidor de relatório.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK instalado em um computador para desenvolver e implantar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativos usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
-   Uma compreensão detalhada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recursos e funcionalidades.  
  
-   Uma sólida compreensão de SOAP e de [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)].  
  
-   Experiência de desenvolvimento em um [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-idioma compatível como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], se você planeja usar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] como sua plataforma de desenvolvimento.  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Web servidor de relatório](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
