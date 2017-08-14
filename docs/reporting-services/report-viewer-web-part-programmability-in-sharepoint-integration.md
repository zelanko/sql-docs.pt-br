---
title: "Relatório de programabilidade do Web Part visualizador na integração do SharePoint | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 9339b0f383efd757e9be49271f4a5bdd2d7a4d4f
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>Programabilidade do Web Part do Visualizador de Relatórios na Integração do SharePoint
  A Web Part do Visualizador de relatórios é um controle de servidor, que contém um conjunto de público de programação de aplicativo (API) de interfaces que permite aos desenvolvedores criar aplicativos do SharePoint personalizados. Você pode criar Web Parts personalizadas que fornecem o caminho do relatório e parâmetros para a Web Part do Visualizador de Relatórios que usa conexões de Web Part. Você também pode inserir a Web Part em uma página personalizada de Web Parts do SharePoint e personalizá-la usando a API pública.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>Conectando-se a uma Web Part do Visualizador de Relatórios com Web Parts personalizadas  
 A Web Part do Visualizador de relatórios é um consumidor de conexão para Web Parts do SharePoint que implementam <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> ou T:Microsoft.SharePoint.WebPartPages.IFilterValues. Um <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web Part, como o **documentos** Web Part pode fornecer um caminho de relatório para um relatório de Web Part do visualizador quando colocada na mesma página de Web Part que a Web Part do Visualizador de relatórios. Da mesma forma, um T:Microsoft.SharePoint.WebPartPages.IFilterValues Web Part, como o **filtro de texto** ou **escolher filtro**, pode fornecer um parâmetro de relatório para um relatório de Web Part do visualizador quando colocada na mesma página de Web Part que a Web Part do Visualizador de relatórios.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>Implementando um provedor de caminho de relatório com IWebPartRow  
 Para fornecer um caminho de relatório à Web Part do Visualizador de Relatórios através de conexões de Web Parts, faça o seguinte:  
  
1.  Crie uma Web Part que implemente a interface <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>.  
  
2.  Adicione a Web Part à mesma página de Web Parts da Web Part do Visualizador de Relatórios.  
  
3.  Conecte sua Web Part à Web Part do Visualizador de Relatórios na interface de usuário de design de Web Parts na Web.  
  
    > [!NOTE]  
    >  Você pode conectar somente uma <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web Part para a Web Part de Visualizador de relatório por vez e você não pode conectar um <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web e uma Web Part de T:Microsoft.SharePoint.WebPartPages.IFilterValues para a Web Part de Visualizador de relatórios ao mesmo tempo.  
  
 Para o <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web Part para funcionar corretamente com o T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart, você deve fazer o seguinte no <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> método:  
  
-   Invoque o método de retorno de chamada com um objeto <xref:System.Data.DataRowView> como o parâmetro de entrada.  
  
-   Verifique se o objeto <xref:System.Data.DataRowView> contém uma coluna chamada "DocUrl", que contém o caminho do relatório.  
  
    > [!NOTE]  
    >  A Web Part do Visualizador de Relatórios no suplemento do [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 também permite o recebimento do caminho do relatório, utilizando a coluna "FileRef."  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>Implementando um provedor de parâmetro de relatório com IFilterValues  
 Uma Web Part que implemente T:Microsoft.SharePoint.WebPartPages.IFilterValues pode fornecer um valor de parâmetro para a Web Part do Visualizador de relatórios. O valor de parâmetro enviado à Web Part do Visualizador de Relatórios está sujeito às mesmas restrições impostas ao parâmetro de relatório especificadas na definição do relatório, como tipo de dados, valores válidos, etc.  
  
 Para fornecer um parâmetro de relatório à Web Part do Visualizador de Relatórios, faça o seguinte:  
  
1.  Crie uma Web Part que implementa a interface T:Microsoft.SharePoint.WebPartPages.IFilterValues.  
  
2.  Adicione a Web Part à mesma página como o T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart.  
  
3.  Conecte-se a Web Part de T:Microsoft.SharePoint.WebPartPages.IFilterValues para a Web Part de Visualizador de relatórios na interface do usuário de design da Web Part baseada na Web.  
  
    > [!NOTE]  
    >  Você pode conectar várias Web Parts de T:Microsoft.SharePoint.WebPartPages.IFilterValues para a Web Part do Visualizador de relatórios por vez. No entanto, você não pode conectar um <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web e uma Web Part de T:Microsoft.SharePoint.WebPartPages.IFilterValues para a Web Part de Visualizador de relatórios ao mesmo tempo.  
  
  
