---
title: "Alterar a diferencia&#231;&#227;o de uma coluna em um modelo de minera&#231;&#227;o | Microsoft Docs"
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
  - "discretização [Analysis Services]"
  - "estruturas de mineração [Analysis Services], tópicos de instruções"
  - "colunas diferenciadas [mineração de dados]"
  - "problemas de segmentação [Analysis Services]"
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 14
---
# Alterar a diferencia&#231;&#227;o de uma coluna em um modelo de minera&#231;&#227;o
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] discretiza automaticamente valores, ou seja, compartimentaliza dados na coluna numérica em determinados cenários. Por exemplo, se seus dados contêm dados numéricos contínuos e você cria um modelo de árvore de decisão, cada coluna de dados contínuos é compartimentalizada automaticamente, dependendo da distribuição dos dados. Para controlar o modo como os dados são diferenciados, altere as propriedades na coluna da estrutura de mineração que controla como os dados são usados no modelo.  
  
 Para obter informações gerais sobre como definir as propriedades em um modelo de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### Para exibir as propriedades para uma coluna do modelo de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, clique com o botão direito do mouse no cabeçalho da coluna que contém o nome do modelo de mineração ou na linha da grade que contém o nome do algoritmo de mineração e selecione **Propriedades**.  
  
     A janela **Propriedades** exibe as propriedades que são associadas com o modelo de mineração.  
  
2.  Na coluna **Estrutura** próxima ao lado esquerdo da tela, clique na coluna que contém os dados numéricos contínuos que você deseja diferenciar.  
  
     A janela **Propriedades** altera para exibir apenas as propriedades associadas com aquela coluna.  
  
### Para alterar o método de diferenciação  
  
1.  Na janela **Propriedades de Mineração** , clique na caixa de texto próxima a **Conteúdo**e selecione **Discretized** na lista suspensa.  
  
     As propriedades <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> agora estão habilitadas.  
  
2.  Na janela **Propriedades**, clique na caixa de texto próxima a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> e selecione os seguintes valores: **Automatic**, **EqualAreas** ou **Cluster**.  
  
    > [!NOTE]  
    >  Se o uso da coluna for definido como **Ignorar**, a janela **Propriedades** da coluna ficará em branco.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
3.  Na janela **Propriedades**, clique na caixa de texto próximo a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> e digite um valor numérico.  
  
    > [!NOTE]  
    >  Se alterar essas propriedades, a estrutura deve ser reprocessada juntamente com quaisquer modelos no quais você queira usar a nova configuração.  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  