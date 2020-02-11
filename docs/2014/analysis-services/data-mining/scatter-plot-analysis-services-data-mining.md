---
title: Gráfico de dispersão (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- charts [Analysis Services]
- mining models [Analysis Services], validating
- scatter charts
- regression algorithms [Analysis Services]
ms.assetid: 166812ec-fd1c-47c8-88db-d5041142be91
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3319b72f1c3b37805a653d1f315aa0a3363521a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082936"
---
# <a name="scatter-plot-analysis-services---data-mining"></a>Dispersão (Analysis Services - Mineração de dados)
  Uma *dispersão* representa de forma gráfica os valores reais de seus dados em relação aos valores previstos pelo modelo. A dispersão exibe os valores reais no eixo X e os valores previstos no eixo Y. Ela também exibe uma linha que ilustra a previsão perfeita, onde o valor previsto corresponde exatamente ao valor real. A distância de um ponto a partir desta linha angular ideal de 45º indica quão boa ou ruim foi a previsão.  
  
## <a name="understanding-the-scatter-plot"></a>Entendendo a dispersão  
 Considere um modelo no qual o departamento de marketing prevê vendas diárias com base no número de cliques em um link enviado em um email promocional. Como o número de cliques e a quantidade de vendas são expressos em valores numéricos contínuos, você pode representar graficamente o número de cliques como uma variável independente e as vendas como uma variável dependente. Ao fazer isso, a linha reta mostra a relação linear esperada e os pontos espalhados ao redor da linha mostram como os dados reais divergem do esperado. Essa análise indica de forma direta se um conjunto de resultados está próximo ou não de uma entrada específica e qual a variação com relação ao modelo ideal.  
  
## <a name="interpreting-the-results"></a>Interpretando os resultados  
 O diagrama a seguir mostra um exemplo de uma dispersão criada para o cenário que acabamos de descrever.  
  
 ![exemplo de um gráfico de dispersão para regressão linear](../media/scatterplot-callctr.gif "exemplo de um gráfico de dispersão para regressão linear")  
  
 Você pode posicionar o mouse em qualquer ponto ao redor da linha para exibir os valores previstos e reais em uma dica de ferramenta. Não há uma **Legenda de Mineração** para uma dispersão; porém, o próprio gráfico contém uma legenda que exibe a pontuação associada ao modelo. Para obter mais informações sobre como interpretar a pontuação, consulte [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Mineração de dados&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
 Você pode copiar a representação visual do gráfico para a área de transferência, mas não os dados subjacentes ou a fórmula. Caso queira exibir a fórmula de regressão da linha, poderá criar uma consulta de conteúdo para o modelo. Para obter mais informações, consulte [Exemplos de consulta do modelo de regressão linear](linear-regression-model-query-examples.md).  
  
## <a name="restrictions-on-scatter-plots"></a>Restrições em dispersões  
 Uma dispersão só pode ser criada quando o modelo escolhido na guia **Seleção de Entrada** contém um atributo previsível contínuo. Não é necessário fazer outras seleções; o tipo de gráfico de dispersão é exibido automaticamente na guia **Gráfico de Comparação de Precisão** com base no modelo e no tipo de atributo.  
  
 Embora modelos de série temporal prevejam números contínuos, você não pode medir a precisão de um modelo de série temporal usando uma dispersão. Você pode usar outros métodos, como reservar uma parte dos dados históricos. Para obter mais informações, consulte [Exemplos de consulta do modelo de série temporal](time-series-model-query-examples.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Os tópicos a seguir contêm mais informações sobre como criar e usar dispersões e gráficos de precisão relacionados.  
  
|Tópicos|Links|  
|------------|-----------|  
|Fornece um passo a passo sobre como criar um gráfico de comparação de precisão para o modelo Mala Direta Dirigida.|[Tutorial de mineração de dados básico](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [Testando a exatidão com gráficos de comparação de precisão &#40;tutorial de mineração de dados básico&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|Explica os tipos de gráficos relacionados.|[&#40;do gráfico de comparação de precisão Analysis Services-Mineração de dados&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de ganho &#40;Analysis Services-Mineração de dados&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [&#40;de matriz de classificação Analysis Services&#41;de mineração de dados](classification-matrix-analysis-services-data-mining.md)|  
|Descreve usos de validação cruzada para modelos de mineração e estruturas de mineração.|[&#40;de validação cruzada Analysis Services&#41;de mineração de dados](cross-validation-analysis-services-data-mining.md)|  
|Descreve as etapas para criar gráficos de comparação de precisão e outros gráficos de exatidão.|[Tarefas de teste e validação e instruções &#40;mineração de dados&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Teste e validação &#40;mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
  
