---
title: Alterar as propriedades de uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 56942ebc74e1a0b49303f842ec2668a46f6f209f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689344"
---
# <a name="change-the-properties-of-a-mining-structure"></a>Alterar as propriedades de uma estrutura de mineração
  Há dois tipos de propriedades em uma estrutura de mineração e ambos podem ser modificados:  
  
-   Propriedades da estrutura de mineração que afetam a estrutura inteira  
  
-   Propriedades em colunas individuais na estrutura  
  
 Note que algumas propriedades dependem de outras configurações de propriedade. Por exemplo, não é possível definir propriedades que controlam o comportamento de compartimentalização (como <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> ou <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>) até definir o tipo de dados da coluna como `Discretized`.  
  
 Para obter mais informações sobre as propriedades da estrutura de mineração, consulte [Colunas da estrutura de mineração](mining-structure-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>Para alterar as propriedades de uma estrutura de mineração  
  
1.  Na guia **Estrutura de Mineração** do Designer de Mineração de Dados, clique com o botão direito do mouse na estrutura de mineração ou em uma coluna na estrutura de mineração e selecione **Propriedades**.  
  
     A janela **Propriedades** será aberta no lado direito da tela se ela ainda não estiver visível.  
  
2.  Na janela **Propriedades** , selecione o valor que corresponde à propriedade que você quer alterar e insira o novo valor.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
  
