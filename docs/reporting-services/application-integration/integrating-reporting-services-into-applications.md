---
title: Integrando o Reporting Services em aplicativos | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 64f4e77a943f1d71fc7655a4a1d36dffafe7afcf
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175139"
---
# <a name="integrating-reporting-services-into-applications"></a>Integrando o Reporting Services em aplicativos

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é uma plataforma de relatório aberta e extensível criada para fornecer aos desenvolvedores um conjunto abrangente de APIs para soluções de desenvolvimento.

> [!NOTE]
> A partir do SQL Server 2017 Reporting Services, o acesso à API REST está disponível para o desenvolvimento de soluções. O acesso à API SOAP foi preterido. Para obter mais informações, consulte [Desenvolver com as APIs REST do Reporting Services](../developer/rest-api.md).
  
 Há três opções para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a aplicativos personalizados: o serviço Web do Servidor de Relatórios, também conhecido como a API SOAP do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], os controles do Visualizador de Relatórios do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e o acesso à URL. Cada opção fornece uma abordagem diferente para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com os aplicativos.
  
## <a name="report-server-web-service"></a>Serviço Web de servidor de relatório

 O serviço Web Servidor de Relatórios é a principal interface de desenvolvimento no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esteja você desenvolvendo código para gerenciar o seu catálogo de relatórios ou desenvolvendo código para renderizar relatórios em um formato suportado, o serviço Web exibe todos os métodos necessários para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos. Um exemplo desse aplicativo é o portal da Web, incluído no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; ele usa o serviço Web para gerenciar o banco de dados do servidor de relatório.  
  
## <a name="report-viewer-controls-for-visual-studio"></a>Controles do Visualizador de Relatórios para Visual Studio

 Os controles do Visualizador de Relatórios disponíveis para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] são usados para integrar a exibição de relatório aos aplicativos. Existem dois controles: um para aplicativos baseados em Windows Forms e um para aplicativos Web Forms. Cada controle oferece o recurso de exibição de relatórios implantados como um servidor de relatório além da capacidade de renderizar relatórios existentes em um ambiente onde um servidor de relatório não foi instalado.  
  
## <a name="url-access"></a>acesso à URL  
 O acesso à URL será outra opção para integrar a exibição de relatório aos seus aplicativos, se os controles ReportViewer não forem uma opção. Além disso, o acesso à URL é útil para enviar aos usuários, por email, links para relatórios.  
  
## <a name="in-this-section"></a>Nesta seção

 [Integração do Reporting Services usando SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Descreve como integrar a navegação de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o gerenciamento aos seus aplicativos comerciais existentes usando o serviço Web Servidor de Relatórios.  
  
 [Integrando o Reporting Services usando os controles do Visualizador de Relatórios](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Descreve como integrar a exibição de relatório aos seus aplicativos existentes usando os controles doo Visualizador de Relatórios.  
  
 [Integração do Reporting Services usando o acesso à URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Descreve como integrar navegação de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos comerciais existentes usando o acesso à URL.  
  
## <a name="next-steps"></a>Próximas etapas

Para decidir sobre como usar o acesso à URL ou as APIs SOAP, consulte [Escolhendo entre o acesso à URL e o SOAP no Reporting Services](choosing-between-url-access-and-soap.md).

Para obter informações sobre a API REST do SQL Server 2017 Reporting Services, consulte [Desenvolver com as APIs REST para o Reporting Services](../developer/rest-api.md).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
