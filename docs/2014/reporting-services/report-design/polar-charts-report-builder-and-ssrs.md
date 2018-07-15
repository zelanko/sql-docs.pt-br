---
title: Gráficos polares (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c9402d8f-202a-4cdf-949e-50f5b1d2b885
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d59ad6ad8059e7261054470c310d8fd82dbd88d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208467"
---
# <a name="polar-charts-report-builder-and-ssrs"></a>Gráficos polares (Construtor de Relatórios e SSRS)
  Um gráfico polar exibe uma série como um conjunto de pontos agrupados por categoria em um círculo de 360 graus. Os valores são representados pelo comprimento do ponto, conforme medido do centro do círculo. Quanto mais distante o ponto está do centro, maior é o seu valor. São exibidos rótulos de categoria no perímetro do gráfico. Para obter mais informações sobre como adicionar dados a um gráfico polar, consulte [gráficos &#40;construtor de relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Gráfico de radar**. Um gráfico de radar exibe uma série como uma linha ou área circular. Ao contrário do gráfico polar, o gráfico de radar não exibe dados em termos de coordenadas polares.  
  
## <a name="data-considerations-for-polar-charts"></a>Considerações de dados para gráficos polares  
  
-   O gráfico de radar é útil para comparações entre várias séries de dados de categoria.  
  
-   Os gráficos polares são usados com mais frequência para fazer gráficos de dados polares, nos quais cada ponto de dados é determinado por um ângulo ou uma distância.  
  
-   Os gráficos polares não podem ser combinados com qualquer outro tipo de gráfico na mesma área de gráfico.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como um gráfico de radar pode ser usado. A tabela a seguir fornece dados de amostra do gráfico.  
  
|Nome|Sales|  
|----------|-----------|  
|Arbustos|61|  
|Sementes|78|  
|Bulbos|60|  
|Árvores|38|  
|Flores|81|  
  
 Nesse exemplo, o campo Nome é colocado na área Grupos de Categorias. O campo Vendas é colocado na área Valores. O campo Vendas é agregado automaticamente para o gráfico quando você o lança. O gráfico de radar calcula onde colocar os rótulos com base no número de valores no campo Vendas, que contém cinco valores e coloca rótulos em cinco pontos equidistantes em um círculo. Se o campo Vendas continha três valores, os rótulos seriam colocados em três pontos equidistantes em um círculo.  
  
 A ilustração a seguir mostra um exemplo de um gráfico de radar baseado nos dados apresentados.  
  
 ![Gráfico de radar](../media/rs-radarchart.gif "gráfico de Radar")  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Gráficos de linhas &#40;Construtor de Relatórios e SSRS&#41;](line-charts-report-builder-and-ssrs.md)   
 [Pontos de dados em gráficos vazios e nulos &#40;relatórios e SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
