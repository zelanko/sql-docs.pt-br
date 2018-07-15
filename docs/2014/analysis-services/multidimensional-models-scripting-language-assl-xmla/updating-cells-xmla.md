---
title: Atualizando células (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d1b25b30623ddcdfe4c21442d15fd0cfa0966cc6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275972"
---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o [UpdateCells](../xmla/xml-elements-commands/updatecells-element-xmla.md) comando para alterar o valor de uma ou mais células em um cubo habilitado para write-back de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena as informações atualizadas em uma tabela de write-back separada para cada partição que contém células a serem atualizadas.  
  
> [!NOTE]  
>  O comando `UpdateCells` não oferece suporte a alocações durante o write-back de cubo. Para usar o write-back alocado, você deve usar o [instrução](../xmla/xml-elements-commands/statement-element-xmla.md) comando para enviar uma instrução UPDATE do MDX (Multidimensional Expressions). Para obter mais informações, consulte [instrução UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificando células  
 O [célula](../xmla/xml-elements-properties/cell-element-xmla.md) propriedade do `UpdateCells` comando contém as células a serem atualizadas. Você identifica cada célula na propriedade `Cell` que usa o número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera células em um cubo, como se o cubo for um *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "fórmula para calcular a posição ordinal da célula")  
  
 Quando você souber o número ordinal de uma célula, você pode indicar o valor pretendido da célula na [valor](../xmla/xml-elements-properties/value-element-xmla.md) propriedade da [célula](../xmla/xml-elements-properties/cell-element-xmla.md) propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/update-element-xmla.md)   
 [Desenvolvendo com XMLA no Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
