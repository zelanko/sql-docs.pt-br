---
title: Eixo (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa65c1531be29273c0a838b978109bbd1c8a2b18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016983"
---
# <a name="axis-mdx"></a>Axis (MDX)


  Retorna o conjunto de tuplas em um eixo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Axis_Number*  
 Uma expressão numérica válida que especifica o número de eixos.  
  
## <a name="remarks"></a>Comentários  
 O **eixo** função usa a posição de base zero de um eixo para retornar o conjunto de tuplas em um eixo. Por exemplo, `Axis(0)` retorna o eixo COLUMNS, `Axis(1)` retorna o eixo ROWS e assim por diante. O **eixo** função não pode ser usada no eixo do filtro. Esta função pode ser usada para que os membros calculados conheçam o contexto da consulta que está sendo executada. Por exemplo, você talvez precise de um membro calculado que fornece a soma somente dos membros selecionados no eixo Linhas. Também pode ser usada para fazer que a definição de um eixo dependa da definição de outro. Por exemplo, ordenando o conteúdo do eixo Linhas de acordo com o valor do primeiro item no eixo Colunas.  
  
> [!NOTE]  
>  Um eixo pode fazer referência apenas a um eixo anterior. Por exemplo, `Axis(0)` deve ocorrer depois do eixo COLUMNS ter sido avaliado, como em um eixo ROW ou PAGE.  
  
## <a name="examples"></a>Exemplos  
 A consulta de exemplo a seguir mostra como usar a função Axis:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 O exemplo a seguir mostra o uso da função Axis dentro de um membro calculado:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
