---
title: Pontos de dados vazios e nulos em gráficos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: faddd29d-4cc1-4c2c-8e29-d3d9918fe22a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1b869739cd944ac96104044efc2c79e91f8e8a7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848039"
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
