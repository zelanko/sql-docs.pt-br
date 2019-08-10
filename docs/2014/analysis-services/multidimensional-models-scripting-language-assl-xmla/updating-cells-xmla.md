---
title: Atualizando células (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 71279981c5fd3879d633e0fdd8cdec74bed6deac
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887705"
---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) para alterar o valor de uma ou mais células em um cubo habilitado para Write-back de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenaasinformaçõesatualizadasemumatabeladewrite-backseparadaparacadapartiçãoquecontémcélulas[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a serem atualizadas.  
  
> [!NOTE]  
>  O comando `UpdateCells` não oferece suporte a alocações durante o write-back de cubo. Para usar write-back alocado, você deve usar o comando de [instrução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) para enviar uma instrução de atualização MDX (Multidimensional Expressions). Para obter mais informações, consulte [Update Cube &#40;Statement&#41;MDX](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificando células  
 A propriedade [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) do `UpdateCells` comando contém as células a serem atualizadas. Você identifica cada célula na propriedade `Cell` que usa o número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera as células de um cubo como se o cubo fosse uma matriz *p*-dimensional, em que *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/cellordinalformula.gif "Fórmula para calcular a posição ordinal da célula")  
  
 Depois de saber o número ordinal de uma célula, você pode indicar o valor pretendido da célula na propriedade [Value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) da propriedade [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) .  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o &#40;elemento XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
