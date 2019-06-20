---
title: Gráficos de colunas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e8477b4e8e0e6c0fc6e4801a975b11d79dadf83f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106227"
---
# <a name="column-charts-report-builder-and-ssrs"></a>Column Charts (Report Builder and SSRS)
  Um gráfico de coluna exibe uma série como um conjunto de barras verticais agrupadas por categoria. Os gráficos de coluna são úteis para mostrar alterações de dados em um período de tempo ou para ilustrar comparações entre itens. O gráfico de coluna plano está bem relacionado ao gráfico de barras, que exibe séries como conjuntos de barras horizontais e o gráfico de coluna de intervalo, que exibe uma série como conjuntos de barras verticais com pontos de início e término variáveis. Para obter mais informações, consulte [Gráfico de barras &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md) e [Gráficos de intervalo &#40;Construtor de Relatórios e SSRS&#41;](range-charts-report-builder-and-ssrs.md).  
  
 O gráfico de colunas é o mais adequado para esses dados porque todas as três séries compartilham um período de tempo comum, permitindo que sejam feitas comparações válidas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>Variações de um gráfico de colunas  
  
-   **Empilhado**. Um gráfico de colunas no qual várias séries são empilhadas verticalmente. Se houver apenas uma série em seu gráfico, o gráfico de colunas empilhadas exibirá o mesmo que o gráfico de colunas.  
  
-   **Por cento empilhado**. Um gráfico de colunas no qual várias séries são empilhadas verticalmente para se ajustarem a 100% da área do gráfico. Se houver apenas uma série em seu gráfico, todas as barras de colunas serão ajustadas a 100% da área do gráfico.  
  
-   **3D clusterizado**. Um gráfico de colunas que mostra séries individuais em linhas separadas em um gráfico 3D.  
  
-   **Cilindro em 3D**. Um gráfico de colunas cujas barras têm forma de cilindros em um gráfico 3D.  
  
-   `Histogram`. Um gráfico de colunas que o gráfico calcula de forma que suas barras sejam organizadas em uma distribuição normal.  
  
-   `Pareto`. Um gráfico de colunas cujas barras são organizadas da mais alta para a mais baixa.  
  
## <a name="data-considerations-for-a-column-chart"></a>Considerações de dados para um gráfico de colunas  
  
-   Gráficos de barras e colunas são usados com mais frequência para mostrar comparações entre grupos. Se mais de três séries estiverem presentes no gráfico, considere usar um gráfico de colunas ou barras empilhadas. Você também pode coletar gráficos de barras ou colunas empilhadas em vários grupos se tiver várias séries em seu gráfico. Para obter mais informações, consulte [gráficos de barras &#40;construtor de relatórios e SSRS&#41; ](charts-report-builder-and-ssrs.md) e *gráficos de colunas*.  
  
-   Em um gráfico de colunas, você tem menos espaço para que sejam exibidos rótulos de eixo de categoria na horizontal. Se você não tiver mais rótulos de categoria, considere usar um gráfico de barras ou alterar o ângulo de rotação do rótulo.  
  
-   Você pode adicionar estilos de desenho especiais às barras individuais em um gráfico de colunas para aumentar seu impacto visual. Os estilos de desenho incluem entalhe, relevo, cilindro e claro para escuro. Esses efeitos são projetados para melhorar a aparência de seu gráfico 2D. Se estiver usando um gráfico 3D, os estilos de desenho ainda serão aplicados, mas podem não ter o mesmo efeito. Para obter mais informações sobre como adicionar um estilo de desenho a um gráfico de barras, consulte [Adicionar estilos de bisel, relevo e textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
-   Exclusivo para gráficos de colunas é a habilidade de mostrar seu gráfico como um histograma ou gráfico de Pareto. Para fazer isso, defina a propriedade ShowColumnAs como `Histogram` ou `Pareto` na janela Propriedades para `true`.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Gráficos de barras &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Gráficos de intervalo &#40;Construtor de Relatórios e SSRS&#41;](range-charts-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um gráfico de barras ao relatório &#40;Construtor de Relatórios&#41;](../tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
