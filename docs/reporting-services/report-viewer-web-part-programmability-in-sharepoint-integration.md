---
title: "Programação da web part do Visualizador de Relatórios na integração do SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: "8"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fe234d83738bda4dd578d8be0a6d2c4619cd8b70
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>Programabilidade do Web Part do Visualizador de Relatórios na Integração do SharePoint
  A Web Part do Visualizador de Relatórios é um controle de servidor, que contém um conjunto de APIs (interfaces de programação de aplicativo) públicas, permitindo que os desenvolvedores criem aplicativos personalizados do SharePoint. Você pode criar Web Parts personalizadas que fornecem o caminho do relatório e parâmetros para a Web Part do Visualizador de Relatórios que usa conexões de Web Part. Você também pode inserir a Web Part em uma página personalizada de Web Parts do SharePoint e personalizá-la usando a API pública.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>Conectando-se a uma Web Part do Visualizador de Relatórios com Web Parts personalizadas  
 A Web Part do Visualizador de Relatórios é um consumidor de conexão para Web Parts do SharePoint que implementam <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> ou T:Microsoft.SharePoint.WebPartPages.IFilterValues. Uma Web Part <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>, como **Documents**, pode fornecer um caminho de relatório para uma Web Part do Visualizador de Relatórios quando colocada na mesma página de Web Part da Web Part do Visualizador de Relatórios. Da mesma forma, uma Web Part T:Microsoft.SharePoint.WebPartPages.IFilterValues, como **Filtro de Texto** ou **Escolher Filtro**, pode fornecer um parâmetro de relatório a uma Web Part do Visualizador de Relatórios quando colocada na mesma página de Web Part da Web Part do Visualizador de Relatórios.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>Implementando um provedor de caminho de relatório com IWebPartRow  
 Para fornecer um caminho de relatório à Web Part do Visualizador de Relatórios através de conexões de Web Parts, faça o seguinte:  
  
1.  Crie uma Web Part que implemente a interface <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>.  
  
2.  Adicione a Web Part à mesma página de Web Parts da Web Part do Visualizador de Relatórios.  
  
3.  Conecte sua Web Part à Web Part do Visualizador de Relatórios na interface de usuário de design de Web Parts na Web.  
  
    > [!NOTE]  
    >  Você pode conectar somente uma Web Part <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> à Web Part do Visualizador de Relatórios por vez e não pode conectar uma Web Part <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> e uma Web Part T:Microsoft.SharePoint.WebPartPages.IFilterValues à Web Part do Visualizador de Relatórios ao mesmo tempo.  
  
 Para que a Web Part <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> funcione corretamente com a T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart, faça o seguinte no método <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A>:  
  
-   Invoque o método de retorno de chamada com um objeto <xref:System.Data.DataRowView> como o parâmetro de entrada.  
  
-   Verifique se o objeto <xref:System.Data.DataRowView> contém uma coluna chamada "DocUrl", que contém o caminho do relatório.  
  
    > [!NOTE]  
    >  A Web Part do Visualizador de Relatórios no suplemento do [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 também permite o recebimento do caminho do relatório, utilizando a coluna "FileRef."  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>Implementando um provedor de parâmetro de relatório com IFilterValues  
 Uma Web Part que implementa T:Microsoft.SharePoint.WebPartPages.IFilterValues pode fornecer um valor de parâmetro para a Web Part do Visualizador de Relatórios. O valor de parâmetro enviado à Web Part do Visualizador de Relatórios está sujeito às mesmas restrições impostas ao parâmetro de relatório especificadas na definição do relatório, como tipo de dados, valores válidos, etc.  
  
 Para fornecer um parâmetro de relatório à Web Part do Visualizador de Relatórios, faça o seguinte:  
  
1.  Crie uma Web Part que implementa a interface T:Microsoft.SharePoint.WebPartPages.IFilterValues.  
  
2.  Adicione a Web Part à mesma página da T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart.  
  
3.  Conecte a Web Part T:Microsoft.SharePoint.WebPartPages.IFilterValues à Web Part do Visualizador de Relatórios na interface do usuário de design da Web Part baseada na Web.  
  
    > [!NOTE]  
    >  Você pode conectar várias Web Parts T:Microsoft.SharePoint.WebPartPages.IFilterValues à Web Part do Visualizador de Relatórios simultaneamente. No entanto, não é possível conectar uma Web Part <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> e uma Web Part T:Microsoft.SharePoint.WebPartPages.IFilterValues à Web Part do Visualizador de Relatórios ao mesmo tempo.  
  
  
