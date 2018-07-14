---
title: 'Lição 5: Criando a rede Neural e modelos de regressão logística (Tutorial de mineração de dados intermediário) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- data mining [Analysis Services], tutorials
- neural networks
- tutorials [Data Mining]
- neural network model [Analysis Services]
ms.assetid: 42c3701a-1fd2-44ff-b7de-377345bbbd6b
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93946e13e9836aef4cd10bc39ec964e7f8c0d531
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222336"
---
# <a name="lesson-5-building-neural-network-and-logistic-regression-models-intermediate-data-mining-tutorial"></a>Lição 5: Criando modelos de rede neural e de regressão logística (Tutorial de mineração de dados intermediário)
  
  
 O departamento de operações de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] está envolvido em um projeto para melhorar a satisfação do cliente com seu call center. Eles contrataram um fornecedor para gerenciar o call center e relatar a métrica da efetividade do call center e pediram a você para analisar alguns dados preliminares apresentados pelo fornecedor. Eles querem saber se é há alguma descoberta interessante. Em particular, eles gostariam de saber se os dados sugerem algum problema com a equipe ou maneiras de melhorar a satisfação do cliente.  
  
 O conjunto de dados é pequeno e abrange apenas um período de 30 dias na operação do call center. Os dados mostram o número de operadores novos e experientes em cada turno, o número de chamadas recebidas, o número de pedidos e os problemas que devem ser resolvidos e o tempo médio que o cliente aguarda para alguém responder à chamada. Os dados também incluem uma métrica de qualidade de serviço baseada na *taxa de abandono*, que é um indicador de frustração do cliente.  
  
 Como você não tem nenhuma expectativa anterior sobre o que os dados mostrarão, você decide usar um modelo de rede neural para explorar as possíveis correlações. Os modelos de rede neural são usados com frequência para exploração, porque podem analisar relações complexas entre muitas entradas e saídas.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Nesta lição, você usará o algoritmo de rede neural para criar um modelo que você e a equipe de Operações possam usar para entender as tendências nos dados. Como parte desta lição, você tentará responder as seguintes perguntas:  
  
-   Quais fatores afetam a satisfação do cliente?  
  
-   O que o call center pode fazer para melhorar a qualidade do serviço?  
  
 Com base nos resultados, você criará um modelo de regressão logística que poderá usar para previsões. As previsões serão usadas pela equipe de Operações como um auxílio no planejamento da operação do call center.  
  
 Eis os tópicos desta lição:  
  
-   [Adicionando dados de um exibição da fonte de dados de Call Center &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
-   [Criando uma estrutura de rede Neural e o modelo &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Explorando o modelo de Call Center &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
-   [Adicionando um modelo de regressão logística à estrutura do Call Center &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
-   [Criando previsões para modelos de Call Center &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Adicionando dados de um exibição da fonte de dados de Call Center &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas as lições  
 [Lição 1: Criando a solução de mineração de dados intermediário &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lição 4: Criando um cenário de Clustering de sequências &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 Lição 5: Cenário de rede neural e de regressão logística (tutorial de mineração de dados intermediário)  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial de mineração de dados básicos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial de mineração de dados intermediário &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
