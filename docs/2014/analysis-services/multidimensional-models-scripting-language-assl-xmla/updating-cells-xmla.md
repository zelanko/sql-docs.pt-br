---
title: Atualizando células (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6237bb773709aa7f5eb8bc29fa2436bf69b08030
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146031"
---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comando para alterar o valor de uma ou mais células em um cubo habilitado para write-back de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena as informações atualizadas em uma tabela de write-back separada para cada partição que contém células a serem atualizadas.  
  
> [!NOTE]  
>  O comando `UpdateCells` não oferece suporte a alocações durante o write-back de cubo. Para usar o write-back alocado, você deve usar o [instrução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando para enviar uma instrução UPDATE do MDX (Multidimensional Expressions). Para obter mais informações, consulte [instrução UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificando células  
 O [célula](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propriedade do `UpdateCells` comando contém as células a serem atualizadas. Você identifica cada célula na propriedade `Cell` que usa o número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera células em um cubo, como se o cubo for um *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "fórmula para calcular a posição ordinal da célula")  
  
 Quando você souber o número ordinal de uma célula, você pode indicar o valor pretendido da célula na [valor](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) propriedade da [célula](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
