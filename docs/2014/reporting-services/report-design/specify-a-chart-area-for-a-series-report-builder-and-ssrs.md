---
title: Especificar uma área do gráfico para uma série (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10157"
- sql12.rtp.rptdesigner.chartareaproperties.alignment.f1
ms.assetid: dc3c365b-c263-402a-bf6f-c2a7081db073
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: b604e8a3378285553542e4b03f6ba7c419315941
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009766"
---
# <a name="specify-a-chart-area-for-a-series-report-builder-and-ssrs"></a>Especificar uma área do gráfico para uma série (Construtor de Relatórios e SSRS)
  O gráfico é o contêiner de nível superior que inclui a borda exterior, o título e a legenda do gráfico. Por padrão, o gráfico contém uma área de gráfico padrão. A área do gráfico não é visível na superfície do gráfico, mas você pode imaginá-la como um contêiner que inclui somente os rótulos e o título dos eixos e a área de plotagem de uma ou mais séries. A ilustração a seguir mostra o conceito de áreas de gráfico dentro de um único gráfico.  
  
 ![Mostra um diagrama de uma área do gráfico](../media/chartareasdiagram.gif "Mostra um diagrama de uma área do gráfico")  
  
 Por padrão, todas as séries são adicionadas à área do gráfico padrão. Ao usar área, coluna, linha e gráficos de dispersão, qualquer combinação dessas séries pode ser exibida na mesma área do gráfico. Caso haja várias séries na mesma área de gráfico, a legibilidade do gráfico é reduzida. Talvez você queira separar os tipos de gráfico em várias áreas. Usar várias áreas de gráfico aumentará a legibilidade, tendo em vista comparações mais fáceis. Por exemplo, gráficos de ações por volume/preço costumam apresentar intervalos diferentes, mas as comparações podem ser feitas entre os dados de preço e volume no mesmo período.  
  
 As séries de barras, polar ou com forma só podem ser combinadas com séries dos mesmos tipos de gráfico na mesma área de gráfico. Caso você esteja usando um gráfico polar ou com forma, considere usar uma região de dados do gráfico separada para cada campo que deseja mostrar.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-series-with-a-new-chart-area"></a>Para associar uma série a uma nova área de gráfico  
  
1.  Clique com o botão direito do mouse em qualquer lugar do gráfico e selecione **Adicionar Nova Área de Gráfico**. Uma nova área de gráfico, em branco, é exibida no gráfico.  
  
2.  Clique com o botão direito do mouse na série do gráfico ou em uma série ou em um campo de dados na área apropriada do painel Dados do Gráfico e clique em **Propriedades da Série**.  
  
3.  Em **Eixos e Áreas do Gráfico**, selecione a área do gráfico em que você deseja mostrar a série.  
  
4.  (Opcional) Alinhe as áreas de gráfico verticalmente. Para isso, clique com o botão direito do mouse no gráfico e selecione **Propriedades da Área do Gráfico**. Em **Alinhamento**, selecione outra área de gráfico com a qual você deseja alinhar a área de gráfico selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Várias séries em um gráfico &#40;SSRS e construtor de relatórios&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;SSRS e construtor de relatórios&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Gráficos polares &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](shape-charts-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40;SSRS e construtor de relatórios&#41;](pie-charts-report-builder-and-ssrs.md)  
  
  