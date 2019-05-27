---
title: Formatar pontos de dados em um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.serieslabelproperties.general.f1
- "10248"
ms.assetid: 08ec3818-f63a-4e89-b52c-750e47f48b85
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d9c0b0a2c6ca3c12ca020dcc79b5aa4cad46c825
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105814"
---
# <a name="formatting-data-points-on-a-chart-report-builder-and-ssrs"></a>Formatando pontos de dados em um gráfico (Construtor de Relatórios e SSRS)
  Ponto de dados é a menor entidade individual no gráfico. Em gráficos sem-forma, os pontos de dados são representados de acordo com seu tipo de gráfico. Por exemplo, uma série de linhas consiste em um ou mais pontos de dados conectados. Em gráficos com forma, os pontos de dados são representados por fatias individuais ou segmentos acrescidos a todo o gráfico. Por exemplo, em um gráfico de pizza, cada pedaço é um ponto de dados. Para obter mais informações, consulte [Tipos de gráficos &#40;Construtor de Relatórios e SSRS&#41;](chart-types-report-builder-and-ssrs.md).  
  
 Um ou mais pontos de dados formam uma série. Por padrão, todas as opções de formatação são aplicadas a todos os pontos de dados na série. Caso queira especificar propriedades para pontos de dados individuais, você pode especificar um campo ou expressão na série que formata um ponto de dados individual em tempo de execução com base no conjunto de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-tooltips-and-drillthrough-actions-to-data-points"></a>Adicionando dicas de ferramenta e ações de detalhamento a pontos de dados  
 É possível adicionar dicas de ferramenta a cada ponto de dados, definindo o valor da propriedade **Dica de Ferramenta** na série. Exibindo dicas de ferramentas, é possível oferecer aos usuários a possibilidade de ver todas as informações relacionadas ao ponto de dados como, por exemplo, o nome do grupo, o valor do ponto de dados e a porcentagem do ponto em relação ao total da série. Para obter mais informações, consulte [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
 Também é possível especificar uma ação de detalhamento para pontos de dados na série a fim de exibir outro relatório ou uma URL. É possível transmitir parâmetros para mostrar informações relacionadas ao ponto de dados clicado. Para obter mais informações, consulte [Adicionar uma ação de detalhamento a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
## <a name="highlighting-individual-data-points-in-a-series"></a>Realçando pontos de dados individuais em uma série  
 Em um gráfico sem forma, é possível realçar pontos de dados individuais, especificando uma expressão para a propriedade Color. Por exemplo, para realçar o maior valor de ponto de dados em uma série chamado `MyField` cuja cor é diferente dos demais pontos de dados, a expressão seria semelhante à seguinte:  
  
 `=Iif(Fields!MyField.Value >= Max(Fields!MyField.Value, "MyDataSet"), "Red", "Green")`  
  
 Nesse exemplo, o maior valor de `MyField` apresentará a cor vermelha e todos os demais pontos de dados, a cor verde. Quando você especifica uma cor para a série usando a propriedade **Preenchimento** na série, o gráfico substitui as cores especificadas na paleta. Para obter mais informações, consulte [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="positioning-data-point-labels-on-a-chart"></a>Posicionando rótulos de ponto de dados em um gráfico  
 Em todos os tipos de gráfico, é possível mostrar rótulos de ponto de dados quando você clica com o botão direito do mouse no gráfico e seleciona **Mostrar Rótulos de Dados**. A posição dos rótulos de ponto de dados é especificada de acordo com o tipo de gráfico:  
  
-   Em um gráfico de barras, é possível reposicionar o rótulo de ponto de dados usando o atributo personalizado **BarLabelStyle** . Há quatro posições possíveis: Externo, Esquerda, Centro e Direita. Quando o estilo do rótulo da barra for definido como Externo, os rótulos serão posicionados fora da barra, desde que caibam na área do gráfico. Caso não possa ser posicionado fora da barra e dentro da área do gráfico, o rótulo é posicionado dentro da barra.  
  
-   Em um gráfico de pizza, é possível reposicionar o rótulo de ponto de dados usando o atributo personalizado **PieLabelStyle** . Há muitas considerações a serem feitas durante o posicionamento dos rótulos de ponto de dados próximos a um gráfico de pizza, inclusive o tipo do gráfico, o espaço disponível entre ele e a legenda correspondente e o tamanho dos rótulos. Para obter mais informações, consulte [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md).  
  
-   Em um gráfico de pirâmide ou de funil, é possível reposicionar os rótulos de ponto de dados usando os atributos personalizados **FunnelLabelStyle** e **PyramidLabelStyle** . Você pode definir esses atributos no painel **Propriedades** quando selecionar um tipo de gráfico de pirâmide ou de funil.  
  
-   Em gráficos empilhados, os rótulos de ponto de dados são sempre posicionados dentro da série e a propriedade **Posição** no rótulo da série é ignorada.  
  
-   Em todos os demais tipos de gráfico, é possível reposicionar o rótulo de ponto de dados usando a propriedade **Posição** no rótulo da série. Por padrão, o gráfico calcula automaticamente a posição dos rótulos de ponto de dados para evitar colisões de rótulo. Quando você definir um valor para **Posição**, todos os rótulos de ponto de dados serão posicionados da mesma forma, o que pode sobrepor os rótulos. Só considere usar essa abordagem quando houver menos pontos de dados.  
  
 Para obter mais informações, consulte [Posicionar rótulos em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](position-labels-in-a-chart-report-builder-and-ssrs.md).  
  
## <a name="adding-keywords-for-data-point-labels-tooltips-and-legend-text"></a>Adicionando palavras-chave a rótulos de ponto de dados, dicas de ferramenta e texto de legenda  
 É possível usar palavras-chave específicas do gráfico, diferenciando maiúsculas de minúsculas, para representar um item existente no gráfico. Essas palavras-chave só são aplicáveis a dicas de ferramenta, texto de legenda personalizado e propriedades de rótulo de ponto de dados. Em muitos casos, uma palavra-chave de gráfico tem uma expressão simples equivalente, mas a palavra-chave é mais rápida e mais fácil de digitar. A seguir, uma lista de palavras-chave de gráfico.  
  
|Palavra-chave de gráfico|Descrição|Aplicável ao tipo de gráfico|Exemplo de uma expressão simples equivalente|  
|-------------------|-----------------|------------------------------|------------------------------------------------|  
|#VALY|Valor Y do ponto de dados.|Todos|`=Fields!MyDataField.Value`|  
|#VALY2|Valor Y número 2 do ponto de dados.|Intervalo, bolha|None|  
|#VALY3|Valor Y número 3 do ponto de dados.|Ações, velas|None|  
|#VALY4|Valor Y número 4 do ponto de dados.|Ações, velas|None|  
|#SERIESNAME|Nome da série.|Todos|None|  
|#LABEL|Rótulo do ponto de dados.|Todos|None|  
|#AXISLABEL|Rótulo do ponto de dados de eixo.|Forma|`=Fields!MyDataField.Value`|  
|#INDEX|Índice do ponto de dados.|Todos|None|  
|#PERCENT|Porcentagem do valor Y do ponto de dados.|Todos|`=FormatPercent(Fields!MyDataField.Value/Sum(Fields!MyDataField.Value, "MyDataSet"),2)`|  
|#TOTAL|Total de todos os valores Y na série.|Todos|`=Sum(Fields!MyDataField.Value)`|  
|#LEGENDTEXT|O texto correspondente ao texto do item de legenda.|Todos|None|  
|#AVG|Média de todos os valores Y na série.|Todos|`=Avg(Fields!MyDataField.Value)`|  
|#MIN|Mínimo de todos os valores Y na série.|Todos|`=Min(Fields!MyDataField.Value)`|  
|#MAX|Máximo de todos os valores Y na série.|Todos|`=Max(Fields!MyDataField.Value)`|  
|#FIRST|Primeiro de todos os valores Y na série.|Todos|`=First(Fields!MyDataField.Value)`|  
  
 Para formatar a palavra-chave, coloque uma cadeia de caracteres de formato [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] entre parênteses. Por exemplo, para especificar o valor do ponto de dados em uma dica de ferramenta como um número com duas casas decimais, coloque a cadeia de caracteres de formato "N2" entre chaves como, por exemplo, "#VALY{N2}" para a propriedade **ToolTip** da série. Para obter mais informações sobre cadeias de caractere de formato do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , consulte [Tipos de formatação](https://go.microsoft.com/fwlink/?LinkId=112024) no MSDN. Para obter mais informações sobre como formatar números em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre como adicionar palavras-chave a um gráfico, consulte [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md), [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](chart-legend-change-item-text-report-builder.md).  
  
## <a name="increasing-readability-in-a-chart-with-multiple-data-points"></a>Aumentando a legibilidade em um gráfico com vários pontos de dados  
 Se houver várias séries no gráfico, talvez isso reduza a legibilidade dos pontos de dados do gráfico. Ao adicionar várias séries ao gráfico, considere usar uma técnica que diferencie as formas de leitura e compreensão de cada uma. Para obter mais informações, consulte [Várias séries em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Para simplificar, quando você estiver usando um gráfico com forma, considere adicionar apenas um campo de dados e um campo de categoria. Para obter mais informações, consulte [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md). Se seu gráfico precisar de mais de um campo de dados e campo de categoria, considere alterar o tipo de gráfico. Você pode clicar com o botão direito do mouse na série e selecionar **Alterar Tipo de Gráfico**.  
  
## <a name="inserting-data-point-markers"></a>Inserindo marcadores de ponto de dados  
 Marcador de ponto de dados é um indicador visual usado para chamar atenção para cada ponto de dados de uma série. Em um gráfico de dispersão, o marcador é usado para determinar a forma e tamanho dos pontos de dados individuais. O tamanho do marcador é especificado com base no tipo de gráfico. É possível alterar o tamanho, a cor ou o estilo do marcador. Os marcadores não estão disponíveis para tipos de gráfico de intervalo ou com forma, ou para qualquer subtipo empilhado.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)  
  
 [Exibir valores percentuais em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um gráfico de pizza ao relatório &#40;Construtor de Relatórios&#41;](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
