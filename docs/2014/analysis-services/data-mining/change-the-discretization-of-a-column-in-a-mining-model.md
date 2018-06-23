---
title: Alterar a diferenciação de uma coluna em um modelo de mineração | Microsoft Docs
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
- discretization [Analysis Services]
- mining structures [Analysis Services], how-to topics
- discretized columns [data mining]
- bucketing problems [Analysis Services]
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cc0352074e37bf284bd4ea033bae759638e040a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012394"
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>Alterar a diferenciação de uma coluna em um modelo de mineração
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] discretiza automaticamente valores, ou seja, compartimentaliza dados na coluna numérica em determinados cenários. Por exemplo, se seus dados contêm dados numéricos contínuos e você cria um modelo de árvore de decisão, cada coluna de dados contínuos é compartimentalizada automaticamente, dependendo da distribuição dos dados. Para controlar o modo como os dados são diferenciados, altere as propriedades na coluna da estrutura de mineração que controla como os dados são usados no modelo.  
  
 Para obter informações gerais sobre como definir as propriedades em um modelo de mineração, consulte [Colunas do modelo de mineração](mining-model-columns.md).  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>Para exibir as propriedades para uma coluna do modelo de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados, clique com o botão direito do mouse no cabeçalho da coluna que contém o nome do modelo de mineração ou na linha da grade que contém o nome do algoritmo de mineração e selecione **Propriedades**.  
  
     A janela **Propriedades** exibe as propriedades que são associadas com o modelo de mineração.  
  
2.  Na coluna **Estrutura** próxima ao lado esquerdo da tela, clique na coluna que contém os dados numéricos contínuos que você deseja diferenciar.  
  
     A janela **Propriedades** altera para exibir apenas as propriedades associadas com aquela coluna.  
  
### <a name="to-change-the-discretization-method"></a>Para alterar o método de diferenciação  
  
1.  No **propriedades de mineração** janela, clique na caixa de texto ao lado **conteúdo**e selecione `Discretized` na lista suspensa.  
  
     A janela <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> agora estão habilitadas.  
  
2.  No **propriedades** janela, clique na caixa de texto ao lado <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> e selecione um dos seguintes valores: `Automatic`, `EqualAreas`, ou `Cluster`.  
  
    > [!NOTE]  
    >  Se o uso da coluna é definido como `Ignore`, o **propriedades** janela para a coluna está em branco.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
3.  Na guia **Propriedades** , clique na caixa de texto próxima a <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> e digite um valor numérico.  
  
    > [!NOTE]  
    >  Se alterar essas propriedades, a estrutura deve ser reprocessada juntamente com quaisquer modelos no quais você queira usar a nova configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)  
  
  