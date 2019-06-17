---
title: Exibir a fórmula para uma série temporal (mineração de dados) do modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43382b5dd8a20de1454bfc3d6a16aa68c99e34a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082594"
---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>Exibir a fórmula para um modelo de série temporal (mineração de dados)
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] inData do Visualizador de série temporal Designer de mineração fornece a maneira mais fácil de exibir os detalhes da equação de regressão usada em um modelo de série temporal.  
  
 Você pode extrair a fórmula de regressão para um modelo de série temporal consultando o conteúdo do modelo. No entanto, para exibir a fórmula ARTXP ou ARIMA completa, recomendamos que você use o **legenda de mineração** da [visualizador MTS](browse-a-model-using-the-microsoft-time-series-viewer.md), que apresenta todas as constantes em um formato legível.  
  
 Se você criar um modelo misto, as análises ARIMA e ARTXP serão criadas em árvores separadas, unidas no nó raiz que representa o modelo. As estruturas das árvores ARIMA e ARTXP são bem diferentes. Por exemplo, a árvore ARTXP na verdade é uma estrutura de árvore, como uma árvore de decisão, enquanto a árvore ARIMA representa uma série de médias móveis. Assim, embora as duas representações estejam presentes em um modelo por conveniência, elas devem ser tratadas como modelos independentes. As equações também são completamente diferentes e não podem ser combinadas ou comparadas.  
  
 Você também pode exibir modelos de série temporal usando o [Microsoft genérico conteúdo Visualizador de árvore](../microsoft-generic-content-tree-viewer-data-mining.md). Para obter mais informações sobre o conteúdo de um modelo de série temporal, consulte [conteúdo do modelo de mineração para modelos de série temporal &#40;Analysis Services - mineração de dados&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>Para exibir a fórmula de regressão ARTXP para um modelo de série temporal  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o modelo de série temporal que você quer exibir e clique em **Procurar**.  
  
     – ou –  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione o modelo de série temporal e clique na guia **Visualizador do Modelo de Mineração** .  
  
2.  Clique na guia **Modelo** .  
  
3.  Se o modelo contiver várias árvores, selecione uma única árvore na lista suspensa **Árvore** .  
  
    > [!NOTE]  
    >  Um modelo sempre terá várias árvores se você tiver mais de uma série de dados. No entanto, você não visualizará tantas árvores no **visualizador MTS** quanto no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](../microsoft-generic-content-tree-viewer-data-mining.md). Isso ocorre porque o visualizador de Série Temporal combina as informações de ARIMA e ARTXP para cada série de dados em uma única representação.  
  
4.  Clique em qualquer nó folha na árvore.  
  
     Nós rotulados como **Série de Dados** sempre são nós folha e podem conter uma equação. Se um nó **(All)** não tiver nenhum nó filho, ele também poderá conter uma equação.  
  
5.  Se a **Legenda de Mineração** não estiver disponível, clique com o botão direito do mouse no nó e selecione **Mostrar Legenda**.  
  
     A fórmula ARTXP é exibida na primeira metade da **Legenda de Mineração**, como a **Equação de nó de árvore**.  
  
### <a name="to-view-the-arima-formula-for-a-time-series-model"></a>Para exibir a fórmula de ARIMA para um modelo de série temporal  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o modelo de série temporal que você quer exibir e clique em **Procurar**.  
  
     – ou –  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione o modelo de série temporal e clique na guia **Visualizador do Modelo de Mineração** .  
  
2.  Clique na guia **Modelo** .  
  
3.  Se o modelo contiver várias árvores, selecione uma única árvore na lista suspensa **Árvore** .  
  
    > [!NOTE]  
    >  O modelo sempre terá várias árvores se você incluir mais de uma série de dados.  
  
4.  Clique em qualquer nó na árvore.  
  
     A fórmula de ARIMA é exibida na segunda metade da **Legenda de Mineração**, como a **Equação ARIMA**.  
  
5.  Se a **Legenda de Mineração** não estiver disponível, clique com o botão direito do mouse no nó e selecione **Mostrar Legenda**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Procurar um modelo usando o Visualizador MTS](browse-a-model-using-the-microsoft-time-series-viewer.md)   
 [Exemplos de consulta de modelos de série temporal](time-series-model-query-examples.md)  
  
  
