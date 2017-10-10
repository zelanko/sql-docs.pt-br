---
title: "Modo local vs modo conectado relatórios no Visualizador de relatórios | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 5f8342550dc105fb6d3544e1d8bd65fcd660ff64
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer"></a>Modo local vs modo conectado relatórios no Visualizador de relatórios

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Os relatórios podem ser configurados para serem executados no *modo local* ou no *modo conectado*, que aproveita um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Em vez disso, você pode usar o Visualizador de Relatórios para renderizar relatórios diretamente do SharePoint quando a extensão de dados der suporte a relatório no modo local. Essa abordagem é chamada de *modo local*. Em versões anteriores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o farm do SharePoint precisava estar conectado a um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado no modo do SharePoint para que o controle do Visualizador de Relatórios pudesse renderizar relatórios. Essa abordagem é chamada *modo remoto* ou *modo conectado*.  

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

 No *modo local* , não há nenhum servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você deve instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint, mas nenhum servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é necessário. Com o modo local, os usuários podem exibir relatórios, mas não terão acesso aos recursos do lado do servidor, como assinaturas e alertas de dados.  

## <a name="local-mode-vs-connected-mode-and-supported-extensions"></a>Modo local vs modo conectado e extensões com suporte

 **Modo local:** quando você tem uma extensão de dados compatível com o modo local, o Visualizador de Relatórios renderiza diretamente os relatórios do SharePoint. No *modo local* , não há nenhum servidor de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você deve instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint, mas nenhum servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é necessário. Com o modo local, os usuários podem exibir relatórios, mas **não** têm acesso aos recursos do lado do servidor, como assinaturas e alertas de dados.  
  
 **Modo conectado**, também chamado de *modo remoto* requer um servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint, conectado ao farm do SharePoint para que o controle do Visualizador de Relatórios possa renderizar relatórios.  
  
 A seguir há uma lista de extensões de processamento de dados que dão suporte a relatório no modo local:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Extensão de relatório do Access 2010. Para obter mais informações sobre os Serviços do Access, consulte [Use Access Services with SQL Reporting Services: Installing SQL Server 2008 R2 Reporting Services Add-In (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=192686)(Usar Serviços do Access com o SQL Reporting Services: Instalando o Suplemento do SQL Server 2008 R2 Reporting Services (SharePoint Server 2010)).  
  
-   A extensão de dados de lista do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre a Extensão de dados de lista do SharePoint, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
 Também podem ser desenvolvidas extensões de processamento de dados personalizadas para dar suporte ao modo local. Para obter mais informações, consulte [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md).  
  
 O modo local dá suporte à renderização de relatórios que têm uma fonte de dados interna ou uma fonte de dados compartilhada de um arquivo .rsds. No entanto, você não pode gerenciar o relatório nem sua fonte de dados associada. Se você tentar fazer isso, receberá um erro indicando que isso não tem suporte no modo local. O gerenciamento de fontes de dados no site do SharePoint tem suporte apenas no modo conectado.  
  
> [!NOTE]  
>  Assim como em versões anteriores, não é possível inserir nomes de usuários e senhas no arquivo .rsds.  
  
## <a name="configure-local-mode-and-access-services-with-sharepoint-2013"></a>Configurar serviços de acesso e modo locais com o SharePoint 2013

 Você pode configurar seu farm do SharePoint 2013 para dar suporte a bancos de dados da Web existentes do Access 2010 e o modo local de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Instalação e configuração dos Serviços do Access 2010 para bancos de dados da Web no SharePoint Server 2013](http://technet.microsoft.com/library/ee748653\(office.15\).aspx).  
  
 Não é possível criar novos bancos de dados da Web do Access para SharePoint 2013. O Access 2013 usa um novo tipo de banco de dados, o *aplicativo Web do Access* , criado no Access e, então, usa e compartilha com outros usuários como um aplicativo do SharePoint em um navegador da Web.  
  
 Para obter mais informações, consulte o seguinte.  
  
-   [Novidades do Access 2013](http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx).  
  
-   [Tarefas básicas para um aplicativo do Access](http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500).  
  
## <a name="configure-local-mode-reporting-with-sharepoint-2010"></a>Configurar o modo local reporting com o SharePoint 2010

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

 [Fontes de dados suportadas pelo Reporting Services](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
