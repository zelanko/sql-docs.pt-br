---
title: Métodos de discretização (mineração de dados) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20a6d7fcef0bd82f44f49d01bb717ef15cdc2c53
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="discretization-methods-data-mining"></a>Métodos de discretização (mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Alguns algoritmos usados para criar modelos de mineração de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] precisam de tipos de conteúdo específicos para que funcionem corretamente. Por exemplo, o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes não pode usar colunas contínuas como entrada nem prever valores contínuos. Além disso, algumas colunas podem conter tantos valores que o algoritmo não pode identificar facilmente os padrões interessantes nos dados dos quais criar um modelo.  
  
 Nesses casos, é possível discretizar os dados nas colunas de modo a permitir o uso dos algoritmos para produzir um modelo de mineração. *Discretização* é o processo de colocar valores em buckets de modo que haja um número limitado de possíveis estados. Os próprios blocos são tratados como valores ordenados e discretos. Você pode discretizar tanto as colunas numéricos quanto as colunas de cadeia de caracteres.  
  
 Há vários métodos que você pode usar para discretizar dados. Se sua solução de mineração de dados usar dados relacionais, será possível controlar o número de buckets usados para agrupamento de dados com a definição do valor da propriedade <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> . O número padrão de recipientes é 5.  
  
 Se sua solução de mineração de dados usar dados de um cubo OLAP (Processamento Analítico Online), o algoritmo de mineração de dados calculará automaticamente o número de buckets a serem gerados usando a seguinte equação, em que n é o número de valores distintos de dados na coluna:  
  
 `Number of Buckets = sqrt(n)`  
  
 Se você não quiser que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcule o número de buckets, será possível usar a propriedade <xref:Microsoft.AnalysisServices.DimensionAttribute.DiscretizationBucketCount%2A> para especificar isso manualmente.  
  
 A tabela a seguir descreve os métodos que podem ser usados para discretizar os dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método de discretização|Description|  
|---------------------------|-----------------|  
|**AUTOMATIC**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina o método de discretização a ser usado.|  
|**CLUSTERS**|O algoritmo divide os dados em grupos por meio de amostragem dos dados de treinamento, inicializando um número aleatório de pontos e em seguida executando várias interações do algoritmo Microsoft Clustering usando o método de clustering Expectation Maximization (EM). O método **CLUSTERS** é útil pois trabalha em qualquer curva de distribuição. Porém, requer mais tempo de processamento que os demais métodos de discretização.<br /><br /> Esse método pode ser usado apenas com colunas numéricas.|  
|**EQUAL_AREAS**|O algoritmo divide os dados em grupos que contenham um número igual de valores. Esse método é usado mais na distribuição normal das curvas, mas não funciona corretamente se a distribuição incluir um grande número de valores que ocorre em um grupo estreito em dados contínuos. Por exemplo, se a metade dos itens tiver um custo zero, a metade dos dados ocorrerá em um único ponto na curva. Nessa distribuição, o método quebra os dados em uma tentativa de estabelecer uma discretização igual em várias áreas. Isso produz uma representação inexata dos dados.|  
  
## <a name="remarks"></a>Remarks  
  
-   Você pode usar o método **EQUAL_AREAS** para discretizar cadeias de caracteres.  
  
-   O método **CLUSTERS** usa um exemplo aleatório de 1000 registros para discretizar os dados. Use o método **EQUAL_AREAS** se não quiser que o algoritmo realize a amostragem dos dados.  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo tipos & #40; mineração de dados & #41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Conteúdo tipos & #40; DMX & #41;](../../dmx/content-types-dmx.md)   
 [Algoritmos de mineração de dados e &#40; Analysis Services – Data Mining e &#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Estruturas de mineração & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tipos de dados & #40; mineração de dados & #41;](../../analysis-services/data-mining/data-types-data-mining.md)   
 [Colunas de estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)   
 [Distribuições de colunas &#40;Mineração de dados&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md)  
  
  
