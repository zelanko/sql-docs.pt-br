---
title: 'Lição 4: explorando os modelos de endereçamento de destino (tutorial de mineração de dados básico) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 97db61dc3b9adf2e345957c8e08aa752e51286e0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312146"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>Lição 4: Explorando os modelos de mala direta (Tutorial de mineração de dados básico)
  Depois que os modelos do seu projeto tiverem sido processados, você poderá explorá-los para procurar por tendências que sejam interessantes. Como padrões podem ser complexos e difíceis se analisarmos somente os números, a Mineração de Dados do SQL Server oferece algumas ferramentas visuais que o ajudam a investigar os dados e a compreender as regras e as relações que os algoritmos encontraram nos dados. Você também pode usar uma variedade de testes de precisão para validar seu conjunto de dados ou para descobrir qual o melhor modelo antes de implantá-lo.  
  
 Quando você usa [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o para explorar seus modelos, cada modelo que você criou é listado na guia **Visualizador do modelo de mineração** no designer de mineração de dados. Você pode usar os visualizadores para explorar os modelos. Estes visualizadores também estão disponíveis no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Cada algoritmo usado para criar um modelo no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] retorna um tipo diferente de resultado. Consequentemente, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece visualizadores personalizados para cada tipo de modelo de aprendizado automatizado.  
  
 Se você quiser obter detalhes, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o também fornece um visualizador de HTML, chamado Visualizador de árvore de **conteúdo genérico**, que exibe informações detalhadas sobre os dados do modelo e quaisquer padrões encontrados, em um formato semitabular. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérico da Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
 Nesta lição, você examinará os resultados dos seus três modelos. Cada tipo de modelo se baseia em um algoritmo diferente e oferece ideias diferentes sobre os dados.  
  
-   O modelo Árvore de Decisão mostra os fatores que influenciam a compra de uma bicicleta.  
  
-   O modelo Clustering agrupa seus clientes por atributos que incluem seu comportamento na compra de bicicletas e outros atributos selecionados.  
  
-   O modelo Naive Baynes permite que você explore o relacionamento entre os atributos diferentes.  
  
 Consulte os tópicos a seguir para saber mais sobre os visualizadores do modelo de mineração.  
  
-   [Exploração do modelo de árvore de decisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o modelo de clustering &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Explorando o Naive Bayes do modelo de mineração de dados &#40;Basic&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 Todos os três modelos podem ser exibidos usando o **Visualizador de árvore de conteúdo genérico**, para extrair fórmulas, valores de dados e assim por diante.  
  
## <a name="first-task-in-lesson"></a>Primeira tarefa na lição  
 [Exploração do modelo de árvore de decisão &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>Lição anterior  
 [Lição 3: Adicionando e processando modelos](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 5: testando modelos &#40;o tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do Visualizador do modelo de mineração](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Visualizadores do Modelo de Mineração de Dados](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
