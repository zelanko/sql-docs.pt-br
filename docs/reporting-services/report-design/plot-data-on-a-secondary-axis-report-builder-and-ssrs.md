---
title: "Plotar dados em um eixo secund&#225;rio (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Plotar dados em um eixo secund&#225;rio (Construtor de Relat&#243;rios e SSRS)
  O gráfico possui dois tipos de eixo: primário e secundário. O eixo secundário é útil ao comparar dois conjuntos de valores com dois intervalos de dados distintos que compartilham uma categoria em comum.  
  
 Por exemplo, suponha que você tenha um gráfico que calcula Receita versus Imposto referente ao ano de 2008. Nesse caso, o período de 2008 é comum para os dois conjuntos de valores. No entanto, quando as duas séries são plotadas no mesmo eixo y, não podemos fazer uma comparação útil porque a escala do eixo y é otimizada para os valores maiores no conjunto de dados. Se mostrarmos Receita no eixo primário, e Imposto no eixo secundário, poderemos exibir cada série em seu próprio eixo y com sua própria escala de valores. A série ainda compartilha um eixo x comum.  
  
 Em situações em que existam mais de duas séries a serem comparadas, considere uma abordagem diferente para comparação e exibição de várias séries em um gráfico. Para obter mais informações, consulte [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Um exemplo deste gráfico está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][Relatórios de exemplo do Construtor de Relatórios e do Designer de Relatórios](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para plotar uma série no eixo secundário  
  
1.  Clique com o botão direito do mouse na série no gráfico ou em um campo na área **Valores** que você deseja exibir no eixo secundário e clique em **Propriedades da Série**. A caixa de diálogo **Propriedades da Série** é exibida.  
  
2.  Clique em **Eixo e Área do Gráfico**e selecione qual dos eixos secundários você deseja habilitar, o eixo de valor ou o eixo de categoria.  
  
## Consulte também  
 [Formatando rótulos dos eixos de um gráfico #40;Construtor de Relatórios e SSRS#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  