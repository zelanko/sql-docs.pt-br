---
title: Instrução DROP CELL CALCULATION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 509717221a51ac790b92969ff052d0a8a5d0143d
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741455"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>Definição de dados MDX - DROP CELL CALCULATION


  Remove o cálculo de célula especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome de uma expressão de cubo.  
  
 *CellCalc_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do cálculo de célula a ser descartado.  
  
## <a name="see-also"></a>Consulte também  
 [Instrução CREATE CELL CALCULATION &#40;MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
