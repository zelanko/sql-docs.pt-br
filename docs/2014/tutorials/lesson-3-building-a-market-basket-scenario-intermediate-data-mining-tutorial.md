---
title: 'Lição 3: Criando um cenário de cesta de compras (Tutorial de mineração de dados intermediário) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- association algorithms [Analysis Services]
- nested tables
- tutorials [Data Mining]
ms.assetid: 651eef38-772e-4d97-af51-075b1b27fc5a
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 009449b753c96e59612654203c06f5c4ee1742a1
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312034"
---
# <a name="lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial"></a>Lição 3: Criando um cenário de cesta de compras (Tutorial de mineração de dados intermediário)
  O departamento de marketing da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] quer melhorar o site da empresa para promover a venda cruzada. Como parte da atualização do site, eles gostariam de ter a capacidade de prever produtos que um cliente talvez queira comprar, com base em outros produtos que já estão em sua cesta de compras online. O departamento de marketing também deseja entender melhor o comportamento de compra do cliente, para que possa criar o site de modo que os itens que tendem a ser adquiridos juntos apareçam juntos. Eles descobriram que a mineração de dados é especialmente útil para esse tipo de *análise de cesta de mercado* e lhe pediram para desenvolver um modelo de mineração de dados.  
  
 Depois de concluir as tarefas desta lição, você terá um modelo de mineração completo que mostra grupos de itens a partir do histórico de transações do cliente. Adicionalmente, você poderá usar o modelo de mineração para prever itens adicionais que talvez o cliente queira comprar.  
  
 Para concluir as tarefas nesta lição, você usará a fonte de dados e a solução que você criou na primeira lição do [Tutorial de mineração de dados intermediário &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Você modificará essa solução adicionando uma exibição da fonte de dados com tabelas sobre o cliente, incluindo uma tabela aninhada de compras de clientes.  Em seguida, você criará um modelo de mineração que use o algoritmo Microsoft Association Rules, apropriado a cenários de cesta de compras.  
  
 Eis os tópicos desta lição:  
  
-   [Adicionando dados de um fonte de exibição com tabelas aninhadas &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
-   [Criando uma estrutura de cesta de compras e modelo &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Modificando e processando o modelo de cesta de compras &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
-   [Explorando os modelos de cesta de compras &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
-   [Filtrando uma tabela aninhada em um modelo de mineração &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
-   [Prevendo associações &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Adicionando dados de um fonte de exibição com tabelas aninhadas &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>Todas as lições  
 [Lição 1: Criando a solução de mineração de dados intermediário &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lição 2: Criando um cenário de previsão &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 Lição 3: Cenário de cesta de compras (tutorial de mineração de dados intermediário)  
  
 [Lição 4: Criando um cenário de Clustering de sequências &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [Lição 5: Criar a rede Neural e modelos de regressão logística &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial de mineração de dados básicos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Lição 2: Criando um cenário de previsão &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)   
 [Lição 4: Criando um cenário de Clustering de sequências &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
  