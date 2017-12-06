---
title: "Pontos de dados vazios e nulos em gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: faddd29d-4cc1-4c2c-8e29-d3d9918fe22a
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a11da5e614ba9a6630c0c82317400af6e035e70d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="empty-and-null-data-points-in-charts-report-builder-and-ssrs"></a>Pontos de dados vazios e nulos em gráficos (Construtor de Relatórios e SSRS)

  Se você estiver exibindo campos com valores vazios ou nulos em um gráfico no seu relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o gráfico poderá não ficar como você espera. Gráficos processam valores vazios de maneira diferente dependendo do tipo de gráfico especificado:  
  
-   Se o gráfico for do tipo linear (barras, colunas, dispersão, linhas, área, intervalo), os valores vazios serão exibidos como espaços vazios ou "lacunas". Para indicar pontos vazios, é necessário adicionar espaços reservados de pontos vazios. Para obter mais informações, consulte [Adicionar pontos vazios a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md).  
  
-   Se o gráfico for do tipo linear contíguo (área, barra, coluna, linha, dispersão), pontos de dados vazios serão adicionados ao gráfico para manter a continuidade na série.  
  
-   Se o gráfico for de tipo não linear (polar, pizza, rosca, funil ou pirâmide), os valores vazios serão omitidos da exibição do gráfico.  
  
-   Em tipos de gráfico forma, valores nulos são omitidos.  
  
 Um exemplo de um gráfico com pontos de dados vazios está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="removing-empty-or-null-values"></a>Removendo valores vazios ou nulos  
 Para evitar o obscurecimento de dados importantes, considere a remoção de valores vazios do conjunto de dados. Para filtrar nulos, é possível usar a cláusula NOT IS NULL na consulta. Como alternativa, é possível adicionar uma expressão de filtragem que especifique que você deseja exibir apenas valores não iguais a zero. Para obter mais informações, consulte [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
## <a name="fields-with-no-values-in-a-chart"></a>Campos sem valores em um gráfico  
 Se um campo não contiver nenhum valor no conjunto de dados retornados, será exibido um gráfico vazio sem nenhum ponto de dados, mas o nome da série (normalmente o nome do campo) será adicionado como um item de legenda.  
  
 Esse comportamento é diferente do caso em que há zero linhas de dados no conjunto de dados retornado, o que pode ocorrer quando o relatório é parametrizado e o valor selecionado retorna um conjunto de resultados vazio. Se a consulta do conjunto de dados retornar zero linhas de dados, será exibida uma mensagem em tempo de execução para indicar que nenhum dado pode ser mostrado. É possível personalizar essa mensagem modificando a legenda NoDataMessage do relatório no painel **Propriedades** . Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  

## <a name="next-steps"></a>Próximas etapas

[Gráficos](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Formatando um gráfico](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[Adicionar um gráfico a um relatório](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)   
[Solução de problemas de gráficos](../../reporting-services/report-design/troubleshoot-charts-report-builder-and-ssrs.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
