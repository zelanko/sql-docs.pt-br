---
title: Especificar área do gráfico para uma série (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10157"
- sql13.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 32f16dd226167c180de81a456a6493f1c717b481
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080951"
---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>Especificar uma área do gráfico para uma série (Construtor de Relatórios e SSRS)
  Em relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , o *gráfico* é o contêiner de nível superior que inclui a borda exterior, o título e a legenda do gráfico. Por padrão, o gráfico contém uma *área de gráfico*. A área do gráfico não é visível na superfície do gráfico, mas você pode imaginá-la como um contêiner que inclui somente os rótulos e o título dos eixos e a área de plotagem de uma ou mais séries. A ilustração a seguir mostra o conceito de várias áreas de gráfico dentro de um único gráfico.  
  
 ![Mostra um diagrama de uma área do gráfico](../../reporting-services/report-design/media/chartareasdiagram.gif "Mostra um diagrama de uma área do gráfico")  
  
 Por padrão, todas as séries são adicionadas à área do gráfico padrão. Ao usar área, coluna, linha e gráficos de dispersão, qualquer combinação dessas séries pode ser exibida na mesma área do gráfico. Caso haja várias séries na mesma área de gráfico, a legibilidade do gráfico é reduzida. Talvez você queira separar os tipos de gráfico em várias áreas. Usar várias áreas de gráfico aumentará a legibilidade, tendo em vista comparações mais fáceis. Por exemplo, gráficos de ações por volume/preço costumam apresentar intervalos diferentes, mas as comparações podem ser feitas entre os dados de preço e volume no mesmo período.  
  
 As séries de barras, polar ou com forma só podem ser combinadas com séries dos mesmos tipos de gráfico na mesma área de gráfico. Caso você esteja usando um gráfico polar ou com forma, considere usar uma região de dados do gráfico separada para cada campo que deseja mostrar.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-associate-a-series-with-a-new-chart-area"></a>Para associar uma série a uma nova área de gráfico  
  
1.  Clique com o botão direito do mouse em qualquer lugar do gráfico e selecione **Adicionar Nova Área de Gráfico**. Uma nova área de gráfico, em branco, é exibida no gráfico.  
  
2.  Clique com o botão direito do mouse na série do gráfico ou em uma série ou em um campo de dados na área apropriada do painel Dados do Gráfico e clique em **Propriedades da Série**.  
  
3.  Em **Eixos e Áreas do Gráfico**, selecione a área do gráfico em que você deseja mostrar a série.  
  
4.  (Opcional) Alinhe as áreas de gráfico verticalmente. Para isso, clique com o botão direito do mouse no gráfico e selecione **Propriedades da Área do Gráfico**. Em **Alinhamento**, selecione outra área de gráfico com a qual você deseja alinhar a área de gráfico selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Gráficos polares &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)   
 [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
