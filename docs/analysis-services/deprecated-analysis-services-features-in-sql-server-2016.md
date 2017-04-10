---
title: "Recursos do Analysis Services preteridos no SQL Server 2016 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Compatibilidade com versões anteriores do Analysis Services"
  - "Compatibilidade com versões anteriores do SSAS"
  - "Compatibilidade com versões anteriores do SQL Server Analysis Services"
  - "recursos preteridos [Analysis Services]"
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# Recursos do Analysis Services preteridos no SQL Server 2016
  Um *recurso preterido* é um recurso que será retirado do produto em uma versão futura, mas que ainda tem suporte e foi incluído na versão atual para manter a compatibilidade com versões anteriores. Em geral, um recurso preterido será removido em uma versão principal, geralmente dentro de duas versões do anúncio original. Por exemplo, os recursos preteridos anunciados no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] provavelmente não terão mais suporte no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 **Sem suporte na próxima versão principal do SQL Server**  
  
|||  
|-|-|  
|**Categoria**|**Recurso**|  
|Multidimensional|Partições remotas|  
|Multidimensional|Grupos de medidas vinculados remotos|  
|Multidimensional|Write-back dimensional|  
|Multidimensional|Dimensões vinculadas|  
  
 **Sem suporte em uma versão futura do SQL Server**  
  
|||  
|-|-|  
|**Categoria**|**Recurso**|  
|Multidimensional|Notificações de tabela do SQL Server para o cache pró-ativo.  <br />A substituição é usar a sondagem para o cache pró-ativo. <br />Consulte [Cache pró-ativo &#40;Dimensões&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) e [Cache pró-ativo e &#40;Partições&#41;](../Topic/Proactive%20Caching%20\(Partitions\).md).|  
|Multidimensional|Cubos de sessão. Não há nenhuma substituição.|  
|Multidimensional|Cubos locais. Não há substituições.|  
|Tabular|Os níveis de compatibilidade de modelo de tabela 1100 e 1103 não terão suporte em uma versão futura. A substituição serve para definir modelos de nível de compatibilidade 1200, convertendo definições de modelo para metadados tabulares. Consulte [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|Ferramentas|SQL Server Profiler para captura de rastreamento<br /><br /> A substituição é usar o Extended Events Profiler interno no SQL Server Management Studio.  <br /> Consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Ferramentas|Server Profiler para reprodução de rastreamento <br />Substituição. Não há nenhuma substituição.|  
|APIs Trace Management Objects e Trace|Objetos Microsoft.AnalysisServices.Trace (contêm as APIs para os objetos Analysis Services Trace e Replay). A substituição é composta por várias partes:<br /><br /> -   Configuração de rastreamento: Microsoft.SqlServer.Management.XEvent<br />-   Leitura de rastreamento: Microsoft.SqlServer.XEvent.Linq<br />-   Reprodução de rastreamento: nenhuma|  
  
> [!NOTE]  
>  Os anúncios anteriores de recursos preteridos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] permanecem em vigor. Como o código de suporte a esses recursos ainda não foi retirado do produto, muitos desses recursos ainda estão presentes nesta versão. Embora os recursos anteriormente preteridos ainda possam ser acessados, eles são considerados preteridos e podem ser fisicamente removidos do produto a qualquer momento durante o lançamento do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . É altamente recomendável que você evite usar recursos preteridos em novos modelos ou aplicativos com base no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## Consulte também  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)   
 [Funcionalidade descontinuada do Analysis Services no SQL Server 2016](../analysis-services/discontinued-analysis-services-functionality-in-sql-server-2016.md)  
  
  