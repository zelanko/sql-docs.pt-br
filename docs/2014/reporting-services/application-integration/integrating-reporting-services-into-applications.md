---
title: Integrando o Reporting Services em aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 993e6abe1df84f712f107f994b5a824e04d89467
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153566"
---
# <a name="integrating-reporting-services-into-applications"></a>Integrando o Reporting Services em aplicativos
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é uma plataforma de relatório aberta e extensível criada para fornecer aos desenvolvedores um conjunto abrangente de APIs para soluções de desenvolvimento.  
  
 Existem três opções para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a aplicativos personalizados: o serviço Web Servidor de Relatórios, também conhecido como a API SOAP do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], os controles ReportViewer do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] e o acesso à URL. Cada opção fornece uma abordagem diferente para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com os aplicativos.  
  
## <a name="report-server-web-service"></a>serviço Web Servidor de Relatórios  
 O serviço Web Servidor de Relatórios é a principal interface de desenvolvimento no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esteja você desenvolvendo código para gerenciar o seu catálogo de relatórios ou desenvolvendo código para renderizar relatórios em um formato suportado, o serviço Web exibe todos os métodos necessários para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos. Um exemplo desse aplicativo é o Gerenciador de Relatórios, incluído no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; ele usa o serviço Web para gerenciar o banco de dados do servidor de relatório.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Controles ReportViewer do Visual Studio  
 Os controles ReportViewer incluídos no [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] são usados para a integração da exibição de relatório com os aplicativos. Existem dois controles: um para aplicativos baseados em Windows Forms e um para aplicativos Web Forms. Cada controle oferece o recurso de exibição de relatórios implantados como um servidor de relatório além da capacidade de renderizar relatórios existentes em um ambiente onde um servidor de relatório não foi instalado.  
  
## <a name="url-access"></a>Acesso à URL  
 O acesso à URL é outra opção para a integração da exibição de relatório com os aplicativos, se os controles ReportViewer não forem uma opção. Além disso, o acesso à URL é útil para enviar aos usuários, por email, links para relatórios.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Integração do Reporting Services usando SOAP](../application-integration/integrating-reporting-services-using-soap.md)  
 Descreve como integrar a navegação de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o gerenciamento aos seus aplicativos comerciais existentes usando o serviço Web Servidor de Relatórios.  
  
 [Integrando o Reporting Services usando os controles ReportViewer](../application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Descreve como integrar a exibição de relatório aos seus aplicativos existentes usando os controles ReportViewer.  
  
 [Integração do Reporting Services usando o acesso à URL](../application-integration/integrating-reporting-services-using-url-access.md)  
 Descreve como integrar navegação de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos comerciais existentes usando o acesso à URL.  
  
## <a name="see-also"></a>Consulte também  
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Escolhendo entre o acesso à URL e SOAP](../../../2014/reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [Referência técnica &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service/report-server-web-service.md)  
  
  
