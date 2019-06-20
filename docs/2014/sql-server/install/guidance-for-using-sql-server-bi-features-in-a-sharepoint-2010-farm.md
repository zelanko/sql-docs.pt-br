---
title: Diretrizes para usar recursos de BI do SQL Server em um Farm do SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ae552c12c3d4773d6a05a6d61c7644eb245b68ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095002"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010
  Este tópico resume a disponibilidade de recursos com base nas versões e nas edições do software que você está usando. Também explica os requisitos de instalação do SharePoint 2010 para o uso de recursos específicos do SQL Server. Para obter informações relacionadas ao SharePoint 2013, consulte [topologias de implantação para recursos de BI do SQL Server no SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
 Neste tópico:  
  
-   [Requisitos gerais SharePoint 2010](#bkmk_generalsharepoint)  
  
-   [SharePoint 2010 Service Pack 1 (SP1)](#bkmk_sp1)  
  
-   [Suporte a edições do SharePoint e o recurso de BI](#bkmk_vers)  
  
-   [Ferramenta de preparação de produtos do SharePoint 2010](#bkmk_prereq)  
  
-   [Requisitos e sugestões para executar a instalação do SharePoint](#bkmk_install)  
  
##  <a name="bkmk_generalsharepoint"></a> Requisitos gerais SharePoint 2010  
  
-   Os produtos do SharePoint 2010 funcionam apenas em 64 bits. Se você tiver uma instalação de 32 bits de uma versão anterior do SharePoint e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no modo Integrado do SharePoint, não poderá realizar a atualização para o SharePoint 2010. Para obter mais informações, consulte a documentação do SharePoint.  
  
-   O Reporting Services inclui um suplemento para produtos do SharePoint. As configurações com suporte para o suplemento e o servidor de relatório estão disponíveis em um nível mais granular do que o indicado aqui. Para obter mais informações, consulte [combinações do SharePoint e com suporte e servidor do Reporting Services Add-in &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   As ferramentas de desenvolvedor do SharePoint só dão suporte a uma configuração autônoma do SharePoint.  Para obter mais informações, consulte a documentação do SharePoint: [Requisitos para desenvolver soluções do SharePoint](https://msdn.microsoft.com/library/ee231582.aspx).  
  
##  <a name="bkmk_vers"></a> Suporte a edições do SharePoint e o recurso de BI  
 Alguns recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence só têm suporte nas edições específicas dos produtos do SharePoint.  
  
|Recursos com suporte|Produto do SharePoint|  
|------------------------|------------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.<br /><br /> Alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.|  
|Integração geral de recursos e exibição de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com SharePoint.|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard e Enterprise Editions.<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)].|  
  
 Para obter mais informações, consulte [recursos compatíveis com as edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).  
  
##  <a name="bkmk_sp1"></a> SharePoint 2010 Service Pack 1 (SP1)  
 É recomendado que você atualize sua instalação do SharePoint 2010 para SharePoint 2010 Service Pack 1 (SP1). O SharePoint SP1 é obrigatório nos casos a seguir:  
  
-   Você quer usar a versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do mecanismo de banco de dados para os bancos de dados de conteúdo do SharePoint ou bancos de dados do catálogo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Você quer usar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e a ferramenta de configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 Um dos principais motivos SP1 é necessário para instalações do SharePoint em execução com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] é o recurso de mecanismo de banco de dados **sp_dboption**, que foi preterido em uma versão anterior, foi descontinuado a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versão. Para obter mais informações, consulte [funcionalidade do mecanismo de banco de dados descontinuada no SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  
### <a name="sharepoint-2010-sp1-installation-guidance"></a>Orientação de instalação do SharePoint 2010 SP1  
 [Baixe o SharePoint Server 2010 SP1](https://go.microsoft.com/fwlink/?LinkID=219697) e aplicá-lo em todos os servidores no farm.  
  
> [!NOTE]  
>  Em um farm existente, você precisará usar um dos seguintes **adicionais** atualizam etapas para concluir o SharePoint SP1. Para obter mais informações, consulte [problemas conhecidos quando você instala o Office 2010 SP1 e o SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126) e [descrição do SharePoint Server 2010 SP1](https://support.microsoft.com/kb/2460045):  
  
-   **Assistente de configuração de produtos do SharePoint:** Execute o Assistente para concluir a atualização do SP1 e a configuração.  
  
-   **Conclua a atualização com psconfig:** Execute o comando `psconfig -upgrade` para concluir a atualização do SP1  
  
 Para obter mais informações, consulte a seção "atualização" do [(SharePoint Server 2010)](https://technet.microsoft.com/library/cc263093.aspx) e [Central de recursos: Atualizações para produtos do SharePoint 2010](https://technet.microsoft.com/sharepoint/ff800847.aspx)  
  
## <a name="sharepoint-installation-with-sql-server-bi-features"></a>Instalação do SharePoint com recursos de BI do SQL Server  
  
###  <a name="bkmk_prereq"></a> Ferramenta de preparação de produtos do SharePoint 2010  
 A Ferramenta de Preparação de Produtos do SharePoint habilita as funções de servidor no sistema operacional e instala outros pré-requisitos de software necessários para uma instalação do SharePoint. A tabela a seguir identifica as etapas adicionais para configurar o servidor para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Componente|Ação|  
|---------------|------------|  
|Suplemento Reporting Services|A ferramenta de Preparação de Produtos do SharePoint 2010 instala a versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] do suplemento Reporting Services. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui uma versão mais nova do suplemento que é necessária para recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O suplemento pode ser instalado com o uso do assistente de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bem como pode ser baixado do MSDN. Para obter mais informações sobre onde obter a versão atual do suplemento e como instalá-lo, consulte [onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md) e [instalar ou desinstalar o Reporting Services Suplemento para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).|  
|Provedor OLE DB do Analysis Services (MSOLAP)|O SharePoint 2010 instala a versão SQL Server 2008 do provedor OLE DB como parte de uma implantação dos Serviços do Excel. Essa versão não tem suporte para o acesso a dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Você deve instalar versões mais recentes do provedor nos SharePoint Servers que tenham suporte para conexões de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Para obter mais informações, consulte [instalar o Analysis Services OLE DB Provider em servidores SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)|  
|Serviços ADO.NET|O SharePoint 2010 lista serviços ADO.NET na lista de pré-requisitos, mas o instalador de pré-requisitos não instala esse item. Para adicionar serviços ADO.NET, você deve instalá-los manualmente. A instalação dos serviços ADO.NET será necessária se você quiser usar listas do SharePoint como feeds de dados para pastas de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou relatórios do Reporting Services. Para obter instruções, consulte [exportações das listas do SharePoint do feed de instalar o ADO.NET Data Services para dar suporte a dados](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).|  
  
###  <a name="bkmk_install"></a> Requisitos e sugestões para executar a instalação do SharePoint  
 Os recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalados por você e a ordem de instalação desses recursos determinarão quais níveis de integração com o SharePoint serão possíveis. Por exemplo, embora algum nível de integração de recursos esteja disponível por meio do Reporting Services em um SharePoint Server que use um banco de dados interno, a maioria dos cenários de integração de recursos requer uma instalação de farm do SharePoint, pois apenas uma instalação de farm fornece a infraestrutura necessária para alguns recursos de BI.  
  
 Um farm do SharePoint pode ser constituído por um único servidor ou vários servidores. O que distingue um farm de uma instalação autônoma é a presença de uma infraestrutura adicional, como o Claims to Windows Token Service.  
  
 Um farm é habilitado quando você escolhe a **Farm de servidores** opção na instalação do SharePoint. Você deverá ter uma instalação de farm se quiser usar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Há suporte para a instalação autônoma do SharePoint e isso é comum para ambientes de desenvolvimento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No entanto, uma instalação de farm do SharePoint é recomendável para um ambiente de produção.  
  
 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")  
  
 Uma instalação completa de servidor também é necessária para o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")  
  
 A última página do assistente de instalação solicita que você configure o farm e, opcionalmente, configure um aplicativo Web padrão e a coleção de sites raiz. A maioria dos usuários da instalação segue esse caminho de instalação. Se, por alguma razão, você não configurar o farm, poderá usar a opção de configuração de farm na Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para configurar o farm.  
  
 Nas versões anteriores, deixar o farm não configurado era recomendável para instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] porque isso reduzia as etapas necessárias se você usou as opções de instalação do SQL Server para instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint em um estado pronto para uso. Nessa versão, isso não é mais importante. Você pode usar a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para ajustar um farm existente para que use as configurações recomendadas para uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
 O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode ser instalado em um farm existente do SharePoint. Você pode instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou SharePoint em qualquer ordem, mas a configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] variará dependendo da ordem. Para obter mais informações, consulte [adicionar outro servidor de relatório a um Farm &#40;expansão SSRS&#41; ](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")  
  
## <a name="see-also"></a>Consulte também  
 [Instalação e implantação do SharePoint Server 2010](https://technet.microsoft.com/sharepoint/ee518643.aspx)   
 [Vários servidores para um farm de três camadas (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)  
  
  
