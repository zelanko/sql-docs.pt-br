---
title: Guia de rede de dependências (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.dependencynetwork.f1
ms.assetid: e58ce1b7-20d6-42cb-ade5-916da8471e09
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01b3535c7a6c2547bdef9a4f74956ff647f1b864
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279982"
---
# <a name="dependency-network-tab-mining-model-viewer"></a>Guia Rede de Dependências (Visualizador do Modelo de Mineração)
  A guia **Rede de Dependências** provê uma exibição gráfica de todos os atributos que o modelo de mineração contém, e mostra como os atributos estão relacionados.  
  
 A guia **Rede de Dependência**  é usada para vários tipos de modelos de mineração, inclusive modelos de Naïve Bayes, modelos de árvore de decisão e modelos de associação. Para obter mais informações sobre como interpretar o conteúdo da guia **Rede de Dependência**  no contexto destes modelos, consulte os links seguintes:  
  
 [Procurar um modelo usando a Exibição de Árvore da Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
 [Procurar um modelo usando o Visualizador do Microsoft Naive Bayes](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
 [Procurar um modelo usando o Visualizador de Regras de Associação da Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do Visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração a ser exibido, dentre eles na estrutura de mineração atual. O modelo de mineração será aberto em um visualizador personalizado. O tipo de visualizador personalizado que é usado para cada modelo é determinado pelo algoritmo que você usou para criar o modelo.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Para cada modelo, você pode usar o visualizador personalizado fornecido para cada modelo de mineração, ou o Visualizador de Conteúdo de Mineração da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in se houver. O Visualizador de Conteúdo de Mineração da Microsoft pode ser usado com todos os modelos e representa o conteúdo do modelo em uma tabela de HTML.  
  
 **Ampliar**  
 Amplie o diagrama para que você possa ver os atributos com mais detalhes.  
  
 **Reduza a imagem**  
 Reduza o diagrama, para que você possa ver mais atributos e os links entre eles.  
  
 **Copiar exibição de gráfico**  
 Copie a seção visível do diagrama para a área de transferência.  
  
 **Copiar gráfico inteiro**  
 Copie todo o diagrama na área de transferência.  
  
 **Links**  
 Ajuste os links (bordas) e nós exibidos pelo visualizador, regulando o controle deslizante à direita dos atributos. Arrastar a barra de controle deslizante para baixo aumenta o valor de limite, de forma que só os links mais fortes sejam mostrados. Para cada tipo de modelo, um valor ligeiramente diferente é usado para representar os links no gráfico:  
  
-   Em um modelo de **árvore de decisão** , as bordas representam a força preditiva da conexão, determinada em parte pela pontuação de divisão.  
  
-   Em um modelo de **Naïve Bayes** , os links entre dois nós podem ir nas duas direções: ou seja, o nó A pode prever o nó B e vice-versa. A contagem associada com a borda representa a força preditiva da conexão.  
  
-   Em um **modelo de associação**, as bordas entre nós representam a contagem de importância da regra que conecta dois conjuntos de itens.  
  
 Uma regra geral para todos os tipos de modelos é que, quanto mais forte o link, mais forte a relação previsível entre os dois atributos.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do modelo de Mineração de dados](data-mining/data-mining-model-viewers.md)  
  
  
