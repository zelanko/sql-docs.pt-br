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
manager: kfile
ms.openlocfilehash: cdc4b2d3e948f0123eb15e38a6140e63009907bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187670"
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
  
  
