---
title: Planejando o suporte ao navegador do Reporting Services e do Power View (Reporting Services 2014)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: cd3a3e268e09e882b4e38eee6a620843fcc21a23
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241198"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>Planejando o suporte ao navegador do Reporting Services e do Power View (Reporting Services 2014)
  No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], você usa um navegador da Web para exibir relatórios e executar o Gerenciador de Relatórios. Nem todos os navegadores dão suporte à funcionalidade de relatório. Este tópico descreve o suporte e os requisitos para os recursos de gerenciamento do Gerenciador de Relatórios, exibir relatórios, os controles do Visualizador de Relatórios no Visual Studio. O tópico também resume a disponibilidade de recursos para os navegadores com suporte, os requisitos de autenticação e os requisitos de script.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Modo do SharePoint | [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo nativo  
  
 **Neste tópico:**  
  
- [Cenários do navegador do Power View](#bkmk_powerview)  
  
- [Requisitos de navegador para o Gerenciador de Relatórios (modo nativo)](#bkmk_reportmanager)  
  
- [Requisitos de navegador para exibir relatórios](#bkmk_reportviewer)  
  
- [Requisitos de autenticação](#bkmk_authentication)  
  
- [Suporte de navegador para controles de servidor Web ReportViewer no Visual Studio](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a>Cenários de navegador Power View

 A lista de navegadores com suporte e versões de navegador à qual o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] oferece suporte depende do tipo de documento aberto. As pastas de trabalho do Excel 2013 e os arquivos "**. rdlx**" utilizam componentes diferentes.  
  
|Tipo de documento|Ambiente|Suporte ao navegador|  
|-------------------|-----------------|---------------------|  
|Relatório do Power View (.RDLX)|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] modo integrado do SharePoint e no aplicativo Web Power View.|Consulte [Power View no SharePoint Server e no modo integrado do SharePoint do Reporting Services](#bkmk_powerview_on_SSRS).|  
|Pasta de trabalho do Excel 2013 com planilhas do Power View|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] em serviços do Excel.<br /><br /> **SharePoint Online (Office 365):** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] no Excel Web App.|Consulte [Power View nos Serviços do Excel ou Excel Web App no SharePoint Online](#bkmk_powerview_on_ExcelServices).|  
  
###  <a name="bkmk_powerview_on_SSRS"></a>Power View no SharePoint Server e no modo integrado do Reporting Services SharePoint  
 A tabela a seguir resume as versões de navegador com suporte para [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] quando um usuário abre um relatório do Power View (.RDLX) em um farm do SharePoint que tenha um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e o suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para SharePoint instalados e configurados.  
  
- A tabela se aplica ao SharePoint 2010 e ao SharePoint 2013.  
  
- Para obter mais informações sobre o suporte ao navegador do SharePoint 2013, consulte [planejar o suporte do navegador no SharePoint 2013](https://technet.microsoft.com//library/cc263526\(office.15\).aspx) (https://technet.microsoft.com/library/cc263526(office.15).aspx).  
  
- Para obter mais informações sobre o suporte ao navegador do SharePoint 2010, consulte [planejar o suporte do navegador (SharePoint Server 2010)](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) (https://technet.microsoft.com/library/cc263526(office.14).aspx).  
  
|**Navegador**|**Windows 8 e 8,1**|**Windows 7**|**Windows Server 2012 e 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10,6-10,9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (para a área de trabalho)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Internet Explorer 10 (para a área de trabalho)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Internet Explorer 9**|Sem suporte|32 bits, 64 bits|Sem suporte|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|  
|**Internet Explorer 8**|Sem suporte|32 bits, 64 bits|Sem suporte|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|  
|**Mozilla Firefox (última versão lançada publicamente)**|32 bits|32 bits|32 bits|32 bits|32 bits|Sem suporte|  
|**Apple Safari (última versão lançada publicamente)**|Sem suporte|Sem suporte|Sem suporte|Sem suporte|Sem suporte|32 bits, 64 bits|  
  
> [!NOTE]  
> "32 bits" refere-se ao navegador, e não ao sistema operacional. Você pode usar o Internet Explorer 9 de 32 bits no Windows 7 de 64 bits, por exemplo.  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>O recurso de navegação InPrivate no Internet Explorer

 O [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] não dá suporte ao recurso de navegação InPrivate no Internet Explorer 8 e no Internet Explorer 9 da [!INCLUDE[msCoName](../includes/msconame-md.md)]. Para obter mais informações sobre a navegação InPrivate, consulte [o que é Navegação InPrivate?](https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a>Power View nos serviços do Excel ou no aplicativo Web do Excel no SharePoint Online

 A tabela a seguir resume as versões de navegador com suporte para [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] quando um usuário abre uma pasta de trabalho do Excel 2013 com planilhas do Power View em um SharePoint Server que está executando os Serviços do Excel:  
  
-   Para obter mais informações sobre o suporte ao navegador do SharePoint 2013, consulte [planejar o suporte do navegador no SharePoint 2013](https://technet.microsoft.com/library/cc263526\(office.15\).aspx) (https://technet.microsoft.com/library/cc263526(office.15).aspx).  
  
|**Navegador**|**Windows 8 e 8,1**|**Windows 7**|**Windows Server 2012 e 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10,6-10,9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (para a área de trabalho)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Internet Explorer 10 (para a área de trabalho)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Internet Explorer 9**|Sem suporte|32 bits, 64 bits|Sem suporte|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|  
|**Internet Explorer 8**|Sem suporte|32 bits, 64 bits|Sem suporte|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|  
|**Mozilla Firefox (última versão lançada publicamente)**|32 bits|32 bits|32 bits|32 bits|32 bits|32 bits, 64 bits|  
|**Apple Safari (última versão lançada publicamente)**|Sem suporte|Sem suporte|Sem suporte|Sem suporte|Sem suporte|32 bits, 64 bits|  
|**Google Chrome (última versão lançada publicamente)**|32 bits **(\*)** por tempo limitado|32 bits **(\*)** por tempo limitado|32 bits **(\*)** por tempo limitado|32 bits **(\*)** por tempo limitado|32 bits **(\*)** por tempo limitado|Sem suporte|  
  
 **(\*)** O Chrome irá parar de oferecer suporte à API de plug-in do Netscape (NPAPI), usada pelo Silverlight. O Power View depende do Silverlight.  Para saber mais, confira [A contagem regressiva do NPAPI](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html).  
  
##  <a name="bkmk_reportmanager"></a>Requisitos de navegador de Report Manager (modo nativo)

 A seguir é apresentada a lista atual de navegadores com suporte que você pode usar para executar o Gerenciador de Relatórios do modo nativo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para gerenciar relatórios e o servidor de relatório.  
  
|Navegador|  
|-------------|  
|O Internet Explorer 7 ou mais novo e scripts devem ser habilitados.|  
|Mozilla FireFox (última versão lançada publicamente)|  
|Apple Safari (última versão lançada publicamente)|  
|Google Chrome (última versão lançada publicamente)|  
  
##  <a name="bkmk_reportviewer"></a>Requisitos de navegador para exibir relatórios

 Veja a seguir uma lista atual de navegadores e recursos com suporte com o visualizador de relatório. O visualizador de relatórios oferece suporte à visualização de relatórios do gerenciador de relatórios do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e de bibliotecas do SharePoint.  
  
|**Navegador**|**Windows 8 e 8,1**|**Windows 7**|**Windows Server 2012 e 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10,6-10,9**|**iOS 6 -7 para iPad**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 (para a área de trabalho)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|Sem suporte|Sem suporte|  
|**Internet Explorer 10 (para a área de trabalho)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|Sem suporte|Sem suporte|  
|**Internet Explorer 9**|Sem suporte|32 bits, 64 bits|Sem suporte|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Internet Explorer 8**|Sem suporte|32 bits, 64 bits|Sem suporte|32 bits, 64 bits|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Internet Explorer 7**|Sem suporte|Sem suporte|Sem suporte|Sem suporte|32 bits, 64 bits|Sem suporte|Sem suporte|  
|**Mozilla Firefox (última versão lançada publicamente)**|32 bits|32 bits|32 bits|32 bits|32 bits|Sem suporte|Sem suporte|  
|**Apple Safari (última versão lançada publicamente)**|Sem suporte|Sem suporte|Sem suporte|Sem suporte|Sem suporte|32 bits, 64 bits|Com suporte com recursos limitados <sup>(1)</sup>|  
|**Google Chrome (última versão lançada publicamente)**|32 bits|32 bits|32 bits|32 bits|32 bits|Sem suporte|Sem suporte|  
  
 **<sup>(1)</sup>** há suporte para os seguintes recursos:  
  
- Exportação para formatos PDF e TIFF.  
  
- Exibir interativamente relatórios no Safari da Apple em dispositivos iOS. O suporte a recursos inclui expandir/recolher, o painel de parâmetro e a classificação interativa.  
  
- Para obter mais informações, consulte [View Reporting Services Reports on Microsoft Surface Devices and Apple Ios Devices](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md).  
  
 **Observação** Se você estiver acessando um servidor de relatório de um computador Macintosh, recomendamos que você use o Safari. Se você estiver usando um produto do SharePoint integrado ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte planejar o suporte do [navegador (Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkId=183583).  
  
### <a name="url-access-for-viewing-reports"></a>Acesso URL para exibir relatórios

 Para exibir relatórios diretamente, em vez de exibi-los por meio do Gerenciador de Relatórios, você pode usar Acesso à URL para vincular ao relatório ao visualizador de relatórios. O acesso à URL dá suporte a uma variedade de navegadores.  
  
 Para obter mais informações sobre acesso URL, consulte o seguinte tópico:  
  
- [Referência de parâmetro de acesso à URL](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a>Requisitos de autenticação

 Os navegadores dão suporte a esquemas de autenticação específicos que devem ser tratados pelo servidor de relatório para que a solicitação do cliente seja bem-sucedida. A tabela a seguir identifica os tipos de autenticação padrão com suporte por cada navegador que é executado em um sistema operacional Windows.  
  
|**Tipo de navegador**|**Suportar**|**Padrão do navegador**|**Padrão do servidor**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|Negotiated, Kerberos, NTLM, Basic|Negociar|Sim. As configurações de autenticação padrão funcionam com o Internet Explorer.|  
|**Janelas**|NTLM, Basic|NTLM|Sim. As configurações de autenticação padrão funcionam com o Firefox.|  
|**Safari**|Básico|Básico|Sim. As configurações de autenticação padrão funcionam com o Safari.|  
|**Monocromático**|Negotiated, NTLM, Basic|Negociado|Sim. As configurações de autenticação padrão funcionam com o Chrome.|  
  
### <a name="script-requirements"></a>Requisitos de script

 Para usar o visualizador de relatórios, configure o seu navegador para executar scripts.  
  
 Se os scripts não estiverem habilitados, você verá uma mensagem de erro semelhante à seguinte ao abrir um relatório:  
  
- **Seu navegador não oferece suporte a scripts ou foi configurado para não permitir a execução de scripts. Clique aqui para exibir este relatório sem scripts**.  
  
 Se você optar por exibir o relatório sem o suporte de scripts, o relatório será renderizado em HTML sem os recursos de visualizador de relatório, como a barra de ferramentas de relatório e o mapa do documento.  
  
> [!NOTE]  
> A barra de ferramentas de relatório faz parte do componente Visualizador de HTML. Por padrão, a barra de ferramentas aparece na parte superior de todos os relatórios que são renderizados em uma janela de navegador. O visualizador de relatórios fornece recursos que incluem a habilidade de pesquisar informações no relatório, rolar até uma página específica e ajustar o tamanho da página para visualização. Para obter mais informações sobre a barra de ferramentas de relatório ou o Visualizador de HTML, consulte [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md).  
  
##  <a name="bkmk_controls"></a>Suporte de navegador para controles de servidor Web ReportViewer no Visual Studio

 O controle ReportViewer de servidor Web é usado para inserir a funcionalidade de relatório em um aplicativo Web ASP.NET. Os controles estão incluídos no Visual Studio e dão suporte a navegadores e versões de navegador diferentes dos outros componentes descritos neste tópico. O tipo de navegador usado para exibir o aplicativo determina o tipo de funcionalidade de ReportViewer que você pode fornecer em seu aplicativo. Use a tabela fornecida neste tópico para determinar qual dos navegadores com suporte está sujeito a restrições de funcionalidade de relatório e as plataformas com suporte.  
  
 Devido a diferenças nos mecanismos de renderização dos navegadores com suporte, alguns recursos de relatório podem ser exibidos diferentemente em diferentes navegadores.  Por exemplo, rotação do texto.  
  
### <a name="scripting-requirements"></a>Requisitos de script

 Use um navegador que tem suporte de script habilitado. Se o navegador não puder executar scripts, você não poderá exibir o relatório.  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>Requisitos de navegador para exibir relatórios com os controles ReportViewer de servidor Web

 O suporte para recursos de relatório interativos varia de acordo com o tipo de navegador. A matriz de suporte a seguir mostra quais tipos de navegador têm suporte em quais plataformas, sujeito a restrições observadas na coluna de Notas.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**Navegador**|**Windows 8** e **Windows 8.1**|**Windows 7**|**Windows Server 2012** e **2012 R2**|**Windows Server 2008** e **2008 R2**|**Windows Server 2003**|**Mac OS X 10,6-10,9**|**Registra**|  
|**Internet Explorer 11 (para desktops**|Sim|Sim|Sim|Sem suporte|Sem suporte|Sem suporte|O Internet Explorer dá suporte a um conjunto completo de recursos do ReportViewer.|  
|**Internet Explorer 10 (para a área de trabalho)**|Sim|Sim|Sim|Sem suporte|Sem suporte|Sem suporte|O Internet Explorer dá suporte a um conjunto completo de recursos do ReportViewer.|  
|**Internet Explorer 9**|Sem suporte|Sim|Sem suporte|Sim|Sim|Sim|O Internet Explorer dá suporte a um conjunto completo de recursos do ReportViewer.|  
|**Internet Explorer 8.0**|Sem suporte|Sim|Sem suporte|Sim|Sim<sup>1</sup>|Sem suporte|O Internet Explorer dá suporte a um conjunto completo de recursos do ReportViewer. <sup>uma</sup>|  
|**Internet Explorer 7.0**|Sem suporte|Sim|Sem suporte|Sim|Sim<sup>1</sup>|Sem suporte|O Internet Explorer dá suporte a um conjunto completo de recursos do ReportViewer. <sup>uma</sup>|  
|**Firefox (última versão lançada publicamente)**|Sim|Sim|Sim|Sim|Sim|Sem suporte|Não há suporte para imprimir ou ampliar.|  
|**Safari (última versão lançada publicamente)**|Sem suporte|Sem suporte|Sem suporte|Sem suporte|Sem suporte|Sim|Não há suporte para imprimir ou ampliar.<br /><br /> O controle Calendário que é usado para selecionar datas em um relatório com parâmetros é desabilitado neste navegador. Os usuários devem digitar manualmente as datas que querem usar na área de prompt de parâmetro.|  
|**Chrome (última versão lançada publicamente)**|Sim|Sim|Sim|Sim|Sim|Sem suporte|Não há suporte para imprimir ou ampliar.|  
  
 <sup>1</sup> No modo de padrões, o Internet Explorer 7,0 e 8,0 não exibem linhas inclinadas em relatórios. Se você usar linhas inclinadas em seus relatórios, defina sua página ASP.NET para ser executada no modo de Quirks no Internet Explorer. Para fazer isso, encontre o \<! DOCTYPE> marca em sua página do ASP.NET. Ou, se usar uma página mestre, poderá localizar a marca no arquivo .master. Essa marca é semelhante ao seguinte:  
  
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```
  
 Substitua o \<! DOCTYPE> marca com a seguinte marca:  
  
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```
  
 Para obter mais informações sobre modos de compatibilidade no Internet Explorer, consulte Definindo ahttps://go.microsoft.com/fwlink/?LinkId=180380)compatibilidade de [documentos](https://go.microsoft.com/fwlink/?LinkId=180380) (.  
  
 Para obter mais informações sobre como usar os controles ReportViewer, consulte [implantando relatórios e controles ReportViewer](https://msdn.microsoft.com/library/ms251723.aspx) (https://msdn.microsoft.com/library/ms251723.aspx).  
  
## <a name="next-steps"></a>Próximas etapas

 [Ferramentas de Reporting Services](tools/reporting-services-tools.md) [Report Manager &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) [Visualizador de HTML e a barra de ferramentas de relatório](html-viewer-and-the-report-toolbar.md)
