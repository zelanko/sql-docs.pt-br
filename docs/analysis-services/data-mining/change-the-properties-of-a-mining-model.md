---
title: "Alterar as propriedades de um modelo de minera&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos de mineração [Analysis Services], propriedades"
  - "propriedades [mineração de dados]"
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# Alterar as propriedades de um modelo de minera&#231;&#227;o
  Algumas propriedades de modelo de mineração se aplicam ao modelo como um todo, enquanto outras propriedades de modelo se aplicam a colunas individuais. Exemplos de propriedades que se aplicam ao modelo inteiro seriam a propriedade **Drillthrough** , que especifica se os dados de caso devem estar disponíveis para consulta, e a propriedade **Description** . Propriedades que se aplicam à coluna incluem **Usage** e **ModelingFlags**, que controlam como os dados na coluna são usados no modelo.  
  
 As propriedades modelo a seguir têm editores avançados que você pode usar para criar expressões ou configurar propriedades de modelo complexas. Estas propriedades oferecem:  
  
-   Propriedade **Filtro**: abre a [Caixa de Diálogo Filtro de Conjunto de Dados ou Filtro de Modelo](../Topic/Data%20Set%20Filter%20or%20Model%20Filter%20Dialog%20Box.md).  
  
-   Propriedade **AlgorithmParameters**: abre a [Caixa de diálogo de Parâmetros de Algoritmo &#40;Exibição de Modelos de Mineração&#41;](../Topic/Algorithm%20Parameters%20Dialog%20Box%20\(Mining%20Models%20View\).md).  
  
 Para obter informações sobre como definir as propriedades em um modelo de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### Para alterar as propriedades de um modelo de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Data Mining, clique com o botão direito do mouse no cabeçalho da coluna que contém o nome do modelo de mineração ou na linha da grade que contém o nome do algoritmo de mineração e selecione **Propriedades**.  
  
2.  Na janela **Propriedades** na lateral direita da tela, realce o valor que corresponde à propriedade que você deseja alterar e digite o novo valor.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
### Para alterar as propriedades de uma coluna de modelo de mineração  
  
1.  Na guia **Modelos de Mineração** no Designer de Data Mining, clique com o botão direito do mouse na célula da grade na interseção da coluna da estrutura de mineração e do modelo de mineração e selecione **Propriedades**.  
  
2.  Na janela **Propriedades** na lateral direita da tela, realce o valor que corresponde à propriedade que você deseja alterar e digite o novo valor.  
  
    > [!NOTE]  
    >  Se o uso da coluna for definido como **Ignorar**, a janela **Propriedades** da coluna ficará em branco.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  