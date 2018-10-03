---
title: Compare os recursos de Business Intelligence em diferentes ambientes Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1fb759ee-8172-4c4c-9f7d-49af2c731006
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dfe97b4cab555b5da6224edef97c73958bb362b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144366"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>Comparar recursos de Business Intelligence em diferentes ambientes Microsoft
  Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence pode ser implantado em vários ambientes diferentes incluindo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o SharePoint Server, SharePoint Online e Power BI para Office 365. Este tópico compara os componentes e recursos compatíveis em cada ambiente.  
  
 Para obter mais informações comparando o SharePoint Server e o SharePoint Online, consulte [Comparar planos e opções do SharePoint](http://products.office.com/SharePoint/compare-sharepoint-plans).  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>Criar e gerenciar relatórios de BI e painéis  
  
||SQL Server 2014 e SharePoint Server 2013|SharePoint Online plano 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Sites BI|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] Galeria|não|Site do Power BI|  
|Gerenciamento e compartilhamento de consulta e administração de dados|não|não|Sim  **<sup>1</sup>**|  
|Integração com o Master Data Services (MDS) e Data Quality Services (DQS)|Sim|não|não|  
|Agendar atualização de dados|Sim, mas não aceita as pastas de trabalho que contêm dados Power Query|não|Sim|  
|Consulta de linguagem natural (Q&A)|não|não|Sim  **<sup>2</sup>**|  
|Previsão de previsão|não|não|Sim  **<sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] integração|Sim|não|não|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] integração (Multidimensional e Tabular)|Sim|não|não|  
|Exportar painel interativo do Power View para apresentação do PowerPoint|Sim|não|não|  
|Criação de painel no navegador|Sim|não|não|  
|Monitoramento de uso|Sim|não|Sim|  
|Linha de aproveitamento de segurança de baseada em [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubos|Sim|não|não|  
  
 **<sup>1</sup>**[Noções básicas sobre a função de administradores de dados no gerenciamento de dados](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) e [vídeo: administração de dados e gerenciamento de informações de BI do Power](https://www.youtube.com/watch?v=8dHOj68ts7c).    
  
 **<sup>2</sup>**[p e r do power BI: otimizar uma pasta de trabalho do Power BI (modelagem em nuvem)](https://support.office.com/article/Power-BI-Q-A-Optimize-a-Power-BI-workbook-cloud-modeling--96dc5941-d0f1-44e2-9d9d-c038a3a55849?ui=en-US&rs=en-US&ad=US).    
  
 **<sup>3</sup>**[apresentando novos recursos de previsão no Power View para o Office 365](http://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx).    
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>Exibir e procurar dados, relatórios e painéis de BI  
  
||SQL Server 2014 e SharePoint Server 2013|SharePoint Online plano 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Exibir pastas de trabalho do Microsoft Excel em um navegador|Sim, se a pasta de trabalho tiver menos de 2 GB de tamanho|Sim, se a pasta de trabalho tiver menos de 10 MB de tamanho|Sim, se a pasta de trabalho tiver menos de 250 MB de tamanho|  
|Exploração de dados no navegador em HTML5|não|não|Sim|  
|Aplicativo Mobile BI para acessar relatórios e painéis remotamente|não|não|Sim  **<sup>1</sup>**|  
|Pasta de trabalho do Excel com [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como uma fonte de dados  **<sup>2</sup>**|Sim|não|não|  
|Capacidade de usar os recursos em diferentes navegadores e versões|Sim, para visualizações não Power View  **<sup>3</sup>**|Sim, para a pasta de trabalho tamanhos de arquivo menor que 10 MB  **<sup>3</sup>**|Sim  **<sup>3</sup>**|  
  
 **<sup>1</sup>**[Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).    
  
 **<sup>2</sup>**[pastas de trabalho PowerPivot como uma fonte de dados  ](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**[suporte móvel nas ferramentas de Business Intelligence (BI)](http://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) e [Planning for Reporting Services e o suporte a navegador Power View (Reporting Services 2014)](http://msdn.microsoft.com/library/ms156511.aspx).    
  
## <a name="more-information"></a>Mais informações  
  
-   [Recursos de business intelligence no Excel, o SharePoint Online e o Power BI para Office 365](https://technet.microsoft.com/en-us/library/dn198235.aspx).  
  
-   Para obter informações sobre os requisitos para usar sinônimos, consulte [Adicionar sinônimos a um modelo de dados do Power Pivot Excel](https://support.office.com/Article/Add-synonyms-to-a-Power-Pivot-Excel-data-model-345f4f5b-5ec2-4998-bc46-a26bdc0810b6?ui=en-US&rs=en-US&ad=US).  
  
-   [Office Online, escolha a sua rede social da empresa: Yammer ou Newsfeed?](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
-   [Power BI para Office 365](http://www.microsoft.com/powerbi/default.aspx).  
  
-   [Preços do Power BI](http://www.microsoft.com/powerBI/pricing.aspx).  
  
-   [Comparar um site Central de BI a sites Power BI para Office 365](http://technet.microsoft.com/library/dn394343\(v=office.15\).aspx).  
  
-   [Apresentando as ferramentas de análise e relatórios de BI da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=617093)  
  
## <a name="community-content"></a>Conteúdo da Comunidade  
 [BI de autoatendimento da Microsoft no local vs em nuvem](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/).  
  
  
