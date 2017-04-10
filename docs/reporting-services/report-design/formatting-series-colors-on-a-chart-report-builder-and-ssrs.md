---
title: "Formatando as cores da s&#233;rie em um gr&#225;fico (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10245"
  - "10252"
  - "sql13.rtp.rptdesigner.serieslabelproperties.borders.f1"
  - "sql13.rtp.rptdesigner.seriesproperties.borders.f1"
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Formatando as cores da s&#233;rie em um gr&#225;fico (Construtor de Relat&#243;rios e SSRS)
  O Reporting Services fornece várias paletas internas para gráficos. Além disso, você pode definir uma paleta personalizada. Por padrão, os gráficos usam a paleta de cores interna **Pacífico** para preencher cada série. Essas cores também aparecem na legenda. Se forem adicionadas várias séries ao gráfico, ele atribuirá um cor à série na ordem em que as cores foram definidas na paleta.  
  
 Se houver mais séries que o número de cores da paleta, o gráfico começará a reutilizar as cores, ou seja, poderão existir duas séries com a mesma cor. Isso ocorrerá frequentemente se você estiver usando um gráfico de Forma, no qual a cada ponto de dados é atribuído uma cor da paleta. Para evitar confusão, defina uma paleta personalizada que tenha, no mínimo, o mesmo número de cores que o número de séries do gráfico.  
  
 Você pode selecionar uma paleta nova ou definir uma paleta personalizada no painel Propriedades. Para obter mais informações, consulte [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Usando paletas internas  
 O Reporting Services fornece uma lista de paletas internas predefinidas que você pode usar para definir um conjunto de cores para as séries do gráfico. Todas as paletas internas contêm entre 10 e 16 valores de cor. Não é possível estender a paleta interna para incluir mais cores, portanto, se você precisar de mais de 16 cores, defina uma paleta personalizada.  
  
 Se você estiver imprimindo um relatório, considere o uso de uma paleta **Escala de cinza**. Essa paleta usa tons de preto e branco para representar cada série de um gráfico.  
  
 A paleta nomeada Padrão foi usada como a paleta de gráfico padrão nas versões anteriores do Reporting Services. Ela foi preservada com o mesmo nome para manter a consistência. A atualização dos gráficos será consistente usando a paleta Padrão, mas, após a atualização, considere alterá-la.  
  
## Usando paletas personalizadas  
 Para aplicar suas próprias cores ao gráfico, use uma paleta personalizada. Uma paleta personalizada permite que você adicione suas próprias cores na ordem que quiser que elas apareçam no gráfico. Uma paleta personalizada será especialmente útil se o número de séries do gráfico for desconhecido no momento da criação. Para obter mais informações, consulte [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
## Usando uma cor preenchimento em cada série  
 Você também pode definir suas próprias cores no gráfico especificando uma cor para cada série no gráfico. Para isso, abra a caixa de diálogo **Propriedades da Série** e defina a propriedade **Cor** para **Preenchimento**. Essa abordagem anulará todas as paletas definidas. Geralmente, é melhor usar uma paleta personalizada para definir suas próprias cores porque o número de séries no conjunto de dados pode ser desconhecido até o processamento do relatório.  
  
 Essa abordagem é a mais adequada se você desejar definir a cor das séries condicionalmente com base em uma expressão.  Para obter mais informações, consulte [Formatação de pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## Nesta seção  
 [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md))  
  
 [Realçar dados do gráfico adicionando faixas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## Consulte também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Adicionar estilos de bisel, relevo e textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-bevel-emboss-and-texture-styles-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)  
  
  