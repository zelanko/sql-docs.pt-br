---
title: "Gráfico de tipos (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7b23da886ccf8fc76cbe8e86a722e4e9a8f3e656
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---

# <a name="chart-types-report-builder-and-ssrs"></a>Tipos de gráficos (Construtor de Relatórios e SSRS)

É importante escolher um tipo de gráfico apropriado para o tipo de dados que você está apresentando. Isto determinará como os dados podem ser interpretados quando colocados em formato de gráfico. Por exemplo, se o conjunto de dados contiver muitos pontos de dados relacionados ao tamanho do gráfico, talvez seja melhor apresentá-lo usando um grafico de área, linha ou de dispersão. Para discussão em como preparar seus dados dependendo do tipo de gráfico selecionado, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>Escolhendo um tipo de gráfico  
 Cada tipo de gráfico tem características exclusivas para lhe ajudar a visualizar seu conjunto de dados. Você pode usar qualquer tipo de gráfico para exibir seus dados, mas esses serão mais facilmente lidos se usar um tipo de gráfico adequado para os seus dados, baseado no assunto que está tentando mostrar no seu relatório. A tabela a seguir resume os recursos de gráfico que afetam a adequação de um gráfico a seu conjunto de dados específico.  
  
 Você poderá alterar o tipo de gráfico depois de criá-lo. Para obter mais informações, consulte [Alterar um tipo de gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md).  
  
 Exemplos de muitos desses tipos de gráficos estão disponíveis como relatórios de exemplo. Para obter mais informações sobre como baixar relatórios de exemplo, consulte [relatórios de exemplo do construtor de relatórios e Designer de relatórios](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
|Tipo de gráfico|Exibir dados de taxa|Exibir dados de estoque|Exibir dados lineares|Exibir dados de vários valores|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[Gráficos de área &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)|||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||  
|[Gráficos de barras &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)|||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||  
|[Barras de dados](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||  
|[Gráficos de colunas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)|||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||  
|[Gráficos de linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)|||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||  
|[Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||||  
|[Gráficos polares &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||||  
|[Gráficos de intervalo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)|||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|  
|[Gráficos de dispersão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/scatter-charts-report-builder-and-ssrs.md)|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||  
|[Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||||  
|[Minigráficos](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|  
|[Gráficos de estoque &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/stock-charts-report-builder-and-ssrs.md)||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")||![Disponível](../../reporting-services/report-data/media/greencheck.gif "disponíveis")|  

## <a name="next-steps"></a>Próximas etapas

[Gráficos](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Pontos de dados vazios e nulos em gráficos](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
[Adicionar um gráfico a um relatório](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

