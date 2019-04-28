---
title: Algoritmo rede Neural da Microsoft | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54896093b887985fc658e823f7d277347a70f0ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724967"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O algoritmo de Rede Neural do [!INCLUDE[msCoName](../../includes/msconame-md.md)] é uma implementação da popular e adaptável arquitetura de rede neural para aprendizado de máquina.  O algoritmo funciona testando cada estado possível do atributo de entrada com cada estado possível do atributo previsível e calculando probabilidades para cada combinação com base nos dados de treinamento. Essas probabilidades podem ser usadas para tarefas de classificação ou regressão e também para a previsão de um resultado com base em alguns atributos de entrada. Uma rede neural também pode ser usada para análise de associação.  
  
 Quando cria um modelo de mineração usando o algoritmo de Rede Neural do [!INCLUDE[msCoName](../../includes/msconame-md.md)] , você pode incluir várias saídas e o algoritmo criará várias redes. O número de redes contidas em um único modelo de mineração depende do número de estados (ou valores de atributo) nas colunas de entrada, bem como do número de colunas previsíveis que o modelo de mineração usa e o número de estados nessas colunas.  
  
## <a name="example"></a>Exemplo  
 O algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é útil para analisar dados de entrada complexos, tais como de um processo de fabricação, de comercialização ou, problemas comerciais para os quais uma quantidade significativa de dados de treinamento está disponível mas, para os quais regras não podem ser facilmente derivadas usando outros algoritmos.  
  
 Os cenários sugeridos para usar o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluem o seguinte:  
  
-   Análise de promoção e marketing, tais como, medição do sucesso de uma promoção de mala direta ou de uma campanha publicitária radiofônica  
  
-   Prevendo movimento de ações, flutuação de moeda ou demais informações financeiras altamente fluidas de dados históricos  
  
-   Analisando processos industriais e de fabricação  
  
-   Mineração de texto  
  
-   Qualquer modelo de previsão que analisa relações complexas entre muitas entradas e, relativamente, menos saídas  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 O algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] cria uma rede que é composta por até três camadas de nós (às vezes, chamadas de *neurônios*). Essas camadas são a *camada de entrada*, a *camada oculta*e a *camada de saída*.  
  
 **Camada de entrada:** Nós de entrada definem todos os valores de atributo de entrada para o modelo de mineração de dados e suas probabilidades.  
  
 **Camada oculta:** Nós ocultos recebem entradas de nós de entrada e fornecem resultados para nós de saída. A camada oculta é onde as várias probabilidades de entradas são ponderadas. Uma ponderação descreve a relevância ou importância de uma entrada específica para o nó oculto. Quanto maior a ponderação atribuída a uma entrada, mais importante será o valor daquela entrada. As ponderações podem ser negativas, o que significa que a entrada pode inibir, em vez de favorecer, um resultado específico.  
  
 **Camada de saída:** Nós de saída representam valores de atributos previsíveis para o modelo de mineração de dados.  
  
 Para obter uma explicação detalhada de como as camadas de entrada, oculta e de saída são criadas e pontuadas, consulte [Referência técnica do algoritmo Rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="data-required-for-neural-network-models"></a>Dados necessários para modelos de rede neural  
 Um modelo de rede neural deve conter uma coluna de chave, uma ou mais colunas de entrada e uma ou mais colunas previsíveis.  
  
 Os modelos de mineração de dados que usam o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] são amplamente influenciados pelos valores especificados para os parâmetros disponíveis para o algoritmo. Esses parâmetros definem como os dados são amostrados, são distribuídos ou estimados para serem distribuídos em cada coluna e quando a seleção de recurso é chamada para limitar os valores usados no modelo final.  
  
 Para obter mais informações sobre como definir parâmetros para personalizar o comportamento do modelo, consulte [Referência técnica do algoritmo Rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="viewing-a-neural-network-model"></a>Exibindo um modelo de rede neural  
 Para trabalhar com os dados e verificar como o modelo correlaciona entradas com resultados, é possível usar o **Visualizador de Rede Neural da Microsoft**. Com esse visualizador personalizado, você pode filtrar os atributos de entrada e seus valores e visualizar gráficos que mostram como eles afetam os resultados. As dicas de ferramentas no visualizador mostram a probabilidade e a comparação associadas a cada par de valores de entrada e de saída. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 A maneira mais fácil de explorar a estrutura do modelo é usando o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. É possível visualizar as entradas, os resultados e as redes criados pelo modelo e clicar em qualquer nó para expandi-lo e exibir as estatísticas relacionadas aos nós nas camadas de entrada, de saída e oculta. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérico da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
## <a name="creating-predictions"></a>Criando previsões  
 Depois de processado o modelo, você pode usar a rede e as ponderações armazenadas em cada nó para fazer previsões. Um modelo de rede neural suporta regressão, associação e análise de classificação. Portanto, o significado de cada previsão pode ser diferente. Você também pode consultar o próprio modelo para revisar as correlações que foram localizadas e recuperar estatísticas relacionadas. Para obter exemplos de como criar consultas em um modelo de rede neural, consulte [Exemplos de consulta de modelo de rede neural](../../analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 Para obter informações gerais sobre como criar uma consulta em um modelo de mineração de dados, consulte [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="remarks"></a>Comentários  
  
-   Não suporta detalhamento ou dimensões de mineração de dados. Isso acontece porque a estrutura dos nós do modelo de mineração não corresponde diretamente aos dados subjacentes.  
  
-   Não suporta a criação de modelos no formato PMML (Predictive Model Markup Language).  
  
-   Suporta o uso de modelos de mineração OLAP.  
  
-   Não suporta a criação de dimensões de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica do algoritmo Rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de rede neural](../../analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Algoritmo Regressão Logística da Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)  
  
  
