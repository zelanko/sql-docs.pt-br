---
title: Instrução DROP CELL CALCULATION (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Calculation
- DROP
- DROP_CELL_CALCULATION
- CELL CALCULATION
- DROP CELL
- cell
- DROP CELL CALCULATION
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculations
- dropping calculations
- removing calculations
- DROP CELL CALCULATION statement
- calculations [SQL Server]
- cubes [Analysis Services], calculations
ms.assetid: 77caedf4-dd96-4eac-a5e4-fd82148a44a7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0286e36fb53ee35fdcc61af8c37c6915d7a8f906
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>Definição de dados MDX - DROP CELL CALCULATION
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [Criar instrução de CÁLCULO de CÉLULA & #40; MDX & #41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
