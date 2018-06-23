---
title: Instalar recursos de BI do SQL Server com o SharePoint (PowerPivot e Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 25c8c6d8c5d83ba3661d30ed85f560d0aa18a54d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009488"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>Instalar recursos do SQL Server BI para o SharePoint (PowerPivot e Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode ser integrado a um farm do Microsoft SharePoint para habilitar os recursos de Business Intelligence (BI) no SharePoint. Os recursos incluem [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é usado para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] acesso a dados em um farm do SharePoint. O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é o mecanismo de dados para pastas de trabalho criadas no [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel e acessadas de uma biblioteca do SharePoint. Depois de salvar um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho no SharePoint, você pode usá-lo como uma fonte de dados para [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] relatórios.  
  
 Algumas das etapas da instalação e da configuração necessárias para o SharePoint 2010 são diferentes das etapas necessárias para o SharePoint 2013. Alguns dos tópicos desta seção se aplicam a ambas as versões do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 ![Observação](../../../2014/reporting-services/media/rs-fyinote.png "Observação") para obter as notas de versão atual, consulte [notas de versão do SQL server 2014](http://go.microsoft.com/fwlink/?LinkID=296445).  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
-   [Cenários de BI do SQL Server e SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [Visão geral da instalação](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>Nesta seção  
 Além das informações neste tópico, os seguintes tópicos relacionados estão nesta seção de conteúdo.  
  
 [Topologias de implantação para recursos de BI do SQL Server no SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [Listas de verificação para instalar recursos com SharePoint](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Instalação do modo do SharePoint do Reporting Services &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [Instalação do PowerPivot para SharePoint 2013](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a> Cenários de BI do SQL Server e SharePoint 2013  
 Essa seção resume os níveis diferentes de recursos de BI que você pode escolher instalar e configurar.  
  
 Os Serviços do Excel no SharePoint 2013 incluem a funcionalidade de modelo de dados para habilitar a interação com uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no navegador. Para a funcionalidade de modelo de dados básico não é necessário implantar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] suplemento 2013 no farm. Você só precisará instalar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint e registrar o servidor nas configurações do **Modelo de Dados** dos Serviços do Excel.  
  
 Implantando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 em permite mais funcionalidades e recursos no seu farm do SharePoint. Os recursos adicionais incluem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] galeria, agendamento de atualização de dados e o painel de gerenciamento do PowerPivot. Consulte a tabela para obter informações adicionais.  
  
||Nível|Recursos|Instalar ou configurar|  
|-|-----------|--------------|--------------------------|  
|1|Apenas SharePoint|Recursos nativos dos Serviços do Excel|Os Serviços do Excel e outros serviços incluídos com o SharePoint Server 2013.|  
|**2**|O SharePoint com Analysis Services no modo do SharePoint|Pastas de trabalho PowerPivot interativas no navegador|Instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint.<br /><br /> Registrar o servidor do Analysis Services nos Serviços do Excel.|  
|**3**|O SharePoint com Reporting Services no modo do SharePoint|Power View|Instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.<br /><br /> Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento **(rsSharePoint.msi)** para SharePoint. Para obter mais informações, consulte [instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|  
|**4**|Todos os recursos do PowerPivot|Acesso a pastas de trabalho como uma fonte de dados fora do farm.<br /><br /> Agendar atualização de dados.<br /><br /> Galeria PowerPivot.<br /><br /> Painel de Gerenciamento.<br /><br /> Tipo de conteúdo do arquivo de vínculo do BISM.|Implantar o PowerPivot para SharePoint 2013 em **(spPowerPivot.msi)**. Para obter mais informações, consulte o seguinte:<br /><br /> [Instalar ou desinstalar o PowerPivot para SharePoint suplemento &#40;do SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)<br /><br /> Para obter informações sobre como baixar o **spPowerPivot.msi**, consulte [Baixe o SQL Server 2014 PowerPivot para SharePoint](http://go.microsoft.com/fwlink/?LinkID=296473).|  
  
 Para obter informações adicionais sobre como habilitar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recursos, consulte [o SQL Server BI esclarecedora história para SharePoint 2013](http://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) (http://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx).  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a> Visão geral da instalação  
 Se você quiser usar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], execute o Assistente de instalação do SQL Server duas vezes. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são escolhas separadas no **função de instalação** página do Assistente de instalação do SQL Server.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] oferece suporte ao SharePoint 2010 e SharePoint 2013; No entanto, um processo de instalação e arquitetura diferente é usado dependendo da versão do SharePoint.  
  
 Veja a seguir um resumo das etapas de instalação para implantar recursos de BI do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um único servidor:  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 Para **SharePoint 2013**, o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instalação pode ser executada em um servidor que não tem um produto SharePoint instalado. O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] arquitetura usada para SharePoint 2013, executa **fora** o farm do SharePoint e pode ser instalado em um servidor que também contém uma instalação do SharePoint ou pode ser instalado um servidor que não contém um Instalação do SharePoint.  
  
1.  Instale o SharePoint Server 2013 e habilite Serviços do Excel.  
  
2.  Instale o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint, e conceda direitos de administrador de servidor às contas do farm e de serviços do SharePoint no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Para ambas as versões do SharePoint, o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] processo de instalação inicia, selecionando a configuração da função do **SQL Server PowerPivot para SharePoint** no Assistente de instalação do SQL Server ou use um prompt de comando do SQL Server instalação.  
  
     ![Função de instalação](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "função de instalação")  
  
3.  Para SharePoint 2013, você pode estender o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recursos e a experiência. Baixe e execute **spPowerPivot.msi** para adicionar suporte de processamento, colaboração e gerenciamento de atualização de dados do servidor para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho. Para obter mais informações, consulte [Microsoft SQL Server 2014 PowerPivot para Microsoft® SharePoint](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
     Execute o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] o pacote de instalação 2013 **spPowerPivot.msi** em cada servidor no farm do SharePoint para garantir que a versão correta dos dados provedores são instalados.  
  
4.  Para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013, use **PowerPivot para SharePoint 2013** ferramenta.  
  
     O Assistente de instalação do SQL Server instala duas [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ferramentas de configurações. Uma das ferramentas de configuração dá suporte ao SharePoint 2013 e a outra ferramenta dá suporte ao SharePoint 2010.  
  
     ![duas ferramentas de configuração do Power Pivot](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "two powerpivot configuratoin tools")  
  
5.  Configure os Serviços do Excel no SharePoint Server 2013 para usar a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte a seção "Configurar a integração básica do Analysis Services SharePoint" em [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)e [modelo de dados de gerenciar os serviços do Excel (SharePoint Server de configurações 2013)](http://technet.microsoft.com/library/jj219780.aspx) (http://technet.microsoft.com/library/jj219780.aspx).  
  
6.  Para obter mais informações, consulte [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 Para o SharePoint 2010, é necessário que a instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint seja executada em um servidor que já tenha o SharePoint 2010 instalado ou em um em que ele será instalado. O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] arquitetura para SharePoint 2010 é executado **dentro de** o farm e exige o SharePoint no servidor que [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint está instalado.  
  
1.  Instale o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint, e conceda direitos de administrador de servidor às contas do farm e de serviços do SharePoint no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Uma implantação do SharePoint 2010 não dá suporte a spPowerPivot.msi, e o .msi **não** é obrigatório com o SharePoint 2010.  
  
     Para ambas as versões do SharePoint, o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] processo de instalação inicia, selecionando a configuração da função do **SQL Server PowerPivot para SharePoint** no Assistente de instalação do SQL Server ou use um prompt de comando do SQL Server instalação.  
  
2.  O Assistente de instalação do SQL Server instala duas [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ferramentas de configurações. Uma das ferramentas de configuração dá suporte ao SharePoint 2013 e a outra ferramenta dá suporte ao SharePoint 2010.  
  
     Para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010, use o **ferramenta de configuração do PowerPivot** .  
  
3.  Para obter mais informações, consulte [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  para o SharePoint 2010 e 2013  
  
1.  A instalação para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint modo está inalterado desde a versão anterior.  
  
     O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] etapas de instalação para o SharePoint 2010 e SharePoint 2013 são muito semelhantes. Observações importantes sobre as versões do SharePoint:  
  
    -   Consulte as combinações com suporte do seguinte:  
  
        -   A versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
        -   O suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint.  
  
        -   A versão do produto do SharePoint.  
  
         [Combinações do SharePoint e Reporting Services Server e o suplemento com suporte &#40;do SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint 2010 exige o SharePoint 2010 Service Pack 2 (SP2).  
  
    1.  Instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. [Instalação do modo do SharePoint do Reporting Services &#40;do SharePoint 2010 e SharePoint 2013&#41; ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) e [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
    2.  Instale o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint (rsSharePoint.msi). Consulte [instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Para a versão atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para SharePoint, consulte [onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
    3.  Configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço do SharePoint e pelo menos um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo de serviço. Para obter mais informações, consulte a seção "Criar um relatório de serviços de aplicativo de serviço" em [instalar o Reporting Services SharePoint Mode para SharePoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).  
  
##  <a name="bkm_database_attach"></a> Visão geral da anexação do banco de dados de atualização e o SharePoint 2013  
 O SharePoint 2013 não oferece suporte a atualização in-loco. No entanto, **atualização da anexação do banco de dados tem suporte**.  
  
 Se você tiver uma instalação existente do PowerPivot integrada com o SharePoint 2010, não poderá atualizar o servidor do SharePoint in-loco.  No entanto, você pode concluir as etapas a seguir como parte de uma atualização da anexação do banco de dados do SharePoint:  
  
1.  Instalar um novo farm do SharePoint Server 2013.  
  
2.  Conclua uma atualização da anexação do banco de dados do SharePoint e migre seus bancos de dados de conteúdo relacionados do PowerPivot para o farm do SharePoint 2013.  
  
3.  Instalar uma instância do SQL Server Analysis Services no modo do SharePoint e conceder a contas de serviços e o farm do SharePoint, os direitos de administrador de servidor em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
4.  Instalar o pacote de instalação do PowerPivot para SharePoint 2013 **spPowerPivot.msi** em cada farm do SharePoint Server.  
  
5.  Na Administração Central do SharePoint 2013, configure os Serviços do Excel para usar o servidor do Analysis Services que está sendo executado modo do SharePoint criado na etapa 3.  
  
     Para migrar agendas de atualização, configure o aplicativo de serviço PowerPivot.  
  
> [!NOTE]  
>  Para obter mais informações sobre a atualização da anexação do banco de dados do PowerPivot e do SharePoint, consulte o seguinte:  
  
-   [Migrar o PowerPivot para o SharePoint 2013](../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)  
  
-   [Visão geral do processo de atualização para o SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpar preparações antes de uma atualização do SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Atualizar bancos de dados do SharePoint 2010 para o SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>Consulte também  
 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Combinações do SharePoint e Reporting Services Server e o suplemento com suporte &#40;do SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  