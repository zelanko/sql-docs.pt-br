---
title: Validando modelos e usando modelos para previsão (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97268dac1fef029bc35ff702ace0d422ee296d65
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66065497"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>Validando modelos e usando modelos para previsão (suplementos de mineração de dados para Excel)
  Testar e validar o modelo são etapas importantes no processo de mineração de dados. Você deve saber o quão bom é o desempenho dos modelos de mineração em relação aos dados reais, antes de implantá-los em um ambiente de produção.  
  
 Os Suplementos de Mineração de Dados incluem ferramentas que ajudam você a testar os modelos criados e a criar previsões e recomendações usando os modelos.  
  
## <a name="accuracy-chart"></a>Gráfico de Precisão  
 O assistente de **gráfico de precisão** ajuda a criar uma consulta de previsão e a avaliar o desempenho de um modelo de Data Mining criando um gráfico de comparação de dispersão ou gráfico de comparação. O gráfico de comparação de precisão ajuda a diferenciar modelos de uma estrutura que são quase os mesmos, a fim de auxiliar a determinar qual modelo fornece as melhores previsões.  
  
 [Gráfico de precisão &#40;SQL Server suplementos de mineração de dados&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>Matriz de classificação  
 O assistente de **matriz de classificação** ajuda a criar uma consulta de previsão para avaliar o desempenho de um modelo de classificação. A saída é um gráfico que resume previsões precisas e imprecisas feitas pelo modelo. A matriz é uma ferramenta valiosa porque além de mostrar com que frequência o modelo previu corretamente um valor, também mostra quais valores o modelo mais previu de forma incorreta.  
  
 [&#40;de matrizes de classificação SQL Server suplementos de mineração de dados&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>Gráfico de ganho  
 O assistente de **gráfico de ganho** ajuda a avaliar os benefícios de usar um modelo de data mining e avaliar os custos de falsos positivos e falsos negativos  
  
 Esse tipo de gráfico mede a precisão da previsão do modelo e incorpora custos unitários e gerais especificados por você.  
  
 [&#40;de gráfico de ganho SQL Server suplementos de mineração de dados&#41;](profit-chart-sql-server-data-mining-add-ins.md).  
  
## <a name="cross-validation"></a>Validação cruzada  
 A validação cruzada é uma técnica estabelecida na comunidade de mineração de dados para avaliar a validade de um conjunto de dados e a precisão de um modelo de mineração no conjunto de dados. Divide um conjunto de dados em subconjuntos e, então, cria, treina e testa interativamente modelos em cada subconjunto.  
  
 O assistente de **validação cruzada** permite especificar o número de dobras pelos quais os dados são divididos e, em seguida, fornece um relatório de validação cruzada que descreve estatisticamente as diferenças entre essas seções cruzadas. A partir disso, você pode determinar se o modelo é bem-executado em todos os dados de treinamento ou talvez seja afetado por um subconjunto em particular.  
  
 [&#40;de validação cruzada SQL Server suplementos de mineração de dados&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>Assistente de Consulta  
 O assistente de **consulta** é uma ferramenta interativa que ajuda você a criar uma consulta de previsão. As consultas são uma forma de gerar recomendações, previsões futuras e assim por diante.  
  
 No assistente de **consulta** , você escolhe um modelo e, em seguida, fornece dados de entrada, como valores únicos ou de uma tabela ou intervalo, e o assistente o ajuda a selecionar colunas para saída. Também é possível adicionar funções à sua consulta para gerar pontuações de probabilidade e outras estatísticas úteis.  
  
 [&#40;de consulta SQL Server suplementos de mineração de dados&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>Editor Avançado de Consulta  
 O **Editor de consulta avançada** é um conjunto interativo de caixas de diálogo que ajuda você a criar todos os tipos de instruções DMX, tudo, desde a execução de consultas personalizadas até a criação e o treinamento de novos modelos, a exclusão de modelos ou a criação de novos conjuntos de dados.  
  
 [Editor de Consulta Avançada de Mineração de Dados](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Explorando e limpando dados](exploring-and-cleaning-data.md)   
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Implantando e dimensionando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
