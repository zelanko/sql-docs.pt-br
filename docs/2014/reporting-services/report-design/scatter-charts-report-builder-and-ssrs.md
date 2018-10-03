---
title: Gráficos de dispersão (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2520ae24-0609-4890-807d-3267018aba8e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 58ab7a391134a36d305e3a1dc3a64543fbe4f673
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066476"
---
# <a name="scatter-charts-report-builder-and-ssrs"></a>Gráficos de dispersão (Construtor de Relatórios e SSRS)
  Um gráfico de dispersão exibe uma série como um conjunto de pontos. Os valores são representados pela posição dos pontos no gráfico. As categorias são representadas por diferentes marcadores no gráfico. Normalmente, os gráficos de dispersão são usados para comparar dados agregados por categorias. Para obter mais informações sobre como adicionar dados a um gráfico de dispersão, consulte [gráficos &#40;construtor de relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
 A ilustração a seguir mostra um exemplo de gráfico de dispersão.  
  
 ![Gráfico de dispersão](../media/rs-scatterchart.gif "Gráfico de dispersão")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Bolha.** Os gráficos de bolhas exibem a diferença entre dois valores de um ponto de dados baseado no tamanho da bolha. Quanto maior a bolha, maior a diferença entre os dois valores.  
  
-   **Bolha em 3D**. Um gráfico de bolhas exibido em 3D.  
  
## <a name="data-considerations-for-a-scatter-chart"></a>Considerações de dados para um gráfico de dispersão  
  
-   Normalmente, os gráficos de dispersão são usados para exibir e comparar valores numéricos, como dados científicos, estatísticos e de engenharia.  
  
-   Use o gráfico de dispersão quando quiser comparar grandes números de pontos de dados sem considerar o tempo. Quanto mais dados você inserir em um gráfico de dispersão, melhor serão as comparações que você pode criar.  
  
-   O gráfico de bolhas requer dois valores (superior e inferior) por ponto de dados.  
  
-   Os gráficos de dispersão são ideais para controlar a distribuição de valores e clusters de pontos de dados. Este será o melhor tipo de gráfico se o seu conjunto de dados contiver muitos pontos (por exemplo, milhares de pontos). Exibir várias séries em um gráfico de pontos causa uma distração visual e deve ser evitado. Neste cenário, considere o uso de um gráfico de linha.  
  
-   Por padrão, os gráficos de dispersão exibem pontos de dados como círculos. Se você tiver várias séries em um gráfico de dispersão, considere a possibilidade de alterar o marcador de cada ponto para outras formas, como quadrado, triângulo, losango, etc.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de linhas &#40;relatórios e SSRS&#41;](line-charts-report-builder-and-ssrs.md)  
  
  
