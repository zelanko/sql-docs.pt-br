---
title: "Especificar uma área do gráfico para uma série (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10157"
- sql13.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d88358516e05214b230ec57b6243168ef9aac048
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>Especificar uma área do gráfico para uma série (Construtor de Relatórios e SSRS)
  Em relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , o *gráfico* é o contêiner de nível superior que inclui a borda exterior, o título e a legenda do gráfico. Por padrão, o gráfico contém uma *área de gráfico*. A área do gráfico não é visível na superfície do gráfico, mas você pode imaginá-la como um contêiner que inclui somente os rótulos e o título dos eixos e a área de plotagem de uma ou mais séries. A ilustração a seguir mostra o conceito de várias áreas de gráfico dentro de um único gráfico.  
  
 ![Mostra um diagrama de uma área do gráfico](../../reporting-services/report-design/media/chartareasdiagram.gif "mostra um diagrama de uma área do gráfico")  
  
 Por padrão, todas as séries são adicionadas à área do gráfico padrão. Ao usar área, coluna, linha e gráficos de dispersão, qualquer combinação dessas séries pode ser exibida na mesma área do gráfico. Caso haja várias séries na mesma área de gráfico, a legibilidade do gráfico é reduzida. Talvez você queira separar os tipos de gráfico em várias áreas. Usar várias áreas de gráfico aumentará a legibilidade, tendo em vista comparações mais fáceis. Por exemplo, gráficos de ações por volume/preço costumam apresentar intervalos diferentes, mas as comparações podem ser feitas entre os dados de preço e volume no mesmo período.  
  
 As séries de barras, polar ou com forma só podem ser combinadas com séries dos mesmos tipos de gráfico na mesma área de gráfico. Caso você esteja usando um gráfico polar ou com forma, considere usar uma região de dados do gráfico separada para cada campo que deseja mostrar.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-associate-a-series-with-a-new-chart-area"></a>Para associar uma série a uma nova área de gráfico  
  
1.  Clique com o botão direito do mouse em qualquer lugar do gráfico e selecione **Adicionar Nova Área de Gráfico**. Uma nova área de gráfico, em branco, é exibida no gráfico.  
  
2.  Clique com o botão direito do mouse na série do gráfico ou em uma série ou em um campo de dados na área apropriada do painel Dados do Gráfico e clique em **Propriedades da Série**.  
  
3.  Em **Eixos e Áreas do Gráfico**, selecione a área do gráfico em que você deseja mostrar a série.  
  
4.  (Opcional) Alinhe as áreas de gráfico verticalmente. Para isso, clique com o botão direito do mouse no gráfico e selecione **Propriedades da Área do Gráfico**. Em **Alinhamento**, selecione outra área de gráfico com a qual você deseja alinhar a área de gráfico selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Gráficos polares &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)   
 [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
