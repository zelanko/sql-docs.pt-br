---
title: Topologias de implantação para recursos de SQL Server BI no SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d1d8d503fc5020fb9d44bb8daa4be79abd00dc0d
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "71952637"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>Topologias de implantação para recursos de BI do SQL Server no SharePoint
  Este tópico descreve as topologias comuns para instalar recursos de Business Intelligence do SQL Server no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] em ambientes do SharePoint 2010 e do SharePoint 2013. Por exemplo, instalações de único servidor e de três níveis.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **Neste tópico:**  
  
-   [Topologias de implantação de exemplo do SharePoint 2013](#bkmk_example_deployments_2013)  
  
    -   [PowerPivot para SharePoint 2013 e Reporting Services a implantação de três servidores](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [Implantação de servidor único PowerPivot para SharePoint 2013](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [Implantação do PowerPivot para SharePoint Server 2013 2](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [Implantação do PowerPivot para SharePoint Server 2013 3](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [Implantação de servidor único PowerPivot para SharePoint 2013 e Reporting Services](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [PowerPivot para SharePoint 2013 e Reporting Services a implantação de dois servidores](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [Topologias de implantação de exemplo do SharePoint 2010](#bkmk_example_deployments_2010)  
  
    -   [Implantações de servidor único](#bkmk_sharepoint2010_1server)  
  
    -   [Implantação em duas camadas](#bkmk_sharepoint2010_2server)  
  
    -   [Implantação de três camadas](#bkmk_sharepoint2010_3server)  
  
    -   [Implantação de expansão em três camadas](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="bkmk_example_deployments_2013"></a>Topologias de implantação de exemplo do SharePoint 2013  
 A opção de instalação **PowerPivot para SharePoint** do SQL Server não tem nenhuma dependência do SharePoint. Ela não usa o modelo de objeto ou as interfaces do SharePoint para dar suporte à integração. Portanto, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode ser instalado em qualquer computador que esteja executando o Windows Server 2008 R2 ou uma versão posterior. Ele pode ser, mas não precisa ser um servidor de aplicativos em um farm do SharePoint. Uma das etapas de configuração é apontar os Serviços do Excel para o servidor que executa o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para o balanceamento de carga e tolerância a falhas, é recomendável instalar e registrar vários servidores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executados no modo do SharePoint.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o modo do SharePoint** requer o sharepoint Server 2013 e utiliza a arquitetura do aplicativo de serviço do SharePoint.  
  
 As seções a seguir ilustram topologias comuns de implantação:  
  
###  <a name="bkmk_bi_Sharepoint2013_3tier"></a>PowerPivot para SharePoint 2013 e Reporting Services a implantação de três servidores  
 Na implantação de três servidores a seguir, o Mecanismo de Banco de Dados do SQL Server, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que estão sendo executados no modo do SharePoint e o SharePoint são executados em um servidor separado. O pacote do instalador do [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 (**spPowerPivot.msi**) deve ser executado no servidor do SharePoint.  
  
 ![Implantação de servidor SSAS e SSRS SharePoint Mode 3](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "Implantação de servidor SSAS e SSRS SharePoint Mode 3")  
  
|||  
|-|-|  
|**(1)**|Aplicativo de Serviços do Excel. O aplicativo de serviço é criado como parte da instalação do SharePoint.|  
|**(2)**|Aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale o suplemento de serviços de relatórios para SharePoint da mídia de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou do feature pack do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Execute o **spPowerPivot.msi** para instalar provedores de dados, a ferramenta de configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e a atualização de dados da agenda.|  
|**(6)**|Servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo SharePoint. Defina as **Configurações de Modelo de Dados** do Aplicativo de Serviços do Excel para usar este servidor.|  
|**(7)**|Conteúdo, configuração e bancos de dados de aplicativo de serviço do SharePoint.|  
  
 ![As configurações do SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configurações do SharePoint") [enviam comentários e informações de contato por meio do Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
###  <a name="bkmk_powerpivot_sharepoint2013_1server"></a>Implantação de servidor único PowerPivot para SharePoint 2013  
 Uma implantação de servidor único é útil para finalidades de teste, mas não é recomendável para implantações de produção.  
  
 O diagrama a seguir ilustra os componentes que fazem parte de uma implantação de servidor único do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 ![Implantação de servidor único PowerPivot para SharePoint](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "Implantação de servidor único PowerPivot para SharePoint")  
  
|||  
|-|-|  
|**(1)**|Aplicativo de Serviços do Excel. O aplicativo de serviço é criado como parte da instalação do SharePoint.|  
|**(2)**|Aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.|  
|**(3)**|Conteúdo, configuração e bancos de dados de aplicativo de serviço do SharePoint.|  
|**(4)**|Um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo SharePoint. Defina as **Configurações de Modelo de Dados** do Aplicativo de Serviços do Excel para usar este servidor.|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_2server"></a>Implantação do PowerPivot para SharePoint Server 2013 2  
 Na implantação de dois servidores a seguir, o Mecanismo de Banco de Dados do SQL Server e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint são executados em um servidor separado do SharePoint. Para o SharePoint 2013, o pacote do instalador do [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] (**spPowerPivot.msi**) é instalado no servidor do SharePoint.  
  
 o [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] estende o SharePoint Server 2013 para adicionar processamento de atualização de dados do servidor, provedores de dados, Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e suporte de gerenciamento para pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e pastas de trabalho do Excel com modelos de dados avançados.  
  
 O pacote do instalador está disponível como parte do feature pack do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . O Feature Pack pode ser baixado do centro de download [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [microsoft® SQL Server® 2014 PowerPivot® para Microsoft® SharePoint®](https://go.microsoft.com/fwlink/?LinkID=296473) (HYPERLINK "<https://go.microsoft.com/fwlink/?LinkID=296473>" \t "_ blank" <https://go.microsoft.com/fwlink/?LinkID=296473>).  
  
 ![Implantação do servidor do modo PowerPivot 2 do SSAS](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-mode-2server-deployment.gif "Implantação do servidor do modo PowerPivot 2 do SSAS")  
  
|||  
|-|-|  
|**(1)**|Aplicativo de Serviços do Excel. O aplicativo de serviço é criado como parte da instalação do SharePoint.|  
|**(2)**|Aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.|  
|**(3)**|EXECUTE o **spPowerPivot.msi** para instalar provedores de dados, a ferramenta de configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e a atualização de dados da agenda.|  
|**(4)**|Um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo SharePoint. Defina as **Configurações de Modelo de Dados** do Aplicativo de Serviços do Excel para usar este servidor.|  
|**(5)**|Conteúdo, configuração e bancos de dados de aplicativo de serviço do SharePoint.|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_3server"></a>Implantação do PowerPivot para SharePoint Server 2013 3  
 Na implantação de três servidores a seguir, o Mecanismo de Banco de Dados do SQL Server, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que estão sendo executados no modo do SharePoint e o SharePoint são executados em um servidor separado. O pacote do instalador do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 (spPowerPivot.msi) deve ser instalado no servidor do SharePoint.  
  
 ![COMO implantação do PowerPivot Mode3 Server](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "COMO implantação do PowerPivot Mode3 Server")  
  
|||  
|-|-|  
|**(1)**|Aplicativo de Serviços do Excel. O aplicativo de serviço é criado como parte da instalação do SharePoint.|  
|**(2)**|Aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.|  
|**(3)**|EXECUTE o spPowerPivot.msi para instalar provedores de dados, a ferramenta de configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e a atualização de dados da agenda.|  
|**(4)**|Um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo SharePoint. Defina as **Configurações de Modelo de Dados** do Aplicativo de Serviços do Excel para usar este servidor.|  
|**(5)**|Conteúdo, configuração e bancos de dados de aplicativo de serviço do SharePoint.|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a>Implantação de servidor único PowerPivot para SharePoint 2013 e Reporting Services  
 Uma implantação de servidor único é útil para finalidades de teste, mas não é recomendável para implantações de produção.  
  
 ![Implantação do servidor SSAS e SSRS SharePoint Mode 1](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "Implantação do servidor SSAS e SSRS SharePoint Mode 1")  
  
|||  
|-|-|  
|**(1)**|Aplicativo de Serviços do Excel. O aplicativo de serviço é criado como parte da instalação do SharePoint.|  
|**(2)**|Aplicativo de serviço PowerPivot. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale o suplemento de serviços de relatórios para SharePoint da mídia de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou do feature pack do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Conteúdo, configuração e bancos de dados de aplicativo de serviço do SharePoint.|  
|**(6)**|Servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo SharePoint. Defina as **Configurações de Modelo de Dados** do Aplicativo de Serviços do Excel para usar este servidor.|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a>PowerPivot para SharePoint 2013 e Reporting Services a implantação de dois servidores  
 Na implantação de dois servidores a seguir, o Mecanismo de Banco de Dados do SQL Server e o Analysis Services que estão sendo executados no modo do SharePoint são executados em um servidor separado do SharePoint. O pacote do instalador do PowerPivot para SharePoint 2013 **(PowerPivot. msi)** deve ser executado no servidor do SharePoint.  
  
 ![Implantação do servidor SSAS e SSRS SharePoint Mode 2](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "Implantação do servidor SSAS e SSRS SharePoint Mode 2")  
  
|||  
|-|-|  
|**(1)**|Aplicativo de Serviços do Excel. O aplicativo de serviço é criado como parte da instalação do SharePoint.|  
|**(2)**|Aplicativo de serviço PowerPivot. O nome padrão é **Aplicativo de Serviço PowerPivot Padrão**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale o suplemento de serviços de relatórios para SharePoint da mídia de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou do feature pack do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|EXECUTE o **spPowerPivot.msi** para instalar provedores de dados, a ferramenta de configuração do PowerPivot, a Galeria do PowerPivot e a atualização de dados da agenda.|  
|**(6)**|Servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em modo SharePoint. Defina as **Configurações de Modelo de Dados** do Aplicativo de Serviços do Excel para usar este servidor.|  
|**(7)**|Conteúdo, configuração e bancos de dados de aplicativo de serviço do SharePoint.|  
  
##  <a name="bkmk_example_deployments_2010"></a>Topologias de implantação de exemplo do SharePoint 2010  
 O diagrama a seguir mostra quais serviços e provedores são executados em cada camada. Observe que o diagrama inclui vários serviços internos; esses serviços são necessários para alguns cenários de BI do SQL Server. Os Serviços do Excel, os Serviços de Repositório Seguro e o Claims to Windows Token Service são necessários ou recomendáveis para uma implantação do PowerPivot para SharePoint ou do Reporting Services no SharePoint. Além disso, os provedores OLE DB MSOLAP e os Serviços ADO.NET são necessários para alguns cenários de acesso a dados PowerPivot. Opcionalmente, você poderá instalar o Analysis Services na camada de dados, se quiser criar relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] com base nos bancos de dados de modelo tabular hospedados fora do SharePoint.  
  
 ![Diagrama de arquitetura lógica](../../../2014/sql-server/install/media/sql11bisetup.gif "Diagrama de arquitetura lógica")  
  
##  <a name="bkmk_sharepoint2010_1server"></a>Implantações de servidor único  
 Você pode instalar todos os componentes de servidor, incluindo a camada de dados, em um único computador. Essa configuração de implantação será útil se você estiver avaliando o software ou desenvolvendo aplicativos personalizados que incluem o Reporting Services no modo do SharePoint. A configuração desta implantação é a mais simples. Como todos os componentes são instalados no mesmo computador, ela também usa menos licenças. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e o [!INCLUDE[ssDE](../../includes/ssde-md.md)] são instalados como uma única cópia licenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para instalar todos os recursos em um único servidor, instale o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sequencialmente, no mesmo servidor físico. Para obter instruções sobre uma configuração de servidor autônomo, consulte [lista de verificação de implantação: Reporting Services, Power View e PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_sharepoint2010_2server"></a>Implantação em duas camadas  
 Em geral, uma implantação em duas camadas corresponde ao SharePoint Server 2010 em um computador e o Mecanismo de Banco de Dados do SQL Server no segundo computador. Mover a camada de dados para um servidor dedicado é a configuração mais comum para um farm de dois computadores. Em um farm de duas camadas, você instala o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] no SharePoint Server. Todos os serviços Web no front-end e os serviços compartilhados na camada do aplicativo são executados no mesmo servidor físico. As etapas de instalação para uma implantação em duas camadas são muito semelhantes às de uma implantação autônoma, na qual você instala o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sequencialmente, no mesmo servidor físico.  
  
##  <a name="bkmk_sharepoint2010_3server"></a>Implantação de três camadas  
 Em geral, uma implantação em três camadas separa os serviços de front-end da Web de aplicativos de processamento ou que consomem muita memória. Nessa topologia, você instala o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] apenas no servidor de aplicativo. Os serviços Web executados no front-end da Web são instalados por meio de soluções implantadas nos aplicativos do farm, durante a configuração do servidor, como uma tarefa pós-instalação. O diagrama a seguir ilustra uma implantação em três camadas.  
  
 ![topologia de 3 servidores](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "topologia de 3 servidores")  
  
##  <a name="bkmk_sharepoint2010_scaleserver"></a>Implantação de expansão em três camadas  
 Esta topologia ilustra uma implantação em expansão que executa o mesmo serviço compartilhado em vários servidores, atendendo um volume maior de solicitações e fornecendo mais capacidade de processamento aos dados PowerPivot ou aos relatórios do Reporting Services. No diagrama abaixo, há três clusters de servidor de aplicativo, cada um executando uma combinação diferente de serviços compartilhados. Em um ambiente do SharePoint, a descoberta e a disponibilidade de serviço são inseridas no farm. O balanceamento de carga em vários servidores físicos executando o mesmo aplicativo de serviço compartilhado faz parte da arquitetura do serviço compartilhado.  
  
 Durante a implantação de um farm com vários servidores, não se esqueça de seguir as instruções neste artigo do SharePoint: [Vários servidores para um farm em três camadas (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834).  
  
 ![5-topologia de servidor](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "5-topologia de servidor")  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services instalação &#40;do SharePoint 2010&#41;e SharePoint 2013](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [Instalação do PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)   
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
