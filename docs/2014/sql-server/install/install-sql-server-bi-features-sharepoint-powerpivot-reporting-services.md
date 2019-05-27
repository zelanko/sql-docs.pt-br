---
title: Instalar recursos de BI do SQL Server com o SharePoint (PowerPivot e Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 436d90b75a5995ac8f455a52ebfffe662b1f9b7f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094459"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>Instalar recursos do SQL Server BI para o SharePoint (PowerPivot e Reporting Services)
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser integrados a um farm do Microsoft SharePoint para habilitar recursos de BI (Business Intelligence) no SharePoint. Os recursos incluem [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é usado para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] acesso a dados em um farm do SharePoint. O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é o mecanismo de dados para pastas de trabalho criadas no [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel e acessadas de uma biblioteca do SharePoint. Ao salvar uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no SharePoint, você poderá usá-la como uma fonte de dados para relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 Algumas das etapas da instalação e da configuração necessárias para o SharePoint 2010 são diferentes das etapas necessárias para o SharePoint 2013. Alguns dos tópicos desta seção se aplicam a ambas as versões do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 ![Observação](../../../2014/reporting-services/media/rs-fyinote.png "Observação") para as notas de versão atuais, consulte [notas de versão do SQL server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
-   [Cenários de BI do SQL Server e SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [Visão geral da instalação](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>Nesta seção  
 Além das informações neste tópico, os seguintes tópicos relacionados estão nesta seção de conteúdo.  
  
 [Topologias de implantação para recursos de BI do SQL Server no SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [Listas de verificação para instalar recursos com SharePoint](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Instalação do modo do SharePoint do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [Instalação do PowerPivot para SharePoint 2013](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a> Cenários de BI do SQL Server e SharePoint 2013  
 Essa seção resume os níveis diferentes de recursos de BI que você pode escolher instalar e configurar.  
  
 Os Serviços do Excel no SharePoint 2013 incluem a funcionalidade de modelo de dados para habilitar a interação com uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no navegador. Para obter a funcionalidade básica de modelo de dados, você não precisa implantar o suplemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 no farm. Você só precisará instalar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint e registrar o servidor nas configurações do **Modelo de Dados** dos Serviços do Excel.  
  
 A implantação do suplemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 habilita a funcionalidade e os recursos adicionais no farm do SharePoint. Os recursos adicionais incluem Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Atualização de Dados da Agenda e o Painel de Gerenciamento PowerPivot. Consulte a tabela para obter informações adicionais.  
  
||Nível|Recursos|Instalar ou configurar|  
|-|-----------|--------------|--------------------------|  
|1|Apenas SharePoint|Recursos nativos dos Serviços do Excel|Os Serviços do Excel e outros serviços incluídos com o SharePoint Server 2013.|  
|**2**|O SharePoint com Analysis Services no modo do SharePoint|Pastas de trabalho PowerPivot interativas no navegador|Instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint.<br /><br /> Registrar o servidor do Analysis Services nos Serviços do Excel.|  
|**3**|O SharePoint com Reporting Services no modo do SharePoint|Power View|Instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.<br /><br /> Instale [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento **(rssharepoint. msi)** para SharePoint. Para obter mais informações, consulte [instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|  
|**4**|Todos os recursos do PowerPivot|Acesso a pastas de trabalho como uma fonte de dados fora do farm.<br /><br /> Agendar atualização de dados.<br /><br /> Galeria PowerPivot.<br /><br /> Painel de Gerenciamento.<br /><br /> Tipo de conteúdo do arquivo de vínculo do BISM.|Implantar o PowerPivot para SharePoint 2013 na **(sppowerpivot. msi)**. Para obter mais informações, consulte o seguinte:<br /><br /> [Instalar ou desinstalar o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)<br /><br /> Para obter informações sobre como baixar o **spPowerPivot.msi**, consulte [Baixe o SQL Server 2014 PowerPivot para SharePoint](https://go.microsoft.com/fwlink/?LinkID=296473).|  
  
 Para obter mais informações sobre como habilitar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recursos, consulte [a história SQL Server BI Light-Up para SharePoint 2013](https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) (https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx).  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a> Visão geral da instalação  
 Se você quiser usar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], execute o assistente de instalação do SQL Server duas vezes. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são escolhas separadas na **função de instalação** página do Assistente de instalação do SQL Server.  
  
 O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dá suporte ao SharePoint 2010 e ao SharePoint 2013, mas uma arquitetura e um processo de instalação diferentes serão usados dependendo da versão do SharePoint.  
  
 Veja a seguir um resumo das etapas de instalação para implantar recursos de BI do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um único servidor:  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 Para o **SharePoint 2013**, a instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] pode ser executada em um servidor sem um produto SharePoint instalado. A arquitetura do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usada para SharePoint 2013, é executada **fora** do farm do SharePoint e pode ser instalada em um servidor que também contém uma instalação do SharePoint ou pode ser instalado um servidor que NÃO contenha uma instalação do SharePoint.  
  
1.  Instale o SharePoint Server 2013 e habilite Serviços do Excel.  
  
2.  Instale o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint, e conceda direitos de administrador de servidor às contas do farm e de serviços do SharePoint no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Para ambas as versões do SharePoint, o processo de instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é iniciado com a seleção da configuração da função do **SQL Server PowerPivot para SharePoint** no assistente de Instalação do SQL Server ou usar uma instalação de prompt de comando do SQL Server.  
  
     ![Função de instalação](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "função de instalação")  
  
3.  Para o SharePoint 2013, você pode estender os recursos e a experiência do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Baixe e execute o **spPowerPivot.msi** para adicionar processamento de atualização de dados no lado do servidor, colaboração e suporte a gerenciamento à pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações, consulte [Microsoft SQL Server 2014 PowerPivot para Microsoft® SharePoint](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
     Execute o pacote de instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 **spPowerPivot.msi** em cada servidor no farm do SharePoint para garantir que as versões corretas dos provedores de dados será instalada.  
  
4.  Para configurar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013, use a ferramenta de **Configuração do PowerPivot para SharePoint 2013** .  
  
     O assistente de instalação do SQL Server instala duas ferramentas de configurações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Uma das ferramentas de configuração dá suporte ao SharePoint 2013 e a outra ferramenta dá suporte ao SharePoint 2010.  
  
     ![duas ferramentas de configuração do Power Pivot](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "two powerpivot configuratoin tools")  
  
5.  Configure os Serviços do Excel no SharePoint Server 2013 para usar a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte a seção "Configurar a integração básica do Analysis Services SharePoint" em [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)e [configurações (SharePoint Server do modelo de dados de gerenciar os serviços do Excel 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx).  
  
6.  Para obter mais informações, consulte [PowerPivot for SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 Para o SharePoint 2010, é necessário que a instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint seja executada em um servidor que já tenha o SharePoint 2010 instalado ou em um em que ele será instalado. A arquitetura do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010 é executada **dentro** do farm e exige o SharePoint no servidor em que o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint está instalado.  
  
1.  Instale o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint, e conceda direitos de administrador de servidor às contas do farm e de serviços do SharePoint no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Uma implantação do SharePoint 2010 não dá suporte a spPowerPivot.msi, e o .msi **não** é obrigatório com o SharePoint 2010.  
  
     Para ambas as versões do SharePoint, o processo de instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é iniciado com a seleção da configuração da função do **SQL Server PowerPivot para SharePoint** no assistente de Instalação do SQL Server ou usar uma instalação de prompt de comando do SQL Server.  
  
2.  O assistente de instalação do SQL Server instala duas ferramentas de configurações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Uma das ferramentas de configuração dá suporte ao SharePoint 2013 e a outra ferramenta dá suporte ao SharePoint 2010.  
  
     Para configurar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010, use a **Ferramenta de Configuração do PowerPivot** .  
  
3.  Para obter mais informações, consulte [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  para SharePoint 2010 e 2013  
  
1.  A instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo de SharePoint não foi alterada em relação à versão anterior.  
  
     As etapas de instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o SharePoint 2010 e o SharePoint 2013 são muito semelhantes. Observações importantes sobre as versões do SharePoint:  
  
    -   Consulte as combinações com suporte do seguinte:  
  
        -   A versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
        -   O suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint.  
  
        -   A versão do produto do SharePoint.  
  
         [Combinações do SharePoint e do servidor e suplemento Reporting Services com suporte &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint 2010 exige o SharePoint 2010 Service Pack 2 (SP2).  
  
    1.  Instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. [Instalação do modo do SharePoint do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41; ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) e [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
    2.  Instale o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint (rsSharePoint.msi). Ver [instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Para a versão atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para SharePoint, consulte [onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
    3.  Configure o serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint e pelo menos um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte a seção "Criar um aplicativo Reporting Services Service" no [instalar o Reporting Services SharePoint Mode para SharePoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).  
  
##  <a name="bkm_database_attach"></a> Visão geral da anexação do banco de dados de atualização e o SharePoint 2013  
 O SharePoint 2013 não oferece suporte a atualização in-loco. No entanto, **atualização da anexação do banco de dados tem suporte**.  
  
 Se você tiver uma instalação existente do PowerPivot integrada com o SharePoint 2010, não poderá atualizar o servidor do SharePoint in-loco.  No entanto, você pode concluir as etapas a seguir como parte de uma atualização da anexação do banco de dados do SharePoint:  
  
1.  Instalar um novo farm do SharePoint Server 2013.  
  
2.  Conclua uma atualização da anexação do banco de dados do SharePoint e migre seus bancos de dados de conteúdo relacionados do PowerPivot para o farm do SharePoint 2013.  
  
3.  Instale uma instância do SQL Server Analysis Services no modo do SharePoint, e conceda direitos de administrador de servidor às contas do farm e de serviços do SharePoint no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
4.  Instalar o pacote de instalação do PowerPivot para SharePoint 2013 **spPowerPivot.msi** em cada farm do SharePoint Server.  
  
5.  Na Administração Central do SharePoint 2013, configure os Serviços do Excel para usar o servidor do Analysis Services que está sendo executado modo do SharePoint criado na etapa 3.  
  
     Para migrar agendas de atualização, configure o aplicativo de serviço PowerPivot.  
  
> [!NOTE]  
>  Para obter mais informações sobre a atualização da anexação do banco de dados do PowerPivot e do SharePoint, consulte o seguinte:  
  
-   [Migrar o PowerPivot para o SharePoint 2013](../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)  
  
-   [Visão geral do processo de atualização para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpar preparações antes de uma atualização do SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Atualizar bancos de dados do SharePoint 2010 para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>Consulte também  
 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Combinações do SharePoint e do servidor e suplemento Reporting Services com suporte &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [Instalar ou desinstalar o Reporting Services suplemento para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
