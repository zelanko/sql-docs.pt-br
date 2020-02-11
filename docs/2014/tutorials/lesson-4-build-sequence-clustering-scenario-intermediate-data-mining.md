---
title: 'Lição 4: Criando um cenário de clustering de sequências (tutorial de mineração de dados intermediário) | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62710598"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>Lição 4: Criando um cenário de clustering de sequências (Tutorial de mineração de dados intermediário)
  O departamento de marketing da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] deseja compreender como os clientes navegam pelo site da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . A empresa suspeita que há um padrão para a ordem na qual os clientes colocam os produtos em suas cestas de compra. Eles desejam analisar a ordem das sequências de compra para aprender como os clientes adicionam itens relacionados às suas cestas. Em seguida, eles podem usar essas informações para simplificar o fluxo do site para que ele leve os clientes a adquirir produtos adicionais.  
  
 Depois de concluir as tarefas desta lição, você terá criado um modelo de mineração que usa o algoritmo Clustering de Sequências do [!INCLUDE[msCoName](../includes/msconame-md.md)] para prever o próximo item que os clientes colocarão em suas cestas de compra. Você fará testes com duas versões do modelo: uma que analisa somente a ordem de produtos na cesta e outra que contém alguns dados demográficos de cliente adicionais para clustering. Por fim, você usará os modelos para criar previsões que poderão ser usadas na recomendação de produtos aos clientes.  
  
 Para concluir as tarefas na lição, você usará a estrutura de mineração da cesta de compras criada na [lição 3: Criando um cenário de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md). Esta lição contém as seguintes tarefas:  
  
-   [Criando uma estrutura de modelo de mineração de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [Processando o modelo de clustering de sequências](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [Explorando o modelo de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Criando um modelo de clustering de sequências relacionados &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Criando previsões em um modelo de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma estrutura de modelo de mineração de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas as lições  
 [Lição 1: criando a solução intermediária de mineração de dados &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lição 2: Criando um cenário de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lição 3: Criando um cenário de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 Lição 4: Cenário de clustering de sequências (tutorial de mineração de dados intermediário)  
  
 [Lição 5: criando modelos de rede neural e de regressão logística &#40;o tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial de mineração de dados intermediário &#40;Analysis Services de mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
