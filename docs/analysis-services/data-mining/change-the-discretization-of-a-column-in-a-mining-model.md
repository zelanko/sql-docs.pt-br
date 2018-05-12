---
title: Alterar a diferenciação de uma coluna em um modelo de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9d6b2c75becad147e196534bb4d366dff01a13d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>Alterar a diferenciação de uma coluna em um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] discretiza automaticamente valores, ou seja, compartimentaliza dados na coluna numérica em determinados cenários. Por exemplo, se seus dados contêm dados numéricos contínuos e você cria um modelo de árvore de decisão, cada coluna de dados contínuos é compartimentalizada automaticamente, dependendo da distribuição dos dados. Para controlar o modo como os dados são diferenciados, altere as propriedades na coluna da estrutura de mineração que controla como os dados são usados no modelo.  
  
 Para obter informações gerais sobre como definir as propriedades em um modelo de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>Para exibir as propriedades para uma coluna do modelo de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, clique com o botão direito do mouse no cabeçalho da coluna que contém o nome do modelo de mineração ou na linha da grade que contém o nome do algoritmo de mineração e selecione **Propriedades**.  
  
     A janela **Propriedades** exibe as propriedades que são associadas com o modelo de mineração.  
  
2.  Na coluna **Estrutura** próxima ao lado esquerdo da tela, clique na coluna que contém os dados numéricos contínuos que você deseja diferenciar.  
  
     A janela **Propriedades** altera para exibir apenas as propriedades associadas com aquela coluna.  
  
### <a name="to-change-the-discretization-method"></a>Para alterar o método de diferenciação  
  
1.  Na janela **Propriedades de Mineração** , clique na caixa de texto próxima a **Conteúdo**e selecione **Discretized** na lista suspensa.  
  
     A janela <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> agora estão habilitadas.  
  
2.  Na guia **Propriedades** , clique na caixa de texto próxima a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> e selecione os seguintes valores: **Automatic**, **EqualAreas**ou **Cluster**.  
  
    > [!NOTE]  
    >  Se o uso da coluna for definido como **Ignorar**, a janela **Propriedades** da coluna ficará em branco.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
3.  Na guia **Propriedades** , clique na caixa de texto próxima a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> e digite um valor numérico.  
  
    > [!NOTE]  
    >  Se alterar essas propriedades, a estrutura deve ser reprocessada juntamente com quaisquer modelos no quais você queira usar a nova configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais e tarefas do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
