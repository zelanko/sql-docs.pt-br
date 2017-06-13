---
title: "Relatórios em Modo Local vs. Modo conectado no Visualizador de relatórios | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a230a9bb-6046-401f-b5e5-53ff6edf2264
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ca6519365ae81c5a7875825fb976c163dbb588f3
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer"></a>Relatórios em Modo Local vs. Modo Conectado no Visualizador de Relatórios
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Os relatórios podem ser configurados para serem executados no *modo local* ou no *modo conectado*, que aproveita um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Em vez disso, você pode usar o Visualizador de Relatórios para renderizar relatórios diretamente do SharePoint quando a extensão de dados der suporte a relatório no modo local. Essa abordagem é chamada de *modo local*. Em versões anteriores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o farm do SharePoint precisava estar conectado a um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado no modo do SharePoint para que o controle do Visualizador de Relatórios pudesse renderizar relatórios. Essa abordagem é chamada *modo remoto* ou *modo conectado*.  
  
 No *modo local* , não há nenhum servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você deve instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint, mas nenhum servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é necessário. Com o modo local, os usuários podem exibir relatórios, mas não terão acesso aos recursos do lado do servidor, como assinaturas e alertas de dados.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode|  
  
 **Neste tópico:**  
  
-   [Modo local vs modo conectado e extensões com suporte](#bkmk_local_vs_connected)  
  
-   [Configurar o modo Local e Serviços do Access com o SharePoint 2013](#bkmk_local_mode_sharepoint2013)  
  
-   [Configurar relatórios no modo Local com o SharePoint 2010](#bkmk_local_mode_sharepoint2010)  
  
##  <a name="bkmk_local_vs_connected"></a> Modo local vs modo conectado e extensões com suporte  
 **Modo local:** quando você tem uma extensão de dados compatível com o modo local, o Visualizador de Relatórios renderiza diretamente os relatórios do SharePoint. No *modo local* , não há nenhum servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você deve instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint, mas nenhum servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é necessário. Com o modo local, os usuários podem exibir relatórios, mas **não** têm acesso aos recursos do lado do servidor, como assinaturas e alertas de dados.  
  
 **Modo conectado**, também chamado de *modo remoto* requer um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint, conectado ao farm do SharePoint para que o controle do Visualizador de Relatórios possa renderizar relatórios.  
  
 A seguir há uma lista de extensões de processamento de dados que dão suporte a relatório no modo local:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Extensão de relatório do Access 2010. Para obter mais informações sobre os Serviços do Access, consulte [Use Access Services with SQL Reporting Services: Installing SQL Server 2008 R2 Reporting Services Add-In (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=192686)(Usar Serviços do Access com o SQL Reporting Services: Instalando o Suplemento do SQL Server 2008 R2 Reporting Services (SharePoint Server 2010)).  
  
-   A extensão de dados de lista do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre a Extensão de dados de lista do SharePoint, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
 Também podem ser desenvolvidas extensões de processamento de dados personalizadas para dar suporte ao modo local. Para obter mais informações, consulte [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md).  
  
 O modo local dá suporte à renderização de relatórios que têm uma fonte de dados interna ou uma fonte de dados compartilhada de um arquivo .rsds. No entanto, você não pode gerenciar o relatório nem sua fonte de dados associada. Se você tentar fazer isso, receberá um erro indicando que isso não tem suporte no modo local. O gerenciamento de fontes de dados no site do SharePoint tem suporte apenas no modo conectado.  
  
> [!NOTE]  
>  Assim como em versões anteriores, não é possível inserir nomes de usuários e senhas no arquivo .rsds.  
  
##  <a name="bkmk_local_mode_sharepoint2013"></a> Configurar o modo Local e Serviços do Access com o SharePoint 2013  
 Você pode configurar seu farm do SharePoint 2013 para dar suporte a bancos de dados da Web existentes do Access 2010 e o modo local de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Instalação e configuração dos Serviços do Access 2010 para bancos de dados da Web no SharePoint Server 2013](http://technet.microsoft.com/library/ee748653\(office.15\).aspx).  
  
 Não é possível criar novos bancos de dados da Web do Access para SharePoint 2013. O Access 2013 usa um novo tipo de banco de dados, o *aplicativo Web do Access* , criado no Access e, então, usa e compartilha com outros usuários como um aplicativo do SharePoint em um navegador da Web.  
  
 Para obter mais informações, consulte o seguinte.  
  
-   [Novidades do Access 2013](http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx).  
  
-   [Tarefas básicas para um aplicativo do Access](http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500).  
  
##  <a name="bkmk_local_mode_sharepoint2010"></a> Configurar relatórios no modo Local com o SharePoint 2010  
 O modo local requer o estado de sessão ASP.NET. A instalação de serviços do Access habilitará esse estado. Também é possível habilitá-lo usando o PowerShell.  
  
1.  Abra o Shell de Gerenciamento do SharePoint 2010.  
  
2.  Digite o seguinte comando:  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  Quando solicitado, digite o nome do banco de dados.  
  
4.  Reinicie o IIS.  
  
 Para obter mais informações, consulte [Use Access Services with SQL Reporting Services: Installing SQL Server 2008 R2 Reporting Services Add-In (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=192686) (Usar Serviços do Access com o SQL Reporting Services: Instalando o Suplemento do SQL Server 2008 R2 Reporting Services (SharePoint Server 2010)) e [Enable-SPSessionStateService](http://technet.microsoft.com/library/ff607857\(v=office.15\).aspx).  
  
## <a name="connected-mode"></a>modo conectado  
 Para obter as informações mais recentes sobre o uso da extensão ADS com o modo conectado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte [Access Services Report in SharePoint Site shows error in data extension ‘ADS’](http://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx)(Relatório de Serviços do Access no site do SharePoint mostra erro na extensão de dados ‘ADS’).  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
