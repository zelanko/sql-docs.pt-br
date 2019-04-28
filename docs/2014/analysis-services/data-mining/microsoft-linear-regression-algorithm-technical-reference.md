---
title: Referência técnica do algoritmo de regressão Linear de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a4bd34c0ce6a84ca4f9050f4c4b428123c379dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721898"
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Referência Técnica do Algoritmo de Regressão Linear da Microsoft
  O algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é uma versão especial do algoritmo Árvores de decisão da Microsoft, otimizada para modelagem de pares de atributos contínuos. Este tópico explica a implementação do algoritmo, descreve como personalizar o comportamento do algoritmo e fornece links para informações adicionais sobre como consultar modelos.  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>Implementação do algoritmo de Regressão Linear  
 O algoritmo Árvores de Decisão da Microsoft pode ser usado para muitas tarefas: regressão linear, classificação ou análise de associação. Para implementar esse algoritmo para fins de regressão linear, os parâmetros do algoritmo são controlados de modo a restringir o crescimento da árvore e manter todos os dados no modelo em um único nó. Em outras palavras, embora a regressão linear se baseie em uma árvore de decisão, a árvore contém apenas uma única raiz e nenhuma ramificação: todos os dados residem no nó raiz.  
  
 Para isso, o parâmetro *MINIMUM_LEAF_CASES* do algoritmo é definido para ser maior ou igual ao número total de casos que o algoritmo usa para treinar o modelo de mineração. Com o parâmetro definido dessa maneira, o algoritmo nunca criará uma divisão e, portanto, executará uma regressão linear.  
  
 A equação que representa a linha na regressão assume a forma geral de y = ax + b e é conhecida como a equação de regressão. A variável Y representa a variável de saída, X representa a variável de entrada e a e b são coeficientes ajustáveis. Você pode recuperar os coeficientes, as interseções e outras informações sobre a fórmula de regressão consultando o modelo de mineração completo. Para obter mais informações, consulte [Exemplos de consulta do modelo de regressão linear](linear-regression-model-query-examples.md).  
  
### <a name="scoring-methods-and-feature-selection"></a>Métodos de pontuação e seleção de recursos  
 Todos os algoritmos de mineração de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usam seleção de recursos automaticamente para melhorar a análise e reduzir a carga de processamento. O método usado para seleção de recursos na regressão linear é a pontuação de interesse, porque o modelo tem suporte apenas para colunas contínuas. Para referência, a tabela a seguir mostra a diferença na seleção de recursos do algoritmo de Regressão Linear e o algoritmo de Árvores de decisão.  
  
|Algoritmo|Método de análise|Comentários|  
|---------------|------------------------|--------------|  
|Regressão Linear|Pontuação de interesse|Padrão.<br /><br /> Outros métodos de seleção de recursos disponíveis com o algoritmo Árvores de Decisão se aplicam às variáveis discretas apenas e, portanto, não são aplicáveis aos modelos de regressão linear.|  
|Árvores de decisão|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Se qualquer coluna contiver valores contínuos não binários, a pontuação de interesse será usada em todas as colunas para garantir a consistência. Caso contrário, será usado o método padrão ou o especificado.|  
  
 Os parâmetros de algoritmo que controlam seleção de recursos para um modelo de árvores de decisão são MAXIMUM_INPUT_ATTRIBUTES e MAXIMUM_OUTPUT.  
  
## <a name="customizing-the-linear-regression-algorithm"></a>Personalizando o algoritmo de Regressão Linear  
 O algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte a parâmetros que afetam o comportamento, o desempenho e a precisão do modelo de mineração resultante. Também é possível definir sinalizadores de modelagem nas colunas do modelo de mineração ou da estrutura de mineração para controlar a maneira como os dados são processados.  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 A tabela a seguir lista os parâmetros fornecidos para o algoritmo de Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|Define o número de atributos de entrada que o algoritmo pode manipular antes de invocar a seleção de recurso. Defina este valor como 0 para desativar a seleção de recursos.<br /><br /> O padrão é 255.|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|Define o número de atributos de saída que o algoritmo pode manipular antes de invocar a seleção de recurso. Defina este valor como 0 para desativar a seleção de recursos.<br /><br /> O padrão é 255.|  
|*FORCE_REGRESSOR*|Força o algoritmo a usar as colunas indicadas como regressores, independentemente da sua importância quando calculadas pelo algoritmo.|  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 O algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte aos seguintes sinalizadores de modelagem. Ao criar um modelo ou uma estrutura de mineração, você define sinalizadores de modelagem para especificar como os valores em cada coluna são manipulados durante a análise. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](modeling-flags-data-mining.md).  
  
|Sinalizador de modelagem|Descrição|  
|-------------------|-----------------|  
|NOT NULL|Indica que a coluna não pode conter um nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.<br /><br /> Aplica-se às colunas de estrutura de mineração.|  
|REGRESSOR|Indica que a coluna contém valores numéricos contínuos que devem ser tratados como variáveis independentes potenciais durante a análise.<br /><br /> Observação: Sinalizar uma coluna como um regressor não assegura que a coluna será usada como um regressor no modelo final.<br /><br /> Aplica-se às colunas de modelo de mineração.|  
  
### <a name="regressors-in-linear-regression-models"></a>Regressor em modelos de regressão lineares  
 Os modelos de regressão lineares baseiam-se no algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Entretanto, mesmo que você não use o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , todo modelo de árvore de decisão poderá conter uma árvore ou nós que representam uma regressão em um atributo contínuo.  
  
 Não é necessário especificar que uma coluna contínua representa um regressor. O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] particionará o conjunto de dados em regiões com padrões significativos mesmo que você não defina o sinalizador REGRESSOR na coluna. A diferença é que, quando você define o sinalizador de modelagem, o algoritmo tenta encontrar equações de regressão do formulário um * C1 + b\*C2 +... de acordo com os padrões em nós da árvore. A soma dos restos é calculada e, se o desvio for muito grande, será forçada uma divisão da árvore.  
  
 Por exemplo, se você estiver prevendo o comportamento de compra dos clientes usando **Renda** como um atributo e definir o sinalizador de modelagem REGRESSOR na coluna, o algoritmo primeiro tentará adequar-se aos valores de **Renda** usando uma fórmula de regressão padrão. Se o desvio for muito grande, a fórmula de regressão será abandonada e a árvore será dividida em algum outro atributo. O algoritmo árvore de decisão tentará ajustar um regressor para renda em cada uma das ramificações após a divisão.  
  
 Você pode usar o parâmetro FORCED_REGRESSOR para garantir que o algoritmo usará um determinado regressor. Esse parâmetro só pode ser usado com os algoritmos Árvores de decisão e Regressão Linear da Microsoft.  
  
## <a name="requirements"></a>Requisitos  
 Um modelo de regressão linear deve conter uma coluna de chave, colunas de entrada e pelo menos uma coluna previsível.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte a colunas de entrada e colunas previsíveis específicas que são listadas na tabela a seguir. Para obter mais informações sobre o significado dos tipos de conteúdo quando usados em um modelo de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](content-types-data-mining.md).  
  
|coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Contínuo, Cíclico, Chave, Tabela e Ordenado|  
|Atributo previsível|Contínuo, cíclico e ordenado|  
  
> [!NOTE]  
>  Os tipos de conteúdo `Cyclical` e `Ordered` têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo Regressão Linear da Microsoft](microsoft-linear-regression-algorithm.md)   
 [Exemplos de consulta do modelo de regressão linear](linear-regression-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
