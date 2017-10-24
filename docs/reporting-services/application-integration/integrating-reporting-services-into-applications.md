---
title: Integrar o Reporting Services em aplicativos | Microsoft Docs
ms.custom: 
ms.date: 10/19/2017
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
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 26e1da5a720aab965d014cada16f85086e0f70a0
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="integrating-reporting-services-into-applications"></a>Integrando o Reporting Services em aplicativos

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é uma plataforma de relatório aberta e extensível criada para fornecer aos desenvolvedores um conjunto abrangente de APIs para soluções de desenvolvimento.

> [!NOTE]
> Começando com o Reporting Services do SQL Server de 2017, acesso à API REST está disponível para o desenvolvimento de soluções. Acesso de SOAP API foi preterido. Para obter mais informações, consulte [desenvolver com as APIs REST para o Reporting Services](../developer/rest-api.md).
  
 Há três opções para a integração de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em aplicativos personalizados: serviço Web do servidor de relatório, também conhecido como o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API SOAP, os controles ReportViewer para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e o acesso à URL. Cada opção fornece uma abordagem diferente para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com os aplicativos.
  
## <a name="report-server-web-service"></a>Serviço Web de servidor de relatório

 O serviço Web Servidor de Relatórios é a principal interface de desenvolvimento no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esteja você desenvolvendo código para gerenciar o seu catálogo de relatórios ou desenvolvendo código para renderizar relatórios em um formato suportado, o serviço Web exibe todos os métodos necessários para a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos. Um exemplo desse aplicativo é o Gerenciador de relatórios, que está incluído no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; ele usa o serviço da Web para gerenciar o banco de dados do servidor de relatório.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Controles ReportViewer do Visual Studio

 Os controles ReportViewer disponíveis para [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] são usados para a integração de exibição de relatório aos seus aplicativos. Existem dois controles: um para aplicativos baseados em Windows Forms e um para aplicativos Web Forms. Cada controle oferece o recurso de exibição de relatórios implantados como um servidor de relatório além da capacidade de renderizar relatórios existentes em um ambiente onde um servidor de relatório não foi instalado.  
  
## <a name="url-access"></a>acesso à URL  
 O acesso à URL é outra opção para a integração da exibição de relatório com os aplicativos, se os controles ReportViewer não forem uma opção. Além disso, o acesso à URL é útil para enviar aos usuários, por email, links para relatórios.  
  
## <a name="in-this-section"></a>Nesta seção

 [Integração do Reporting Services usando SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Descreve como integrar a navegação de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o gerenciamento aos seus aplicativos comerciais existentes usando o serviço Web Servidor de Relatórios.  
  
 [Integrando o Reporting Services usando os controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Descreve como integrar a exibição de relatório aos seus aplicativos existentes usando os controles ReportViewer.  
  
 [Integração do Reporting Services usando o acesso à URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Descreve como integrar navegação de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos comerciais existentes usando o acesso à URL.  
  
## <a name="next-steps"></a>Próximas etapas

Para decidir sobre como usar o acesso à URL ou as APIs de SOAP, consulte [escolhendo entre acesso à URL e SOAP no Reporting Services](choosing-between-url-access-and-soap.md).

Para obter informações sobre o SQL Server de 2017 REST API do Reporting Services, consulte [desenvolver com as APIs REST para o Reporting Services](../developer/rest-api.md).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
