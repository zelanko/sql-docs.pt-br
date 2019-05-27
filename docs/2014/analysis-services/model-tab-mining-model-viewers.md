---
title: Modelo de guia (visualizadores do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05c0a25ceded07264e4dbe10467e9dc6f093f6c0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077616"
---
# <a name="model-tab-mining-model-viewers"></a>Guia Modelos (Visualizadores do Modelo de Mineração)
  A guia **Modelo** no Visualizador MTS exibe uma representação de uma série temporal como um nó em um gráfico, semelhante aos usados em modelos de árvore de decisão.  
  
 Use esta exibição de um modelo de série temporal para extrair informações úteis sobre a análise de série temporal, inclusive a equação para o gráfico, as condições de ARIMA e os coeficientes.  
  
 **Para obter mais informações:** [Algoritmo MTS](data-mining/microsoft-time-series-algorithm.md), [procurar um modelo usando o visualizador MTS](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), [algoritmo MTS](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibição. O modelo de mineração será aberto no visualizador associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado para este tipo de modelo ou o visualizador de **Árvore de Conteúdo Genérica da Microsoft** . Você também poderá usar visualizadores de plug-in, se houver algum.  
  
 **Ampliar**  
 Amplie a imagem do diagrama.  
  
 **Reduza a imagem**  
 Reduza a imagem do diagrama.  
  
 **Copiar exibição de gráfico**  
 Copie a seção visível do diagrama para a área de transferência.  
  
 **Copiar gráfico inteiro**  
 Copie todo o diagrama na área de transferência.  
  
 **Dimensionar diagrama para ajustar à janela**  
 Reduza o diagrama até que o diagrama inteiro se ajuste na tela.  
  
 **Árvore**  
 Selecione uma árvore da lista suspensa para ser mostrada no visualizador  
  
 Se o modelo de série temporal incluir várias séries, cada série será representada como uma árvore separada. Por exemplo, se você criou previsões com o passar do tempo para [Quantidade] e [Quantidade de Vendas], uma série separada foi criada para cada atributo previsível.  
  
 O comprimento da cor que é realçada na lista indica o número de níveis na árvore. Ou seja, um modelo de série temporal que pode ser representado por um único nó teria uma única equação para descrever a tendência e a barra colorida seria muito curta. (Logicamente, se o modelo for MIXED, o nó conterá uma equação ARIMA e ARTXP.)  
  
 Se a árvore mostrada na lista suspensa tiver uma barra colorida mais longa, isso significará que o modelo tem muitas ramificações na árvore. Ramificar significa que a regressão é mais complexa e o modelo tem que ser quebrado em vários segmentos, com uma equação diferente (ou par de equações) em cada nó.  
  
 **Plano de fundo**  
 Use este controle para selecionar o estado que é representado pela cor do plano de fundo em cada nó.  
  
 **Expansão padrão**  
 Ajuste o número de níveis padrão exibidos para todas as árvores do modelo.  
  
 **Mostrar nível**  
 Altere o número de níveis mostrados na árvore.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
