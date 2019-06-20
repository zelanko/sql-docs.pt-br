---
title: Exibindo uma série com vários intervalos de dados em um gráfico (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 45da3d39-278e-4760-a4b3-9932c9547cf2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8c226cc9603aa687616d54fa95ee82c7f2b86792
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106002"
---
# <a name="displaying-a-series-with-multiple-data-ranges-on-a-chart-report-builder-and-ssrs"></a>Exibindo uma série com vários intervalos de dados em um gráfico (Construtor de Relatórios e SSRS)
  O gráfico usará os valores mínimo e máximo de uma série para calcular a escala do eixo. Quando uma série do gráfico contiver mais que um intervalo de dados, os pontos de dados poderão ficar obscuros e apenas alguns deles poderão ser visualizados facilmente no gráfico. Por exemplo, suponha que um relatório exiba informações sobre o total de vendas diário de um período de 30 dias.  
  
 ![Gráfico com vários intervalos de dados](../media/rs-multipledatarangeschart.gif "Gráfico com vários intervalos de dados")  
  
 Na maior parte do mês, as vendas ficam entre 10 e 40. No entanto, uma campanha publicitária de uma semana provocou um aumento repentino nas vendas no início de abril. Essa alteração nos dados de vendas produz uma distribuição irregular dos pontos de dados que reduz a legibilidade geral do gráfico.  
  
 Existem maneiras diferentes de melhorar a legibilidade:  
  
-   **Habilitar quebras de escala**. Se os dados formarem dois ou mais conjuntos de intervalos de dados, use uma quebra de escala para remover a lacuna entre os intervalos. Uma quebra de escala é uma faixa desenhada em uma área de plotagem para indicar a quebra entre os valores altos e baixos de uma série.  
  
-   **Filtrar valores desnecessários**. Se houver pontos de dados que estão encobrindo um intervalo de dados importante que deve aparecer no gráfico, remova os pontos indesejados usando um filtro de relatório. Para obter informações sobre como adicionar um filtro ao gráfico no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md).  
  
-   **Plotar cada intervalo de dados como uma série separada para comparar várias séries**. Se houver dois ou mais intervalos de dados, considere separá-los em séries distintas. Para obter mais informações, consulte [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-multiple-data-ranges-using-scale-breaks"></a>Exibindo vários intervalos de dados usando quebras de escala  
 Quando você habilita uma quebra de escala, o gráfico calcula onde desenhar uma linha no gráfico. Deve haver espaço suficiente entre os intervalos para desenhar uma quebra de escala. Por padrão, a quebra de escala poderá ser adicionada somente se houver uma separação entre os intervalos de dados de pelo menos 25% do gráfico.  
  
 ![Gráfico com quebra de escala](../media/rs-multipledatarangeschart-scalebreak.gif "Gráfico com quebra de escala")  
  
> [!NOTE]  
>  Não é possível especificar onde posicionar a quebra de escala em um gráfico. No entanto, você pode modificar como ela será calculada, o que será descrito adiante neste tópico.  
  
 Se você habilitar uma quebra de escala mas ela não aparecer, mesmo que haja distância suficiente entre os intervalos de dados, será possível definir a propriedade CollapsibleSpaceThreshold com um valor inferior a 25. CollapsibleSpaceThreshold especifica o percentual de espaço recolhível necessário entre os intervalos de dados. Para obter mais informações, consulte [Adicionar quebras de escala a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md).  
  
 Os gráficos suportam até cinco quebras de escala por gráfico; no entanto, exibir mais de uma quebra de escala pode deixar o gráfico ilegível. Se houver dois ou mais intervalos de dados, considere o uso de outro método para exibir esses dados. Para obter mais informações, consulte [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="unsupported-scale-break-scenarios"></a>Cenários de quebra de escala não suportados  
 As quebras de escala não são suportadas nos seguintes cenários:  
  
-   O gráfico está habilitado para 3D.  
  
-   Um eixo de valor logarítmico foi especificado.  
  
-   O eixo de valor mínimo ou máximo foi definido explicitamente.  
  
-   O tipo de gráfico é polar, radar, pizza, anel, funil, pirâmide ou algum gráfico empilhado.  
  
 Um exemplo de gráfico com quebras de escala está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
## <a name="see-also"></a>Consulte também  
 [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Efeitos 3D, bisel e outros efeitos em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-3d-bevel-and-other-report-builder.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Eixo, Opções do Eixo &#40;Construtor de Relatórios e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
