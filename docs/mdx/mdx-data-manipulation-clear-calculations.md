---
title: Instrução CLEAR CALCULATIONS (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1b0766cb002960a96d702184ac9719abe7610afd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938029"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipulação de dados MDX – CLEAR CALCULATIONS


  Remove todos os cálculos do cubo e retorna o cubo para a análise de cálculo 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Expression*  
 Uma expressão de cubo da linguagem MDX válida.  
  
## <a name="remarks"></a>Comentários  
 O **FROM** cláusula pode ser omitida quando o contexto do cubo é conhecido, como em um script MDX.  
  
> [!NOTE]  
>  Essa instrução só pode ser executada por um administrador de banco de dados ou servidor ou por um membro de uma função que tenha acesso aos dados de origem no cubo (ou seja, ReadSourceData=true)  
  
## <a name="see-also"></a>Consulte também  
 [Instruções MDX de manipulação de dados &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
