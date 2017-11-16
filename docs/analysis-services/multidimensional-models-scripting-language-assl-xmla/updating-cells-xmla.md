---
title: "Atualizando células (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57edea50d67fa52de99f92b85b40bcd5caf307fb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando para alterar o valor de uma ou mais células em um cubo habilitado para write-back de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena as informações atualizadas em uma tabela de write-back separada para cada partição que contém células a serem atualizadas.  
  
> [!NOTE]  
>  O **UpdateCells** comando não oferece suporte a alocações durante o write-back de cubo. Para usar o write-back alocado, você deve usar o [instrução](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando para enviar uma instrução UPDATE de MDX (Multidimensional Expressions). Para obter mais informações, consulte [instrução UPDATE CUBE &#40; MDX &#41; ](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Especificando células  
 O [célula](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) propriedade o **UpdateCells** comando contém as células a serem atualizadas. Identifica cada célula no **célula** propriedade usando um número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera células em um cubo como se o cubo for um *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "fórmula para calcular a posição ordinal da célula")  
  
 Quando você souber o número ordinal de uma célula, você pode indicar o valor desejado da célula no [valor](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md) propriedade o [célula](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

