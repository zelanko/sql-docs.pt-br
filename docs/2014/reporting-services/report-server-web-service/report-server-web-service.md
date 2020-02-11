---
title: Serviço Web Servidor de Relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
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
manager: kfile
ms.openlocfilehash: b577fd9a78dbb5f12af79e190709065931ec463a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62520548"
---
# <a name="report-server-web-service"></a>serviço Web Servidor de Relatórios
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece acesso à funcionalidade completa do servidor de relatório por meio do serviço Web servidor de relatórios. O serviço Web Servidor de Relatórios é um serviço Web XML com uma API SOAP. Usa o SOAP sobre HTTP e age como uma interface de comunicações entre programas cliente e o servidor de relatório. O serviço Web oferece dois pontos de extremidade - um para a execução de relatórios e outro para o gerenciamento de relatórios - com métodos que exibem a funcionalidade do servidor de relatório e permitem que você crie ferramentas personalizadas para qualquer parte do ciclo e vida.  
  
 Existem três modos principais para desenvolver aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com base no serviço Web. Você pode:  
  
-   Desenvolva aplicativos [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o SDK. Para obter mais informações sobre como usar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para criar aplicativos de serviço Web, consulte [Criando aplicativos usando o serviço Web e o .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
-   Desenvolver aplicativos com o utilitário **rs** (RS.exe), o ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Com os scripts do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], você pode executar qualquer uma das operações do serviço Web Servidor de Relatórios. Para obter mais informações sobre scripts no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Gerar scripts com o Utilitário rs.exe e o serviço Web](../tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
-   Desenvolver aplicativos usando qualquer conjunto de ferramentas de desenvolvimento habilitado para SOAP. Para obter mais informações, consulte [Função do SOAP no Reporting Services](../report-server-web-service/the-role-of-soap-in-reporting-services.md).  
  
## <a name="programming-diagram"></a>Diagrama de programação  
 ![Opções de implantação do serviço Web do Servidor de Relatório](../../../2014/reporting-services/media/reportserviceswebserviceprog-01.gif "Opções de implantação do serviço Web do Servidor de Relatório")  
Opções de desenvolvimento disponíveis para serviço Web do Reporting Services  
  
## <a name="in-this-section"></a>Nesta seção  
 [Métodos de serviço Web Servidor de Relatórios](../report-server-web-service/methods/report-server-web-service-methods.md)  
 Descreve os recursos e os métodos de cada serviço Web Servidor de Relatórios.  
  
 [The Role of SOAP in Reporting Services](../report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 Oferece uma visão geral de SOAP e como ele é usado nos serviços Web Servidor de Relatório.  
  
 [Acessando a API SOAP](../report-server-web-service/accessing-the-soap-api.md)  
 Descreve o WSDL (Web Service Description Language) e fornece as URLs para acessar um arquivo do WSDL do Reporting Services.  
  
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Contém informações sobre como desenvolver aplicativos e serviços Web que chamam a API SOAP do Reporting Services.  
  
 [Gerar scripts com o utilitário rs.exe e o serviço Web](../tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 Oferece uma visão geral do ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 [Referência técnica &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)  
 Contém material de referência específico dos métodos e dos tipos complexos correspondentes dos serviços Web Servidor de Relatório.  
  
## <a name="user-requirements-for-web-service-development"></a>Requisitos de usuário para o desenvolvimento de serviço Web  
 Para desenvolver aplicativos usando o serviço Web Servidor de Relatórios, você precisa:  
  
-   
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 5.5 ou posterior instalado em um computador com uma conexão com a Internet e acesso ao servidor de relatório.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK instalado em um computador se você quiser desenvolver e implantar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativos usando o. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  
  
-   Uma compreensão detalhada dos recursos e das capacidades do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Uma sólida compreensão de SOAP e de [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)].  
  
-   Experiência de desenvolvimento em [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]uma linguagem compatível, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] como ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], se você planeja usar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] como sua plataforma de desenvolvimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Web do Servidor de Relatório](../report-server-web-service/report-server-web-service.md)  
  
  
