---
title: Compare os recursos de Business Intelligence em diferentes ambientes da Microsoft | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 12/15/2019
ms.openlocfilehash: 3305e682f6ccbbee4ac9710e29ae522eb7339910
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241208"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>Comparar recursos de Business Intelligence em diferentes ambientes Microsoft

O Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence pode ser implantado em vários ambientes diferentes incluindo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o SharePoint Server, SharePoint Online e Power BI para Office 365. Este tópico compara os componentes e recursos compatíveis em cada ambiente.  
  
Para obter mais informações comparando o SharePoint Server e o SharePoint Online, consulte [Comparar planos e opções do SharePoint](https://products.office.com/SharePoint/compare-sharepoint-plans).  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>Criar e gerenciar relatórios de BI e painéis  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online plano 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Sites BI|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]Clip|Não|Site do Power BI|  
|Gerenciamento e compartilhamento de consulta e administração de dados|Não|Não|Sim ** <sup>1</sup>**|  
|Integração com o Master Data Services (MDS) e Data Quality Services (DQS)|Sim|Não|Não|  
|Agendar atualização de dados|Sim, mas não aceita as pastas de trabalho que contêm dados Power Query|Não|Sim|  
|Consulta de linguagem natural (Q&A)|Não|Não|Sim ** <sup>2</sup>**|  
|Previsão de previsão|Não|Não|Sim ** <sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]integrar|Sim|Não|Não|  
|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] integração (Multidimensional e Tabular)|Sim|Não|Não|  
|Exportar painel interativo do Power View para apresentação do PowerPoint|Sim|Não|Não|  
|Criação de painel no navegador|Sim|Não|Não|  
|Monitoramento de uso|Sim|Não|Sim|  
|Aproveitar segurança de baseada em linha de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubos|Sim|Não|Não|  
|||||

 **<sup>1</sup>**  [entendendo a função dos administradores de dados em gerenciamento de dados](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) e [vídeo: gerenciamento de informações de Power bi e administração de dados](https://www.youtube.com/watch?v=8dHOj68ts7c).  
  
 **<sup>2</sup>**  [Power bi Q&A: otimizar uma pasta de trabalho do Power bi (modelagem de nuvem)](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/).  
  
 **<sup>3</sup>**  [apresentando novos recursos de previsão no Power View para o Office 365](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx).  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>Exibir e procurar dados, relatórios e painéis de BI  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online plano 2|Power BI para Office 365|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|Exibir pastas de trabalho do Microsoft Excel em um navegador|Sim, se a pasta de trabalho tiver menos de 2 GB de tamanho|Sim, se a pasta de trabalho tiver menos de 10 MB de tamanho|Sim, se a pasta de trabalho tiver menos de 250 MB de tamanho|  
|Exploração de dados no navegador em HTML5|Não|Não|Sim|  
|Aplicativo Mobile BI para acessar relatórios e painéis remotamente|Não|Não|Sim ** <sup>1</sup>**|  
|Pasta de trabalho do Excel com [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como uma fonte de dados **<sup>2</sup>**|Sim|Não|Não|  
|Capacidade de usar os recursos em diferentes navegadores e versões|Sim, para visualizações não Power View **<sup>3</sup>**|Sim, para tamanhos de arquivo de pasta de trabalho menores que 10 MB **<sup>3</sup>**|Sim ** <sup>3</sup>**|  
|||||

 **<sup>1</sup>**  [Microsoft Power bi](https://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).  
  
 **<sup>2</sup>**  [pastas de trabalho PowerPivot como uma fonte de dados](https://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [suporte móvel entre ferramentas de Business Intelligence (BI)](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) e [planejamento para Reporting Services e suporte a navegador Power View (Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx).  
  
## <a name="more-information"></a>Mais informações  
  
- [Recursos de BI no Excel e no Office 365](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743).  
  
- Para obter informações sobre os requisitos para usar sinônimos, consulte [otimizando Power bi Q&a com sinônimos & frases](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling) em pragmaticworks.com.  
  
- [Office Online, escolha sua rede social corporativa: Yammer ou News Feed?](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
- [Power bi para Office 365](https://www.microsoft.com/powerbi/default.aspx).  
  
- [Preços de Power bi](https://www.microsoft.com/powerBI/pricing.aspx).  
  
- [Análise e relatório com ferramentas de BI (business intelligence) da Microsoft](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>Conteúdo da comunidade

