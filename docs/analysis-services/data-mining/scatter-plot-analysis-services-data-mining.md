---
title: "Dispersão (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- charts [Analysis Services]
- mining models [Analysis Services], validating
- scatter charts
- regression algorithms [Analysis Services]
ms.assetid: 166812ec-fd1c-47c8-88db-d5041142be91
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 14f83d4b7235f3633c05c35afd2c648397e4f8a0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="scatter-plot-analysis-services---data-mining"></a>Dispersão (Analysis Services - Mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Um *dispersão* gráficos os valores reais em seus dados em relação aos valores previstos pelo modelo. A dispersão exibe os valores reais no eixo X e os valores previstos no eixo Y. Ela também exibe uma linha que ilustra a previsão perfeita, onde o valor previsto corresponde exatamente ao valor real. A distância de um ponto a partir desta linha angular ideal de 45º indica quão boa ou ruim foi a previsão.  
  
## <a name="understanding-the-scatter-plot"></a>Entendendo a dispersão  
 Considere um modelo no qual o departamento de marketing prevê vendas diárias com base no número de cliques em um link enviado em um email promocional. Como o número de cliques e a quantidade de vendas são expressos em valores numéricos contínuos, você pode representar graficamente o número de cliques como uma variável independente e as vendas como uma variável dependente. Ao fazer isso, a linha reta mostra a relação linear esperada e os pontos espalhados ao redor da linha mostram como os dados reais divergem do esperado. Essa análise indica de forma direta se um conjunto de resultados está próximo ou não de uma entrada específica e qual a variação com relação ao modelo ideal.  
  
## <a name="interpreting-the-results"></a>Interpretando os resultados  
 O diagrama a seguir mostra um exemplo de uma dispersão criada para o cenário que acabamos de descrever.  
  
 ![exemplo de um gráfico de dispersão para regressão linear](../../analysis-services/data-mining/media/scatterplot-callctr.gif "exemplo de um gráfico de dispersão para regressão linear")  
  
 Você pode posicionar o mouse em qualquer ponto ao redor da linha para exibir os valores previstos e reais em uma dica de ferramenta. Não há uma **Legenda de Mineração** para uma dispersão; porém, o próprio gráfico contém uma legenda que exibe a pontuação associada ao modelo. Para obter mais informações sobre como interpretar a pontuação, consulte [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
 Você pode copiar a representação visual do gráfico para a área de transferência, mas não os dados subjacentes ou a fórmula. Caso queira exibir a fórmula de regressão da linha, poderá criar uma consulta de conteúdo para o modelo. Para obter mais informações, consulte [Exemplos de consulta do modelo de regressão linear](../../analysis-services/data-mining/linear-regression-model-query-examples.md).  
  
## <a name="restrictions-on-scatter-plots"></a>Restrições em dispersões  
 Uma dispersão só pode ser criada quando o modelo escolhido na guia **Seleção de Entrada** contém um atributo previsível contínuo. Não é necessário fazer outras seleções; o tipo de gráfico de dispersão é exibido automaticamente na guia **Gráfico de Comparação de Precisão** com base no modelo e no tipo de atributo.  
  
 Embora modelos de série temporal prevejam números contínuos, você não pode medir a precisão de um modelo de série temporal usando uma dispersão. Você pode usar outros métodos, como reservar uma parte dos dados históricos. Para obter mais informações, consulte [Exemplos de consulta do modelo de série temporal](../../analysis-services/data-mining/time-series-model-query-examples.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Os tópicos a seguir contêm mais informações sobre como criar e usar dispersões e gráficos de precisão relacionados.  
  
|Tópicos|Links|  
|------------|-----------|  
|Fornece um passo a passo sobre como criar um gráfico de comparação de precisão para o modelo Mala Direta Dirigida.|[Tutorial de mineração de dados básico](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)<br /><br /> [Testando a precisão com gráficos de comparação de precisão &#40;Tutorial de mineração de dados básica&#41;](http://msdn.microsoft.com/library/822d414b-4a39-473f-80c3-53476e30655a)|  
|Explica os tipos de gráficos relacionados.|[Gráfico de comparação de precisão &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de ganho &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Matriz de classificação &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)|  
|Descreve usos de validação cruzada para modelos de mineração e estruturas de mineração.|[Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Descreve as etapas para criar gráficos de comparação de precisão e outros gráficos de exatidão.|[Tarefas de teste e validação e instruções &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Teste e validação &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
