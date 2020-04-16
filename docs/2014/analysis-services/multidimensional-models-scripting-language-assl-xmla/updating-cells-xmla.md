---
title: Células de Atualização (XMLA) | Microsoft Docs
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
ms.openlocfilehash: f0eab50aa7e70aedee93eef2cefee648e6ceb5c9
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387886"
---
# <a name="updating-cells-xmla"></a>Atualizando células (XMLA)
  Você pode usar o comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) para alterar o valor de uma ou mais células em um cubo ativado para gravação de cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena as informações atualizadas em uma tabela de gravação separada para cada partição que contém células a serem atualizadas. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
> [!NOTE]  
>  O comando `UpdateCells` não oferece suporte a alocações durante o write-back de cubo. Para usar a gravação alocada, você deve usar o comando [Declaração](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) para enviar uma declaração UPDATE de Expressões Multidimensionais (MDX). Para obter mais informações, consulte [UPDATE CUBE Statement &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificando células  
 A [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propriedade Cell `UpdateCells` do comando contém as células a serem atualizadas. Você identifica cada célula na propriedade `Cell` que usa o número ordinal dessa célula. Conceitualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] as células numéricas em um cubo eram uma matriz *p-dimensional,* onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. A ilustração a seguir mostra a fórmula para o cálculo do número ordinal de uma célula.  
  
 ![Fórmula para calcular a posição ordinal da célula](../../analysis-services/dev-guide/media/cellordinalformula.gif "Fórmula para calcular a posição ordinal da célula")  
  
 Uma vez que você sabe o número ordinal de uma célula, você pode indicar o valor pretendido da célula na propriedade [Valor](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) da propriedade [Cell.](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento de atualização &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
