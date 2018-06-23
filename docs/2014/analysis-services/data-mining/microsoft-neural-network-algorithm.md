---
title: Algoritmo rede Neural da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- training neural networks
- output neurons [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- neurons [Analysis Services]
- classification algorithms [Analysis Services]
- neural networks
- multilayer perceptron network of neurons [Analysis Services]
- hidden neurons
- Back-Propagated Delta Rule network
- input neurons [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 61eb4861-8a6a-4214-a4b8-1dd278ad7a68
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fc557e9a063b5f3031d6a817b0bf85325b94e086
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120228"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm
  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo rede Neural combina cada estado possível do atributo de entrada com cada estado possível do atributo previsível e usa os dados de treinamento para calcular probabilidades. Posteriormente, essas probabilidades podem ser usadas para classificação ou regressão e também para a previsão de um resultado do atributo previsível com base nos atributos de entrada.  
  
 Um modelo de mineração desenvolvido com o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode conter várias redes, dependendo do número de colunas usadas para a previsão de entrada ou usadas apenas para previsão. O número de redes que um modelo de mineração simples contém depende do número de estados que estão contidos nas colunas de entrada e as colunas previsíveis que o modelo de mineração usa.  
  
## <a name="example"></a>Exemplo  
 O algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é útil para analisar dados de entrada complexos, tais como de um processo de fabricação, de comercialização ou, problemas comerciais para os quais uma quantidade significativa de dados de treinamento está disponível mas, para os quais regras não podem ser facilmente derivadas usando outros algoritmos.  
  
 Os cenários sugeridos para usar o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluem o seguinte:  
  
-   Análise de promoção e marketing, tais como, medição do sucesso de uma promoção de mala direta ou de uma campanha publicitária radiofônica.  
  
-   Prevendo movimento de ações, flutuação de moeda ou demais informações financeiras altamente fluidas a partir de dados históricos.  
  
-   Analisando processos industriais e de fabricação.  
  
-   Mineração de texto.  
  
-   Qualquer modelo de previsão que analisa relações complexas entre muitas entradas e, relativamente, menos saídas.  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 O [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo rede Neural cria uma rede que é composta de até três camadas de neurônios. Essas camadas são uma camada de entrada, uma camada opcional oculta e uma camada de saída.  
  
 **Camada de entrada:** os neurônios de entrada definem todos os valores de atributo de entrada para o modelo de mineração de dados e suas probabilidades.  
  
 **Camada oculta:** neurônios ocultos recebem entradas de neurônios de entrada e fornecem saídas para os neurônios de saída. A camada oculta é onde as várias probabilidades de entradas são ponderadas. Uma ponderação descreve a relevância ou importância de uma entrada específica para o neurônio oculto. Quanto maior a ponderação atribuída a uma entrada, mais importante será o valor daquela entrada. As ponderações podem ser negativas, o que significa que a entrada pode inibir, em vez de favorecer, um resultado específico.  
  
 **Camada de saída:** neurônios de saída representam valores de atributos previsíveis para o modelo de mineração de dados.  
  
 Para obter uma explicação detalhada de como as camadas de entrada, oculta e de saída são criadas e pontuadas, consulte [Referência técnica do algoritmo Rede Neural da Microsoft](microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="data-required-for-neural-network-models"></a>Dados necessários para modelos de rede neural  
 Um modelo de rede neural deve conter uma coluna de chave, uma ou mais colunas de entrada e uma ou mais colunas previsíveis.  
  
 Os modelos de mineração de dados que usam o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] são amplamente influenciados pelos valores especificados para os parâmetros disponíveis para o algoritmo. Esses parâmetros definem como os dados são amostrados, são distribuídos ou estimados para serem distribuídos em cada coluna e quando a seleção de recurso é chamada para limitar os valores usados no modelo final.  
  
 Para obter mais informações sobre como definir parâmetros para personalizar o comportamento do modelo, consulte [Referência técnica do algoritmo Rede Neural da Microsoft](microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="viewing-a-neural-network-model"></a>Exibindo um modelo de rede neural  
 Para trabalhar com os dados e verificar como o modelo correlaciona entradas com resultados, é possível usar o **Visualizador de Rede Neural da Microsoft**. Com esse visualizador personalizado, você pode filtrar os atributos de entrada e seus valores e visualizar gráficos que mostram como eles afetam os resultados. As dicas de ferramentas no visualizador mostram a probabilidade e a comparação associadas a cada par de valores de entrada e de saída. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 A maneira mais fácil de explorar a estrutura do modelo é usando o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. É possível visualizar as entradas, os resultados e as redes criados pelo modelo e clicar em qualquer nó para expandi-lo e exibir as estatísticas relacionadas aos nós nas camadas de entrada, de saída e oculta. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérico da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
## <a name="creating-predictions"></a>Criando previsões  
 Depois de processado o modelo, você pode usar a rede e as ponderações armazenadas em cada nó para fazer previsões. Um modelo de rede neural suporta regressão, associação e análise de classificação. Portanto, o significado de cada previsão pode ser diferente. Você também pode consultar o próprio modelo para revisar as correlações que foram localizadas e recuperar estatísticas relacionadas. Para obter exemplos de como criar consultas em um modelo de rede neural, consulte [Exemplos de consulta de modelo de rede neural](neural-network-model-query-examples.md).  
  
 Para obter informações gerais sobre como criar uma consulta em um modelo de mineração de dados, consulte [Consultas de mineração de dados](data-mining-queries.md).  
  
## <a name="remarks"></a>Remarks  
  
-   Não suporta detalhamento ou dimensões de mineração de dados. Isso acontece porque a estrutura dos nós do modelo de mineração não corresponde diretamente aos dados subjacentes.  
  
-   Não suporta a criação de modelos no formato PMML (Predictive Model Markup Language).  
  
-   Suporta o uso de modelos de mineração OLAP.  
  
-   Não suporta a criação de dimensões de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)   
 [Conteúdo do modelo de rede Neural modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de rede neural](neural-network-model-query-examples.md)   
 [Algoritmo Regressão Logística da Microsoft](microsoft-logistic-regression-algorithm.md)  
  
  