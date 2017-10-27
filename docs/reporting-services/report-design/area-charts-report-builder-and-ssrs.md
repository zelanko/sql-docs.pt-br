---
title: "Gráficos de área (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 245b236d-1d55-4744-b752-80bd133502aa
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cbb5e600306a5d107f7cbd542fb2c66abe96b35a
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="area-charts-report-builder-and-ssrs"></a>Gráficos de área (Construtor de Relatórios e SSRS)
  Um gráfico de área exibe uma série como um conjunto de pontos conectados por uma linha, com toda a área preenchida abaixo da linha. Para obter mais informações sobre como adicionar dados a um gráfico de área, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 A ilustração a seguir mostra um exemplo de um gráfico de áreas empilhadas. Os dados são bem-adequados para serem exibidos em um gráfico de áreas empilhadas porque o gráfico pode exibir os totais de todas as séries, bem como a proporção com que cada série contribui no total.  
  
 ![Gráfico de área](../../reporting-services/report-design/media/areachart.gif "gráfico de área")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Área empilhada**. Um gráfico de áreas no qual várias séries são empilhadas verticalmente. Se houver apenas uma série em seu gráfico, o gráfico de áreas empilhadas exibirá o mesmo que o gráfico de áreas.  
  
-   **Porcentual de área empilhada**. Um gráfico de áreas no qual várias séries são empilhadas verticalmente para ajustar toda a área de gráfico. Se houver apenas uma série em seu gráfico, o gráfico de áreas empilhadas exibirá o mesmo que o gráfico de áreas.  
  
-   **Área suave**. Um gráfico de áreas onde os pontos de dados são conectados por uma linha suave em vez de uma linha regular. Use um gráfico de áreas suaves em vez de um gráfico de áreas quando você estiver mais preocupado com as tendências de exibição do que com a exibição dos valores dos pontos de dados individuais.  
  
## <a name="data-considerations-for-area-charts"></a>Considerações de dados para gráficos de área  
  
-   Junto com o gráfico de linhas, o gráfico de áreas é o único tipo de gráfico que exibe dados contiguamente. Por esta razão, normalmente um gráfico de áreas é usado para representar dados que ocorrem em um período de tempo contínuo.  
  
-   O porcentual de um gráfico de áreas empilhadas é útil para mostrar dados proporcionais que ocorrem com o passar do tempo.  
  
-   Se houver apenas uma série, um gráfico de áreas empilhadas será desenhado em um gráfico de áreas.  
  
-   Em um gráfico de áreas comum, se os valores em várias séries forem semelhantes, as séries serão sobrepostas, impedindo a exibição de valores de pontos de dados importantes. Esse problema pode ser solucionado alterando o tipo de gráfico para um gráfico de área empilhada, que foi desenvolvido para mostrar várias séries em um gráfico de áreas.  
  
-   Caso o gráfico de áreas empilhadas contenha lacunas, pode ser que seu conjunto de dados tenha valores vazios, que serão exibidos como uma seção vaga nesse tipo de gráfico. Se o seu conjunto de dados tiver valores vazios, insira pontos vazios no gráfico. Ao adicionar pontos vazios, as áreas vazias no gráfico serão preenchidas com uma cor diferente para indicar valores nulos ou zero. Para obter mais informações, consulte [pontos vazios de adicionar a um gráfico de &#40; Construtor de relatórios e SSRS &#41; ](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md).  
  
-   O comportamento do gráfico de áreas é bem semelhante ao comportamento dos gráficos de colunas e linhas. Se você estiver fazendo uma comparação entre várias séries, use um gráfico de colunas. Se estiver analisando tendências durante um determinado período de tempo, use um gráfico de linhas.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tipos de gráfico &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Gráficos de linha &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)   
 [Alterar um tipo de gráfico &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md)   
 [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  

