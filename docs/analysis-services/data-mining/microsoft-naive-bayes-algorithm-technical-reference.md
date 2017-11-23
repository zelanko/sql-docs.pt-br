---
title: "Referência técnica do Microsoft Naive Bayes algoritmo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MINIMUM_DEPENDENCY_PROBABILITY parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
ms.assetid: a4cd47fe-2127-4930-b18f-3edd17ee9a65
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 812ca4b26ed14645bbd84094077f24f44d8784cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-naive-bayes-algorithm-technical-reference"></a>Referência técnica do algoritmo Microsoft Naive Bayes
  O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo de classificação fornecido pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para uso em modelagem de previsão. O algoritmo calcula a probabilidade condicional entre as colunas de entrada e as previsíveis e assume que as colunas são independentes. Esta pressuposição de independência leva ao nome Naive Bayes.  
  
## <a name="implementation-of-the-microsoft-naive-bayes-algorithm"></a>Implementação do algoritmo Naive Bayes da Microsoft  
 Esse algoritmo é computacionalmente menos intenso de que outros algoritmos da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e, portanto, é útil para gerar modelos de mineração rapidamente para descobrir as relações entre as colunas de entrada e as colunas previsíveis. O algoritmo considera cada par de valores de atributo de entrada e valores de atributo de saída.  
  
 Uma descrição das propriedades matemáticas do Teorema de Bayes está além do escopo desta documentação; para obter mais informações, consulte o documento da Microsoft Research denominado [Learning Bayesian Networks: The Combination of Knowledge and Statistical Data](http://go.microsoft.com/fwlink/?LinkId=207029) (Aprendendo sobre redes Bayesianas: a combinação de dados de conhecimento e estatísticos).  
  
 Para obter uma descrição de como são ajustadas as probabilidades em todos os modelos para considerar valores ausentes, consulte [Valores ausentes &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
### <a name="feature-selection"></a>Seleção de recursos  
 O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] executa a seleção de recursos automática para limitar o número de valores considerados durante a criação do modelo. Para obter mais informações, consulte [Seleção de recursos &#40;Mineração de Dados&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md).  
  
|Algoritmo|Método de análise|Comentários|  
|---------------|------------------------|--------------|  
|Naive Bayes|entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Naive Bayes aceita somente atributos discretos ou diferenciados; portanto, não pode usar a pontuação de interesse.|  
  
 O algoritmo foi projetado para minimizar o tempo de processamento e selecionar com eficiência os atributos que têm a maior importância; no entanto, você pode controlar os dados usados pelo algoritmo definindo parâmetros da seguinte forma:  
  
-   Para limitar os valores usados como entradas, diminua o valor de MAXIMUM_INPUT_ATTRIBUTES.  
  
-   Para limitar o número de atributos analisados pelo modelo, diminua o valor de MAXIMUM_OUTPUT_ATTRIBUTES.  
  
-   Para limitar o número de valores que podem ser considerados para qualquer atributo, diminua o valor de MINIMUM_STATES.  
  
## <a name="customizing-the-naive-bayes-algorithm"></a>Personalizando o algoritmo Naive Bayes  
 O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] tem suporte para vários parâmetros que afetam o comportamento, o desempenho e precisão do modelo de mineração resultante. Também é possível definir sinalizadores de modelagem nas colunas de modelo para controlar o modo como os dados são processados ou definir sinalizadores na estrutura de mineração para especificar como valores ausentes ou nulos devem ser manipulados.  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] tem suporte para vários parâmetros que afetam o desempenho e exatidão do modelo de mineração resultante. A tabela a seguir descreve cada parâmetro.  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Especifica o número máximo de atributos de entrada que o algoritmo pode manipular antes de invocar a seleção de recurso. Definir esse valor como 0 desabilita a seleção do recurso para os atributos de entrada.  
  
 O padrão é 255.  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Define o número máximo de atributos de saída que o algoritmo pode manipular antes de invocar a seleção de recurso. Definir esse valor como 0 desabilita a seleção do recurso para os atributos de saída.  
  
 O padrão é 255.  
  
 *MINIMUM_DEPENDENCY_PROBABILITY*  
 Especifica a probabilidade mínima de dependência entre os atributos de entrada e de saída. Esse valor é usado para limitar o tamanho do conteúdo gerado pelo algoritmo. Essa propriedade pode ser definida de 0 a 1. Valores maiores reduzem o número de atributos no conteúdo do modelo.  
  
 O padrão é 0,5.  
  
 *MAXIMUM_STATES*  
 Especifica o número máximo de estados de atributo para os quais o algoritmo dá suporte. Se o número de estados que um atributo tiver for maior do que o número máximo de estados, o algoritmo usará os estados mais populares do atributo e tratará os demais estados como ausentes.  
  
 O padrão é 100.  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte aos seguintes sinalizadores de modelagem. Ao criar um modelo ou uma estrutura de mineração, você define sinalizadores de modelagem para especificar como os valores em cada coluna são manipulados durante a análise. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Sinalizador de modelagem|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Significa que a  coluna será tratada como tendo dois estados possíveis: Ausente e Existente. Nulo é um valor ausente.<br /><br /> Aplica-se à coluna de modelo de mineração.|  
|NOT NULL|Indica que a coluna não pode conter um nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.<br /><br /> Aplica-se à coluna de estrutura de mineração.|  
  
## <a name="requirements"></a>Requisitos  
 Um modelo de árvore Naive Bayes deve conter uma coluna de chave, pelo menos um atributo previsível e pelo menos um atributo de entrada. Nenhum atributo pode ser contínuo; se seus dados contiverem dados numéricos contínuos, eles serão ignorados ou diferenciados.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo Naive Bayes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte a colunas de entrada e colunas previsíveis específicas que são listadas na tabela a seguir. Para obter mais informações sobre o significado dos tipos de conteúdo quando usados em um modelo de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Cíclico, discreto, diferenciado, chave, tabela, e ordenado|  
|Atributo previsível|Cíclico, discreto, diferenciado, tabela, e ordenado|  
  
> [!NOTE]  
>  Os tipos de conteúdo Cíclico e Ordenado têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo Naïve Bayes da Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Exemplos de consulta de modelo naive Bayes](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos Naive Bayes &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
