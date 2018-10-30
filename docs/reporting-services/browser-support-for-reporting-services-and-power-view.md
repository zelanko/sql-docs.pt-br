---
title: Suporte ao navegador para o Reporting Services e o Power View | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- scripts [Reporting Services], requirements
- viewing reports
- browsers [Reporting Services]
- Web browsers [Reporting Services], about browser support
- browsing reports [Reporting Services]
- components [Reporting Services], browsers
- Web browsers [Reporting Services]
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7282fd5627bc46d9f392a449c4707c75c867dd92
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50021202"
---
# <a name="browser-support-for-reporting-services-and-power-view"></a>Suporte ao navegador para Reporting Services e Power View

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Saiba mais sobre quais versões de navegador têm suporte para gerenciar e exibir o SQL Server Reporting Services, os Controles ReportViewer e o Power View.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="browser-requirements-for-the-web-portal"></a>Requisitos de navegador para o portal da Web

Veja a seguir a lista atual de navegadores com suporte para o portal da Web.

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*
- Microsoft Edge (+)
- Microsoft Internet Explorer 10 ou 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple iOS**  
*iPhone e iPad com iOS 9*

- Apple Safari (+)

**Google Android**  
*Telefones e tablets com Android 4.4 (KitKat) ou posterior*

- Google Chrome (+)

 **(+)** A versão lançada mais recente

## <a name="browser-requirements-for-the-reportviewer-web-control-2015"></a>Requisitos de navegador para o controle da Web do ReportViewer (2015)

 Veja a seguir uma lista atual de navegadores com suporte com o controle da Web do ReportViewer (2015). O visualizador de relatórios dá suporte à exibição de relatórios do portal da Web [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e de bibliotecas do SharePoint.  

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 ou 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)

 **(+)** A versão lançada mais recente

 Se você estiver usando um produto SharePoint integrado ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], confira  [Planejar suporte ao navegador no SharePoint 2016](https://technet.microsoft.com//library/cc263526\(v=office.16\).aspx).

### <a name="authentication-requirements"></a>Requisitos de autenticação

 Os navegadores dão suporte a esquemas de autenticação específicos que devem ser tratados pelo servidor de relatório para que a solicitação do cliente seja bem-sucedida. A tabela a seguir identifica os tipos de autenticação padrão com suporte por cada navegador que é executado em um sistema operacional Windows.

|**Tipo de navegador**|**Suporta**|**Padrão de navegador**|**Padrão de servidor**|
|----------------------|------------------|-------------------------|------------------------|
|**Microsoft Edge** (+)|Negotiate, Kerberos, NTLM, Basic|Negotiate|Sim. As configurações de autenticação padrão funcionam com o Edge.|
|**Microsoft Internet Explorer**|Negotiate, Kerberos, NTLM, Basic|Negotiate|Sim. As configurações de autenticação padrão funcionam com o Internet Explorer.|
|**Google Chrome**(+)|Negotiate, NTLM, Basic|Negotiate|Sim. As configurações de autenticação padrão funcionam com o Chrome.|
|**Mozilla Firefox**(+)|NTLM, Basic|NTLM|Sim. As configurações de autenticação padrão funcionam com o Firefox.|
|**Apple Safari**(+)|NTLM, Basic|Basic|Sim. As configurações de autenticação padrão funcionam com o Safari.|

 **(+)** A versão lançada mais recente

### <a name="script-requirements-for-viewing-reports"></a>Requisitos de script para exibição de relatórios

 Para usar o visualizador de relatórios, configure o seu navegador para executar scripts.

 Se os scripts não estiverem habilitados, você verá uma mensagem de erro semelhante à seguinte ao abrir um relatório:

- **Seu navegador não oferece suporte para scripts ou foi configurado para não permitir que sejam executados. Clique aqui para exibir este relatório sem scripts**.

 Se você optar por exibir o relatório sem o suporte de scripts, o relatório será renderizado em HTML sem os recursos de visualizador de relatório, como a barra de ferramentas de relatório e o mapa do documento.

> [!NOTE]
> A barra de ferramentas de relatório faz parte do componente Visualizador de HTML. Por padrão, a barra de ferramentas aparece na parte superior de todos os relatórios que são renderizados em uma janela de navegador. O visualizador de relatórios fornece recursos que incluem a habilidade de pesquisar informações no relatório, rolar até uma página específica e ajustar o tamanho da página para visualização. Para obter mais informações sobre a barra de ferramentas de relatório ou o Visualizador de HTML, consulte [HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md).

## <a name="browser-support-for-reportviewer-web-server-controls-in-visual-studio"></a>Suporte ao navegador em controles de servidor Web do ReportViewer no Visual Studio

 O controle ReportViewer de servidor Web é usado para inserir a funcionalidade de relatório em um aplicativo Web ASP.NET. Os controles estão incluídos no Visual Studio e dão suporte a navegadores e versões de navegador diferentes dos outros componentes descritos neste tópico. O tipo de navegador usado para exibir o aplicativo determina o tipo de funcionalidade de ReportViewer que você pode fornecer em seu aplicativo. Use a tabela fornecida neste tópico para determinar qual dos navegadores com suporte está sujeito a restrições de funcionalidade de relatório e as plataformas com suporte.  

 Use um navegador que tem suporte de script habilitado. Se o navegador não puder executar scripts, você não poderá exibir o relatório.

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 ou 11
- Google Chrome (+)
- Mozilla Firefox (+)

 **(+)** A versão lançada mais recente

## <a name="power-view-browser-support"></a>Suporte ao navegador no Power View

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Internet Explorer 10 ou 11
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)

 **(+)** A versão lançada mais recente

 Para saber mais sobre o suporte a navegadores do SharePoint 2016, confira [Planejar suporte ao navegador no SharePoint 2013](https://technet.microsoft.com//library/cc263526\(v=office.16\).aspx).

## <a name="next-steps"></a>Próximas etapas

[Localizar e exibir relatórios no Portal da Web](report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
[Ferramentas do Reporting Services](../reporting-services/tools/reporting-services-tools.md)  
[Portal da Web (Modo Nativo do SSRS)](https://msdn.microsoft.com/7349e626-6ed5-4d21-b05f-cf042ad9ad70)  
[HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)  
[Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)

