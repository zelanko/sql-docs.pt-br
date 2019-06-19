---
title: Atualizando células (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0cfee2adf9d730b458fd482317d16d963f15ebc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262173"
---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comando para alterar o valor de uma ou mais células em um cubo habilitado para write-back de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena as informações atualizadas em uma tabela de write-back separada para cada partição que contém células a serem atualizadas.  
  
> [!NOTE]  
>  O **UpdateCells** comando não dá suporte a alocações durante o write-back de cubo. Para usar o write-back alocado, você deve usar o [instrução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando para enviar uma instrução UPDATE do MDX (Multidimensional Expressions). Para obter mais informações, consulte [instrução UPDATE CUBE &#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Especificando células  
 O [célula](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propriedade da **UpdateCells** comando contém as células a serem atualizadas. Identifica cada célula na **célula** propriedade usando um número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera células em um cubo, como se o cubo for um *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "fórmula para calcular a posição ordinal da célula")  
  
 Quando você souber o número ordinal de uma célula, você pode indicar o valor pretendido da célula na [valor](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) propriedade da [célula](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
