---
title: "Exibir a f&#243;rmula para um modelo de s&#233;rie temporal (minera&#231;&#227;o de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mineração de dados [Analysis Services], tópicos de instruções"
  - "ARTXP"
  - "algoritmos de série temporal [Analysis Services]"
  - "ARIMA"
  - "série temporal [Analysis Services]"
  - "Visualizador MTS [Analysis Services]"
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 14
---
# Exibir a f&#243;rmula para um modelo de s&#233;rie temporal (minera&#231;&#227;o de dados)
  Se você tiver criado um modelo de série temporal usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining, a maneira mais fácil de ver a equação de regressão para o modelo será usar a **Legenda de Mineração** do [Visualizador MTS](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), que apresenta todas as constantes em um formato legível.  
  
### Para exibir a fórmula de regressão ARTXP para um modelo de série temporal  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o modelo de série temporal que você quer exibir e clique em **Procurar**.  
  
     – ou –  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione o modelo de série temporal e clique na guia **Visualizador do Modelo de Mineração** .  
  
2.  Clique na guia **Modelo** .  
  
3.  Se o modelo contiver várias árvores, selecione uma única árvore na lista suspensa **Árvore**.  
  
    > [!NOTE]  
    >  Um modelo sempre terá várias árvores se você tiver mais de uma série de dados. No entanto, você não visualizará tantas árvores no **visualizador MTS** quanto no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md). Isso ocorre porque o visualizador de Série Temporal combina as informações de ARIMA e ARTXP para cada série de dados em uma única representação.  
  
4.  Clique em qualquer nó folha na árvore.  
  
     Nós rotulados como **Série de Dados** sempre são nós folha e podem conter uma equação. Se um nó **(All)** não tiver nenhum nó filho, ele também poderá conter uma equação.  
  
5.  Se a **Legenda de Mineração** não estiver disponível, clique com o botão direito do mouse no nó e selecione **Mostrar Legenda**.  
  
     A fórmula ARTXP é exibida na primeira metade da **Legenda de Mineração**, como a **Equação de nó de árvore**.  
  
     ![viewing the time series formula in the legend](../../analysis-services/data-mining/media/ssdm-timeserieslegend.png "viewing the time series formula in the legend")  
  
### Para exibir a fórmula de ARIMA para um modelo de série temporal  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o modelo de série temporal que você quer exibir e clique em **Procurar**.  
  
     – ou –  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione o modelo de série temporal e clique na guia **Visualizador do Modelo de Mineração** .  
  
2.  Clique na guia **Modelo** .  
  
3.  Se o modelo contiver várias árvores, selecione uma única árvore na lista suspensa **Árvore**.  
  
    > [!NOTE]  
    >  O modelo sempre terá várias árvores se você incluir mais de uma série de dados.  
  
4.  Clique em qualquer nó na árvore.  
  
     A fórmula de ARIMA é exibida na segunda metade da **Legenda de Mineração**, como a **Equação ARIMA**.  
  
5.  Se a **Legenda de Mineração** não estiver disponível, clique com o botão direito do mouse no nó e selecione **Mostrar Legenda**.  
  
### Para obter os coeficientes e termos da equação  
  
1.  Você também pode obter os termos e os coeficientes da fórmula de regressão para um modelo de série temporal criando uma **consulta de conteúdo** no conteúdo do modelo.  
  
     Para obter mais informações, consulte [Exemplos de consulta de um modelo de série temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)  
  
2.  Você também pode procurar modelos de série temporal e encontrar os termos e os coeficientes usando o [Visualizador de Árvore de Conteúdo Genérica da Microsoft](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md).  
  
     Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de série temporal &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
    > [!NOTE]  
    >  Se você procurar o conteúdo de um modelo misto que use ambos os modelos ARIMA e ARTXP, os dois modelos estarão em árvores separadas e unidas no nó raiz que representa o modelo. Embora os modelos ARIMA e ARTXP sejam apresentados em um visualizador para sua conveniência, as estruturas são muito diferentes, assim como as equações, que não podem ser combinadas ou comparadas. A árvore ARTXP na verdade é mais como uma árvore de decisão, enquanto a árvore ARIMA representa uma série de médias móveis.  
  
## Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Procurar um modelo usando o Visualizador MTS](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
  