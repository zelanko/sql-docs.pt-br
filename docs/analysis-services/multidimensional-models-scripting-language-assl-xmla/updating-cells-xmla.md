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
ms.openlocfilehash: 1e886925621378aa5d01cc77a74edf0e1ea246cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando para alterar o valor de uma ou mais células em um cubo habilitado para write-back de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena as informações atualizadas em uma tabela de write-back separada para cada partição que contém células a serem atualizadas.  
  
> [!NOTE]  
>  O **UpdateCells** comando não oferece suporte a alocações durante o write-back de cubo. Para usar o write-back alocado, você deve usar o [instrução](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando para enviar uma instrução UPDATE de MDX (Multidimensional Expressions). Para obter mais informações, consulte [instrução UPDATE CUBE &#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Especificando células  
 O [célula](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) propriedade o **UpdateCells** comando contém as células a serem atualizadas. Identifica cada célula no **célula** propriedade usando um número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera células em um cubo como se o cubo for um *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "fórmula para calcular a posição ordinal da célula")  
  
 Quando você souber o número ordinal de uma célula, você pode indicar o valor desejado da célula no [valor](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md) propriedade o [célula](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
