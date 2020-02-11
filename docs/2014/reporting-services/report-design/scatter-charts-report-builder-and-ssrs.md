---
title: Gráficos de dispersão (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2520ae24-0609-4890-807d-3267018aba8e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dde53428c738fc30595d17b62175b50835fe7ec2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105034"
---
# <a name="scatter-charts-report-builder-and-ssrs"></a>Gráficos de dispersão (Construtor de Relatórios e SSRS)
  Um gráfico de dispersão exibe uma série como um conjunto de pontos. Os valores são representados pela posição dos pontos no gráfico. As categorias são representadas por diferentes marcadores no gráfico. Normalmente, os gráficos de dispersão são usados para comparar dados agregados por categorias. Para obter mais informações sobre como adicionar dados a um gráfico de dispersão, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
 A ilustração a seguir mostra um exemplo de gráfico de dispersão.  
  
 ![Gráfico de dispersão](../media/rs-scatterchart.gif "Gráfico de dispersão")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Emergi.** Os gráficos de bolhas exibem a diferença entre dois valores de um ponto de dados baseado no tamanho da bolha. Quanto maior a bolha, maior a diferença entre os dois valores.  
  
-   **bolha 3D**. Um gráfico de bolhas exibido em 3D.  
  
## <a name="data-considerations-for-a-scatter-chart"></a>Considerações de dados para um gráfico de dispersão  
  
-   Normalmente, os gráficos de dispersão são usados para exibir e comparar valores numéricos, como dados científicos, estatísticos e de engenharia.  
  
-   Use o gráfico de dispersão quando quiser comparar grandes números de pontos de dados sem considerar o tempo. Quanto mais dados você inserir em um gráfico de dispersão, melhor serão as comparações que você pode criar.  
  
-   O gráfico de bolhas requer dois valores (superior e inferior) por ponto de dados.  
  
-   Os gráficos de dispersão são ideais para controlar a distribuição de valores e clusters de pontos de dados. Este será o melhor tipo de gráfico se o seu conjunto de dados contiver muitos pontos (por exemplo, milhares de pontos). Exibir várias séries em um gráfico de pontos causa uma distração visual e deve ser evitado. Neste cenário, considere o uso de um gráfico de linha.  
  
-   Por padrão, os gráficos de dispersão exibem pontos de dados como círculos. Se você tiver várias séries em um gráfico de dispersão, considere a possibilidade de alterar o marcador de cada ponto para outras formas, como quadrado, triângulo, losango, etc.  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de linhas &#40;Construtor de Relatórios e SSRS&#41;](line-charts-report-builder-and-ssrs.md)  
  
  
