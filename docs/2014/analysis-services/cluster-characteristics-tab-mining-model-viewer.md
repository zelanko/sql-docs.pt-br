---
title: Guia características do cluster (Visualizador do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.characteristics.f1
ms.assetid: 8e33ed1d-1ce4-405d-895b-7e995b2c910d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0b4a798f9a395741ae831d3b22fc06a71f55607
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087987"
---
# <a name="cluster-characteristics-tab-mining-model-viewer"></a>Guia Características do Cluster (Visualizador do Modelo de Mineração)
  A guia **Características de Cluster** permite explorar as características de um cluster em um modelo de clustering ou o conjunto de todos os casos no modelo. O gráfico mostra a importância de cada par atributo-valor como uma característica que define o cluster, em comparação com outros clusters.  
  
 **Para obter mais informações:** [Algoritmo MSC](data-mining/microsoft-clustering-algorithm.md), [Procurar um modelo usando o Visualizador de Cluster da Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opções  
 **Atualizar conteúdo do visualizador**  
 Recarregue o modelo de mineração no visualizador.  
  
 **Modelo de mineração**  
 Escolha um modelo de mineração dentre eles na estrutura de mineração atual. O modelo de mineração será aberto no visualizador personalizado.  
  
 **Visualizador**  
 Escolha um visualizador a ser utilizado para explorar o modelo de mineração selecionado. Você pode usar o visualizador personalizado associado a esse tipo de modelo, ou o Visualizador de Conteúdo de Mineração do [!INCLUDE[msCoName](../includes/msconame-md.md)] . Você também pode usar visualizadores de plug-in que estiverem disponíveis.  
  
 **Cluster**  
 Escolha o cluster que você deseja exibir ou escolha **População (Tudo)** para ver a distribuição de atributos para o modelo como um todo.  
  
 **Características do \<cluster>**  
 O gráfico contém as seguintes colunas, que descrevem as características do cluster selecionado.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável**|Lista os atributos do modelo de mineração que são localizados no cluster selecionado.|  
|**Valores**|Lista os valores dos atributos atuais que são localizados no cluster selecionado atualmente.|  
|**Probabilidade**|A barra indica a força do par atributo-valor como um recurso distintivo deste cluster. Se você passar o mouse sobre a barra, poderá ver o valor da probabilidade, representado como uma porcentagem. O que isso indica é, considerando esta combinação de atributo e valor neste caso específico, qual é a probabilidade desse caso pertencer a este cluster.|  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizadores do Modelo de Mineração de Dados](data-mining/data-mining-model-viewers.md)  
  
  
