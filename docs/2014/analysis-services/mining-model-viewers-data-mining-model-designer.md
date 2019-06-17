---
title: Visualizadores do modelo (Designer de modelo de mineração de dados) de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67cd89f4cf857f11f08f69769ff54a22fd83760f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077736"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>Visualizadores do Modelo de Mineração (Designer do Modelo de Mineração de Dados)
  Use a guia **Visualizador do Modelo de Mineração** para explorar os modelos de mineração contidos em uma estrutura de mineração.  
  
 Selecione primeiro o modelo de mineração e, em seguida, selecione um visualizador. Cada modelo tem sempre dois visualizadores disponíveis: um visualizar personalizado, que pode incluir várias guias, e o visualizador genérico.  
  
 Para obter instruções passo a passo sobre como usar cada visualizador, consulte [Visualizadores do modelo de mineração de dados](data-mining/data-mining-model-viewers.md).  
  
## <a name="common-options"></a>Opções comuns  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração para exibir o que está presente na estrutura de mineração atual. O modelo de mineração será aberto primeiro no visualizador personalizado associado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Esta lista contém os visualizadores que o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece para cada modelo de mineração, o Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] e quaisquer visualizadores plug-in.  
  
 O diagrama a seguir mostra um visualizador personalizado e um genérico para o mesmo modelo.  
  
-   O diagrama superior mostra o visualizador para um modelo de mineração baseado no algoritmo MTS. Esse visualizador personalizado específico cria automaticamente um gráfico da série temporal e fornece cinco previsões.  
  
-   O diagrama inferior mostra o mesmo modelo, exibido usando o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Este visualizador apresenta o conteúdo do modelo de mineração de acordo com um esquema padronizado. Para obter mais informações, consulte [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de dados&#41;](microsoft-generic-content-tree-viewer-data-mining.md).  
  
 ![Visão geral do designer de modelo de mineração](media/generic-mining-model-tab1.gif "visão geral do designer de modelo de mineração")  
  
## <a name="viewers-and-their-components"></a>Visualizadores e seus componentes  
 Dependendo do modelo que você selecionar, você verá um visualizador personalizado diferente, adaptado para o algoritmo usado para criar o modelo de mineração de dados selecionado. Cada visualizador personalizado tem uma variedade de ferramentas e caixas de diálogo para ajudar a explorar as estatísticas e os padrões no modelo.  
  
 A lista a seguir descreve as opções em cada visualizador personalizado.  
  
### <a name="microsoft-association-rules-algorithm"></a>Algoritmo Regras de Associação da Microsoft  
  
-   [Procurar um modelo usando o Visualizador de Regras de Associação da Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
    -   [Guia conjuntos de itens &#40;Visualizador do modelo de mineração&#41;](itemsets-tab-mining-model-viewer.md)  
  
    -   [Guia regras &#40;Visualizador do modelo de mineração&#41;](rules-tab-mining-model-viewer.md)  
  
    -   [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](dependency-network-tab-mining-model-viewer.md)  
  
### <a name="microsoft-clustering-algorithm"></a>Algoritmo Microsoft Clustering  
  
-   [Procurar um modelo usando o Visualizador de Cluster da Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
    -   [Guia diagrama de cluster &#40;Visualizador do modelo de mineração&#41;](cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Guia Perfis de cluster &#40;Visualizador do modelo de mineração&#41;](cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Guia características do cluster &#40;Visualizador do modelo de mineração&#41;](cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Guia discriminação de cluster &#40;Visualizador do modelo de mineração&#41;](cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Caixa de diálogo legenda de mineração &#40;Visualizador do modelo de mineração&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-decision-tree-algorithm"></a>Algoritmo Árvore de Decisão da Microsoft  
  
-   [Procurar um modelo usando a Exibição de Árvore da Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
    -   [Guia árvore de decisão &#40;Visualizador do modelo de mineração&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Caixa de diálogo legenda de mineração &#40;Visualizador do modelo de mineração&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-linear-regression-algorithm"></a>Algoritmo Regressão Linear da Microsoft  
  
-   [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Guia árvore de decisão &#40;Visualizador do modelo de mineração&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Caixa de diálogo legenda de mineração &#40;Visualizador do modelo de mineração&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo Regressão Logística da Microsoft  
  
-   [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
### <a name="microsoft-nave-bayes-algorithm"></a>Algoritmo Microsoft Naïve Bayes  
  
-   [Procurar um modelo usando o Visualizador do Microsoft Naive Bayes](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
    -   [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Guia Perfis de atributo &#40;Visualizador do modelo de mineração&#41;](attribute-profiles-tab-mining-model-viewer.md)  
  
    -   [Guia características do atributo &#40;Visualizador do modelo de mineração&#41;](attribute-characteristics-tab-mining-model-viewer.md)  
  
    -   [Guia discriminação de atributo &#40;Visualizador do modelo de mineração&#41;](attribute-discrimination-tab-mining-model-viewer.md)  
  
### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm  
  
-   [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Guia rede de dependências &#40;Visualizador do modelo de mineração&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Rede neural &#40;Visualizador do modelo de mineração&#41;](neural-network-mining-model-viewer.md)  
  
    -   [Localize a caixa de diálogo do nó &#40;Visualizador do modelo de mineração&#41;](find-node-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft Sequence Clustering Algorithm  
  
-   [Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
    -   [Guia diagrama de Cluster de Clustering de sequência &#40;Visualizador do modelo de mineração](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Guia Perfis de Cluster de Clustering de sequência &#40;Visualizador do modelo de mineração](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Guia características do Cluster de Clustering de sequência &#40;Visualizador do modelo de mineração&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Guia discriminação de Cluster de Clustering de sequência &#40;Visualizador do modelo de mineração&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Guia transição de Cluster de Clustering de sequência &#40;Visualizador do modelo de mineração&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)  
  
### <a name="microsoft-time-series-algorithm"></a>Algoritmo MTS  
  
-   [Procurar um modelo usando o Visualizador MTS](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
    -   [Guia de modelo &#40;visualizadores do modelo de mineração&#41;](model-tab-mining-model-viewers.md)  
  
    -   [Guia do gráfico &#40;visualizadores do modelo de mineração&#41;](chart-tab-mining-model-viewers.md)  
  
    -   [Caixa de diálogo legenda de mineração &#40;Visualizador do modelo de mineração&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de modelos de mineração &#40;Designer de modelo de mineração de dados&#41;](mining-models-view-data-mining-model-designer.md)   
 [Exibição de estrutura de mineração &#40;Designer de modelo de mineração de dados&#41;](mining-structure-view-data-mining-model-designer.md)   
 [Designer do gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Construtor de consultas de previsão &#40;mineração de dados&#41;](prediction-query-builder-data-mining.md)  
  
  
