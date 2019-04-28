---
title: 'Lição 4: Criando um cenário (Tutorial de mineração de dados intermediário) de Clustering de sequências | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d34125b7b750daa1da25c9e8788172b5d9ca2c35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710598"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>Lição 4: Criando um cenário (Tutorial de mineração de dados intermediário) de Clustering de sequências
  O departamento de marketing da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] deseja compreender como os clientes navegam pelo site da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . A empresa suspeita que há um padrão para a ordem na qual os clientes colocam os produtos em suas cestas de compra. Eles desejam analisar a ordem das sequências de compra para aprender como os clientes adicionam itens relacionados às suas cestas. Em seguida, eles podem usar essas informações para simplificar o fluxo do site para que ele leve os clientes a adquirir produtos adicionais.  
  
 Depois de concluir as tarefas desta lição, você terá criado um modelo de mineração que usa o algoritmo Clustering de Sequências do [!INCLUDE[msCoName](../includes/msconame-md.md)] para prever o próximo item que os clientes colocarão em suas cestas de compra. Você fará testes com duas versões do modelo: uma que analisa somente a ordem de produtos na cesta e outra que contém alguns dados demográficos de cliente adicionais para clustering. Por fim, você usará os modelos para criar previsões que poderão ser usadas na recomendação de produtos aos clientes.  
  
 Para concluir as tarefas na lição, você usará a estrutura de mineração da cesta de compras que você criou na [lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md). Esta lição contém as seguintes tarefas:  
  
-   [Criando uma estrutura de modelo de mineração de Clustering de sequência &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [Processando o modelo de clustering de sequências](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [Explorando o modelo de Clustering de sequências &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Criando um modelo de Clustering de sequências relacionado &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Criando previsões em um modelo de Clustering de sequência &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma estrutura de modelo de mineração de Clustering de sequência &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas as lições  
 [Lição 1: Criando a solução de mineração de dados intermediário &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lição 3: Criando um cenário de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 Lição 4: Sequência de cenário de Clustering (Tutorial de mineração de dados intermediário)  
  
 [Lição 5: Criação de rede Neural e modelos de regressão logística &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial de mineração de dados intermediário &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
