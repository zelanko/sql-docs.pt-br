---
title: "Procurar um modelo usando o Visualizador MTS | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mineração de dados [Analysis Services], colunas contínuas"
  - "conteúdo do modelo de mineração, exibindo"
  - "Visualizador MTS"
  - "gráficos [Analysis Services]"
  - "Visualizador MTS [Analysis Services]"
  - "colunas contínuas"
  - "algoritmos de regressão [Analysis Services]"
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 44
---
# Procurar um modelo usando o Visualizador MTS
  O Visualizador Time Series da [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração que são criados com o algoritmo MTS da [!INCLUDE[msCoName](../../includes/msconame-md.md)]. O algoritmo MTS da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de regressão que cria modelos de mineração de dados para previsão de colunas contínuas, tais como vendas de produtos, em um cenário de previsão. Esses modelos de série temporal podem incluir informações baseadas em diferentes algoritmos:  
  
-   O algoritmo ARTxp foi otimizado para previsão a curto prazo.  
  
-   O algoritmo ARIMA foi otimizado para previsão a longo prazo.  
  
-   Uma combinação dos algoritmos ARTxp e ARIMA.  
  
 Para obter mais informações sobre esses algoritmos, consulte [Algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm.md) e [Referência técnica do algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
> [!NOTE]  
>  Para exibir informações detalhadas sobre as equações usadas no modelo e os padrões identificados, use o Visualizador de Árvore de Conteúdo Genérica da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md).  
  
##  <a name="BKMK_ViewerTabs"></a> Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador MTS da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece as seguintes guias:  
  
-   [Modelo](#BKMK_Tree)  
  
-   [Gráficos](#BKMK_Charts)  
  
 **Observação** As informações indicadas para o conteúdo do modelo e na Legenda de Mineração dependem do algoritmo usado pelo modelo. Porém, as guias **Modelo** e **Gráficos** são as mesmas, independentemente da combinação de algoritmos.  
  
###  <a name="BKMK_Tree"></a> Modelo  
 Quando um modelo de série temporal é criado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] apresenta o modelo concluído como uma árvore. Se seus dados tiverem várias séries de casos, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] criará uma árvore separada para cada série. Por exemplo, você está prevendo vendas para o Pacífico, América do Norte e regiões da Europa. As previsões para cada uma destas regiões são série de caso. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria uma árvore separada para cada uma destas séries. Para exibir uma série específica, selecione-a na lista **Árvore**.  
  
 Para cada árvore, o modelo de série temporal contém um nó **Todos** e, depois, se divide em vários nós que representam estruturas periódicas identificadas pelo algoritmo. Você pode clicar em cada nó para exibir estatísticas tais como o número de casos e a equação.  
  
 Se você criou o modelo usando somente ARTxp, a **Legenda de Mineração** do nó raiz conterá apenas o número total de casos. Para cada nó não raiz, a **Legenda de Mineração** tem informações mais detalhadas sobre a divisão da árvore: por exemplo, ela pode mostrar a equação do nó e o número de casos. A *regra* na legenda contém informações que identificam a série e o tempo durante o qual ela se aplica. Por exemplo, o texto de legenda `M200 Europe Amount -2` indica que o nó representa o modelo da série M200 Europe, durante um período de duas frações de tempo atrás.  
  
 Se você criou o modelo usando somente ARIMA, a guia **Modelo** terá um único nó com a legenda **Todos**. A **Legenda de Mineração** do nó raiz contém a equação ARIMA.  
  
 Se criar um modelo misto, o nó raiz conterá apenas o número de casos e a equação ARIMA. Depois do nó de raiz, a árvore se divide em nós separados para cada estrutura periódica. Para cada nó não raiz, a Legenda de Mineração contém algoritmos ARTxp e ARIMA, a equação para o nó e o número de casos no nó. A equação do ARTxp é listada primeiro e rotulada como a equação de nó de árvore. Isto é seguido pela equação de ARIMA. Para obter mais informações sobre como interpretar essas informações, consulte [Referência técnica do algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 De modo geral, o gráfico da árvore de decisão mostra a divisão mais importante, o nó **Todos**, à esquerda do visualizador. Nas árvores de decisão, a divisão após o nó **Todos** é a mais importante pois contém a condição que separa, com mais ênfase, os casos nos dados de treinamento. Em um modelo de série temporal, a ramificação principal indica o ciclo sazonal mais provável. Divisões após o nó **Todos** são exibidas à direita da ramificação.  
  
 É possível expandir ou recolher os nós individuais na árvore para mostrar ou ocultar as divisões que ocorrem após cada nó. Também é possível usar as opções na guia **Árvore de Decisão** para interferir na maneira de exibição da árvore. Use o controle deslizante **Mostrar Nível** para ajustar o número de níveis exibidos na árvore. Use a opção **Expansão Padrão** para definir o número padrão de níveis exibidos em todas as árvores no modelo.  
  
 O sombreamento da cor de fundo de cada nó equivale ao número de casos localizados no nó. Para saber o número exato de casos no nó, coloque o ponteiro sobre o nó para exibir uma InfoDica para o nó.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> Gráficos  
 A guia **Gráficos** exibe o gráfico que mostra o comportamento do atributo previsto ao longo do tempo, junto com cinco valores de previsão futuros. O eixo vertical do gráfico representa o valor da série e o eixo horizontal representa o tempo.  
  
> [!NOTE]  
>  As frações de tempo usadas no eixo de tempo dependem das unidades utilizadas nos seus dados: elas podem representar dias, meses ou até mesmo segundos.  
  
 Use o botão **Abs** para alternar entre curvas absolutas e relativas. Se seu gráfico tiver vários modelos, a escala dos dados para cada modelo poderá ser muito diferente. Se você usar uma curva absoluta, um modelo poderá ser exibido como uma linha reta, enquanto que outro mostrará alterações significativas. Isso ocorre porque a escala de um modelo é maior que a escala do outro modelo. Alternando para uma curva relativa, você altera a escala para mostrar a porcentagem de alteração em vez de valores absolutos. Isso facilita a comparação dos modelos baseados em escalas diferentes  
  
 Se o modelo de mineração tiver várias séries temporais, você poderá selecionar uma ou várias séries para serem exibidas no gráfico. Basta clicar na lista à direita do visualizador e selecionar as séries desejadas. Se o gráfico tornar-se muito complexo, é possível filtrar as séries exibidas marcando ou desmarcando as caixas de seleção das séries na legenda.  
  
 O gráfico exibe dados históricos e futuros. Os dados futuros aparecem sombreados, para diferenciá-los dos dados históricos. Os valores dos dados aparecem como linhas sólidas para dados históricos e como linhas pontilhadas para previsões. Você pode alterar a cor das linhas usadas para cada série ao definir propriedades no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Alterar as cores usadas no Visualizador de mineração de dados](../../analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md).  
  
 Você pode ajustar o intervalo de tempo exibido usando as opções de zoom. Pode também exibir um intervalo de tempo específico clicando no gráfico, arrastando uma seleção de tempo pelo gráfico e clicando novamente para ampliar o intervalo selecionado.  
  
 Você pode selecionar quantas **etapas** de tempo futuras deseja exibir no modelo usando as **Etapas de Previsão**. Se você marcar a caixa de seleção **Mostrar Desvios**, o visualizador fornecerá barras de erro para que seja possível verificar a exatidão do valor previsto.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
## Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Exemplos de consulta de um modelo de série temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Visualizadores do Modelo de Mineração de Dados](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  