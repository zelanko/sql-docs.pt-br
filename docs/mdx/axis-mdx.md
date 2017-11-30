---
title: Eixo (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: AXIS
dev_langs: kbMDX
helpviewer_keywords: Axis function
ms.assetid: a3a60a1e-e266-4fa1-ae13-bae73544de33
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f53246e6442f7aebc60bea3a4ccbdecd7423e60d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="axis-mdx"></a>Axis (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
