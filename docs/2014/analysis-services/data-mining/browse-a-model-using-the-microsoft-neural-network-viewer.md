---
title: Procurar um modelo usando o Visualizador de rede Neural da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
- classification mining model [Analysis Services]
- Microsoft Neural Network Viewer
- regression algorithms [Analysis Services]
- Neural Network Viewer [Analysis Services]
- neural network model [Analysis Services]
ms.assetid: 2343d746-c4f4-499b-9d3c-17d63310a9a3
caps.latest.revision: 42
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45561d4e2b5463e6525d9def3cf0d508fddd592f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196666"
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>Procurar um modelo usando o Visualizador de Rede Neural da Microsoft
  O Visualizador de Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exibe modelos de mineração criados com o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O algoritmo de Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] cria modelos de mineração para classificação e regressão que podem analisar várias entradas e saídas, e é muito útil para análises abertas e exploração. Para obter mais informações sobre esse algoritmo, consulte [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md).  
  
 Ao explorar um modelo usando o Visualizador de Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , você costuma obter um atributo e um estado de destino e, depois, usa o visualizador para ver como os atributos de entrada afetam o resultado  
  
 Por exemplo, digamos que você conheça estes fatos sobre uma classe de clientes em potencial:  
  
-   Meia idade (entre 40 e 50 anos de idade).  
  
-   Tem casa própria.  
  
-   Tem dois filhos que ainda moram em casa.  
  
 Como correlacionar estes atributos à probabilidade de que o cliente faça uma compra?  
  
 Criando um modelo de rede neural usando o comportamento de compra como o resultado final, você pode explorar várias combinações em atributos de clientes, como renda alta, e descobrir como a combinação de atributos tem maior probabilidade de influenciar o comportamento de compra. Por exemplo, talvez você descubra que o fator determinante é a distância percorrida por eles até o trabalho.  
  
 Se precisar obter mais informações detalhadas de exibição, como as equações que representam cada padrão descoberto, você poderá alternar exibições e usar o Visualizador de Árvores de Conteúdo Genérico da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) ou [Visualizador de Árvore de Conteúdo Genérica da Microsoft &#40;Mineração de Dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Guias do Visualizador  
 Quando você navega em um modelo de mineração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ele é exibido na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados no visualizador adequado ao modelo. O Visualizador de Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece as seguintes guias para uso na exploração de modelos de mineração de rede neural:  
  
-   [Entradas](#BKMK_Inputs)  
  
-   [Saídas](#BKMK_Outputs)  
  
-   [Variáveis](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> Entradas  
 Use a guia **Entradas** para escolher os atributos e valores usados pelo modelo como entradas. Por padrão, o visualizador é aberto com todos os atributos incluídos. Nesta exibição padrão, o modelo escolhe os valores de atributo mais importantes para exibição.  
  
 Para selecionar um atributo de entrada, clique dentro da coluna **Atributo** da grade **Entrada** e selecione um atributo na lista suspensa. (Somente os atributos incluídos no modelo são incluídos na lista.)  
  
 O primeiro valor específico é exibido na coluna **Valor** . Quando você clica no valor padrão, uma lista com todos os possíveis estados do atributo associado é exibida. Você pode selecionar o estado que deseja verificar. É possível selecionar quantos atributos desejar.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> Saídas  
 Use a guia **Saídas** para escolher o atributo de resultado a ser investigado. Você pode escolher dois estados de resultado a serem comparados, assumindo que as colunas foram definidas como atributos previsíveis quando o modelo foi criado.  
  
 Use a lista **OutputAttribute** para selecionar um atributo. Você pode selecionar dois estados associados ao atributo nas listas **Valor 1** e **Valor 2** . Esses dois estados do atributo de saída serão comparados no painel **Variáveis** .  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Variáveis  
 A grade na guia **Variáveis** contém as seguintes colunas: **Atributo**, **Valor**, **Preferências [valor 1]** e **Preferências [valor 2]**. Por padrão, as colunas são classificadas pela força de **Preferências [valor 1]**. Clicar no cabeçalho de uma coluna altera a ordem de classificação para a coluna selecionada.  
  
 Uma barra à direita do atributo mostra qual estado do atributo de saída o estado atributo de entrada especificado prefere. O tamanho da barra mostra como o estado de saída favorece significativamente o estado de entrada.  
  
 [Voltar ao Início](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo rede Neural da Microsoft](microsoft-neural-network-algorithm.md)   
 [Tarefas do Visualizador do modelo e instruções de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Tarefas do Visualizador do modelo e instruções de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining-model-viewers.md)  
  
  
