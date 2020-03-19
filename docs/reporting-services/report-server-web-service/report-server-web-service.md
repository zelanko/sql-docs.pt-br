---
title: Serviço Web Servidor de Relatórios | Microsoft Docs
description: O Reporting Services fornece a funcionalidade do servidor de relatório com o serviço Web do Servidor de Relatórios, pontos de extremidade de serviço SOAP para execução e gerenciamento de relatórios.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6fb059d867a7a3448e5a842929df48ad009f2518
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198473"
---
# <a name="report-server-web-service"></a>serviço Web Servidor de Relatórios
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece acesso à funcionalidade completa do servidor de relatório por meio do serviço Web Servidor de Relatórios. O serviço Web Servidor de Relatórios é um serviço Web XML com uma API SOAP. Usa o SOAP sobre HTTP e age como uma interface de comunicações entre programas cliente e o servidor de relatório. O serviço Web oferece dois pontos de extremidade - um para a execução de relatórios e outro para o gerenciamento de relatórios - com métodos que exibem a funcionalidade do servidor de relatório e permitem que você crie ferramentas personalizadas para qualquer parte do ciclo e vida.  
  
 Existem três modos principais para desenvolver aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com base no serviço Web. Você pode:  
  
-   Desenvolver aplicativos usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e o SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre como usar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para criar aplicativos de serviço Web, consulte [Criando aplicativos usando o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
-   Desenvolver aplicativos com o utilitário **rs** (RS.exe), o ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Com os scripts do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], você pode executar qualquer uma das operações do serviço Web Servidor de Relatórios. Para obter mais informações sobre scripts no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Gerar scripts com o Utilitário rs.exe e o serviço Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
-   Desenvolver aplicativos usando qualquer conjunto de ferramentas de desenvolvimento habilitado para SOAP. Para obter mais informações, consulte [Função do SOAP no Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md).  
  
## <a name="programming-diagram"></a>Diagrama de programação  
 ![Opções de implantação do serviço Web Servidor de Relatórios](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "Opções de implantação do serviço Web Servidor de Relatórios")  
Opções de desenvolvimento disponíveis para serviço Web do Reporting Services  
  
## <a name="in-this-section"></a>Nesta seção  
 [Métodos de Serviço Web do Servidor de Relatório](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 Descreve os recursos e os métodos de cada serviço Web Servidor de Relatórios.  
  
 [A função de SOAP no Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 Oferece uma visão geral de SOAP e como ele é usado nos serviços Web Servidor de Relatório.  
  
 [Acessar a API SOAP](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 Descreve o WSDL (Web Service Description Language) e fornece as URLs para acessar um arquivo do WSDL do Reporting Services.  
  
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Contém informações sobre como desenvolver aplicativos e serviços Web que chamam a API SOAP do Reporting Services.  
  
 [Gerar scripts com o utilitário rs.exe e o serviço Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 Oferece uma visão geral do ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
 Contém material de referência específico dos métodos e dos tipos complexos correspondentes dos serviços Web Servidor de Relatório.  
  
## <a name="user-requirements-for-web-service-development"></a>Requisitos de usuário para o desenvolvimento de serviço Web  
 Para desenvolver aplicativos usando o serviço Web Servidor de Relatórios, você precisa:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 5.5 ou posterior instalado em um computador com uma conexão com a Internet e acesso ao servidor de relatório.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou o SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instalado em um computador caso deseje desenvolver e implantar aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
-   Uma compreensão detalhada dos recursos e das capacidades do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Uma sólida compreensão de SOAP e de [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)].  
  
-   Experiência de desenvolvimento em uma linguagem compatível com [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], caso pretenda usar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] como a plataforma de desenvolvimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Web do Servidor de Relatório](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
