---
title: Procurando um modelo de previsão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- forecasting [data mining]
- mining models, viewing
- mining model, time series
- time series [data mining]
ms.assetid: ad35a528-1949-4048-8678-3b9760c1c88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 830aea002e8000feeda061f42af9084696ed6fe8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088487"
---
# <a name="browsing-a-forecasting-model"></a>Procurando um modelo de previsão
  Quando você abre um modelo de previsão usando **navegue**, o modelo é exibido em um visualizador interativo, semelhante ao Visualizador de modelo de série de tempo no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O visualizador ajuda a explorar tendências, comparar séries, criar previsões e obter informações sobre o modelo e os dados subjacentes.  
  
##  <a name="bkmk_Top"></a> Explorar o modelo  
 O **procurar** visualizador para modelos de previsão fornece uma exibição de gráfico, que mostra as tendências ao longo do tempo e permite criar previsões e uma exibição de modelo, que representa a série de tempo como uma árvore de decisão ou uma árvore de regressão.  
  
-   [Modo de exibição de gráfico](#bkmk_charts)  
  
-   [Exibição de modelo](#bkmk_Model)  
  
 Para fazer experiências com um modelo de previsão, você pode usar os dados de exemplo na guia previsão da pasta de trabalho de dados de exemplo e criar um modelo de série temporal usando o [Assistente de previsão &#40;Data Mining Add-ins para Excel&#41; ](forecast-wizard-data-mining-add-ins-for-excel.md) em que o  **Data Mining** faixa de opções, ou [previsão &#40;ferramentas de análise de tabela para Excel&#41; ](forecast-table-analysis-tools-for-excel.md) no **analisar** faixa de opções.  
  
###  <a name="bkmk_charts"></a> Gráfico  
 O **gráfico** guia exibe a tendência da série de dados ao longo do tempo, junto com os valores previstos. O eixo vertical do gráfico representa os valores da série e o eixo horizontal representa o tempo.  
  
##### <a name="explore-the-forecasting-chart"></a>Explorar o gráfico de previsão  
  
1.  Este modelo contém várias séries temporais, mas para simplificar o gráfico, você poderá exibir uma única série ou algumas séries relacionadas.  
  
     ![previsões históricas no modelo de previsão](media/dm13-forecast-chart-historicpredictions.gif "previsões históricas no modelo de previsão")  
  
     Use as caixas de seleção para selecionar a previsão apenas para América do Norte e apenas para Valor de vendas.  
  
2.  Clique em **etapas de previsão** e digite um novo valor para controlar a hora futura quantos valores você deseja ver no gráfico.  
  
     O padrão é 5.  
  
3.  Clique em qualquer ponto na linha, histórica ou futura, para ver os valores exatos para esse ponto no tempo, exibidos na **legenda de mineração**.  
  
4.  O gráfico exibe dados históricos e futuros. Observe a linha pontilhada, com um plano de fundo sombreado. Esses valores são as previsões futuras, com base no modelo.  
  
     Os dados históricos (usados para criar o modelo) são mostrados no lado esquerdo do gráfico.  
  
5.  Selecione o **Mostrar previsões históricas** opção para ter uma noção a estabilidade da série temporal.  
  
     ![previsões para uma única série no modelo](media/dm13-forecast-chart-singleseries.gif "previsões para uma única série no modelo")  
  
     As previsões históricas são valores previstos com base nas séries para esse ponto, que são comparadas com os valores reais históricos. Se a linha pontilhada (com os valores previstos) estiver muito distante da linha sólida (os valores reais), isso significará que a primeira parte da série talvez não exatamente preveja os valores posteriores. Você poderá precisar de mais dados ou isso pode apenas ser um indicador de volatilidade no ciclo.  
  
6.  Selecione o **Mostrar desvios** opção para exibir barras de erro no gráfico.  
  
     As barras de erro permitem avaliar visualmente a variação das previsões. A qualidade das previsões varia dependendo dos seus dados de origem, mas, à medida que você aumenta o número de etapas de previsão, deverá ver os desvios aumentarem continuamente.  
  
 **Dicas**  
  
-   Para alternar a exibição do **legenda de mineração**, clique em qualquer ponto no gráfico.  
  
     É possível exibir um intervalo de tempo específico clicando no gráfico, arrastando uma seleção de tempo pelo gráfico e clicando novamente para ampliar o intervalo selecionado.  
  
-   Para obter uma cópia do gráfico atual, clique em **copiar para Excel**, em seguida, clique em uma planilha do Excel. Um gráfico é inserido na planilha usando todas as opções que você tiver definido, incluindo uma legenda.  
  
     No entanto, este gráfico é estático para que você não pode editar a legenda ou exibir os dados subjacentes; Se você precisar de uma exibição de gráfico mais interativa, use o [visualizadores do Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
-   Clique em **Abs** na barra de menus do visualizador para alternar entre curvas absolutas e relativas.  
  
     Essa opção será útil se seu gráfico tiver vários modelos, mas a escala dos dados para cada modelo será muito diferente.  
  
     Por exemplo, se as lojas da região do Pacífico forem novas e as vendas estiverem baixas, e se os valores absolutos estiverem sendo usados, a linha que mostra as vendas do Pacífico poderá aparecer inalterada, dificultando a visualização das alterações reais, enquanto os outros modelos serão exibidos em uma escala mais comum.  
  
     Ao alternar a exibição para usar valores relativos, você poderá normalizar a escala de modelos diferentes e exibir diferenças como uma porcentagem de alteração. Quando a alteração é referente a cada modelo, ela pode ser exibida no mesmo gráfico sem distorção significativa.  
  
 [Explorar o modelo](#bkmk_Top)  
  
###  <a name="bkmk_Model"></a> Modelo  
 Um modelo de previsão também pode ser representado como uma árvore de decisão ou, se a série for predominantemente linear, um modelo de regressão.  
  
 Por exemplo, neste modelo, há uma diferença na fórmula de regressão com base em uma determinada condição, para que a árvore seja dividida em duas ramificações, cada uma com uma fórmula de regressão diferente.  
  
 ![Filtrar série única no modelo de previsão](media/dm13-forecast-model-northamerica.gif "Filtrar série única no modelo de previsão")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>Explorar o modelo de previsão como uma árvore  
  
1.  Clique o **árvore** lista suspensa lista e escolha um modelo para exibir.  
  
     Uma árvore separada ou nó de regressão é exibido para cada atributo previsível. Por exemplo, se seus dados contiverem vendas para Europa, América do Norte e Pacífico, haverá três modelos diferentes, um para cada série de dados.  
  
2.  Arraste o **Mostrar nível** controle deslizante para filtrar níveis inferiores da árvore e se concentrar em divisões mais importantes.  
  
3.  Clique em cada nó para exibir algumas estatísticas descritivas na **legenda de mineração**.  
  
     Quando você coloca o cursor do mouse sobre um nó, uma Dica de Ferramenta também exibe as mesmas estatísticas, bem como a fórmula completa que descreve esse nó.  
  
4.  Se você quiser copiar as informações na **legenda de mineração**, clique com botão direito do **legenda de mineração**, selecione **cópia**e clique dentro de sua planilha do Excel. O **copiar para Excel** opção copia o gráfico, não as estatísticas.  
  
 [Explorar o modelo](#bkmk_Top)  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
