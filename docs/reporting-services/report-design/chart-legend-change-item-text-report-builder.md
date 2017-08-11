---
title: "Alterar o texto de um Item de legenda (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8c253794b7b884a3dd7835409e256245ae0dc5a2
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="chart-legend---change-item-text-report-builder"></a>Legenda do gráfico - Item alterar texto (construtor de relatórios)
  Quando um campo é colocado na área Valores do gráfico, um item de legenda é gerado automaticamente contendo o nome desse campo. Cada item de legenda está conectado a uma série individual no gráfico, exceto para gráficos de forma, nos quais a legenda está conectada a pontos de dados individuais em vez de séries individuais.  
  
 Em gráficos de forma, você pode alterar o texto de um item de legenda para mostrar mais informações sobre os pontos de dados individuais. Por exemplo, se você desejar mostrar os valores dos pontos de dados como porcentagens na legenda, poderá usar uma palavra-chave, como **#PERCENT**. É possível adicionar códigos de formato do .NET Framework em conjunto com palavras-chave para aplicar formatos numéricos e de data. Para obter mais informações sobre palavras-chave, consulte [Formatação de pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
 ![Gráfico de sustenido](../../reporting-services/report-design/media/sharpchart.png "sustenido gráfico")  
  
 Em gráficos de não forma, você pode alterar o texto de um item de legenda. Por exemplo, se o nome da série for "Série1", você poderá desejar alterar o texto para algo mais descritivo, como "Vendas de 2008".  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>Para modificar o texto que aparece na legenda em um gráfico de forma  
  
1.  Clique com o botão direito do mouse em uma série ou em um campo na área **Valores** e selecione **Propriedades da Série**.  
  
2.  Clique em **Legenda** e digite uma palavra-chave na caixa **Texto da legenda personalizada** .  
  
 A tabela a seguir fornece exemplos de palavras-chave específicas de gráfico para usar para a propriedade **Texto da Legenda Personalizada**. Para obter mais informações sobre palavras-chave, consulte [Formatação de pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
|Palavra-chave|Description|Exemplo do que é exibido como texto na legenda|  
|-------------|-----------------|---------------------------------------------------|  
|`#PERCENT{P1}`|Exibe a porcentagem do valor total para uma casa decimal.|85.0%|  
|`#VALY`|Exibe o valor numérico real do campo de dados.|17000|  
|`#VALY{C2}`|Exibe o valor numérico real do campo de dados como uma moeda para duas casas decimais.|$17000.00|  
|`#AXISLABEL (#PERCENT{P0})`|Exibe a representação de texto do campo de categoria, seguida pela porcentagem que cada categoria exibe no gráfico.|Michael Blythe (85%)|  
  
> [!NOTE]  
>  A palavra-chave #AXISLABEL pode ser avaliada em tempo de execução quando não há um campo especificado na área **Grupos de Séries** .  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-non-shape-chart"></a>Para modificar o texto que aparece na legenda em um gráfico de não forma  
  
1.  Clique com o botão direito do mouse em uma série ou em um campo na área **Valores** e selecione **Propriedades da Série**.  
  
2.  Clique em **Legenda** e, na caixa **Texto da legenda personalizada** , digite um rótulo para a legenda. A série é atualizada com o texto.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando a legenda em um gráfico de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [Formatando as cores de série em um gráfico de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Ocultar itens de legenda no gráfico &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/chart-legend-hide-items-report-builder.md)  
  
  
