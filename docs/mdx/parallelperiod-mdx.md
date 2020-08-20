---
description: Função ParallelPeriod (MDX)
title: ParallelPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c8a6c91bae50ca06be46926f34de172e424e613
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471718"
---
# <a name="parallelperiod-mdx"></a>Função ParallelPeriod (MDX)


  Retorna um membro de um período anterior na mesma posição relativa como um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Index*  
 Uma expressão numérica válida que especifica o número de períodos paralelos a serem atrasados.  
  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Embora seja semelhante à função [primo](../mdx/cousin-mdx.md) , a função **ParallelPeriod** está mais bem relacionada à série temporal. A função **ParallelPeriod** usa o ancestral do membro especificado no nível especificado, localiza o irmão do ancestral com o retardo especificado e, finalmente, retorna o período paralelo do membro especificado entre os descendentes do irmão.  
  
 A função **ParallelPeriod** tem os seguintes padrões:  
  
-   Se nenhuma expressão de nível nem uma expressão de membro for especificada, o valor do membro padrão será o membro atual da primeira hierarquia na primeira dimensão com um tipo de *tempo* no grupo de medidas.  
  
-   Se uma expressão de nível for especificada, mas uma expressão de membro não for especificada, o valor de membro padrão será *Level_Expression*. **Hierarchy. CurrentMember**.  
  
-   O valor de índice padrão é 1.  
  
-   O nível padrão é o nível do pai do membro especificado.  
  
 A função **ParallelPeriod** é equivalente à seguinte instrução MDX:  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o período paralelo para o mês de outubro de 2003 com um atraso de três períodos, com base no nível do trimestre, que retorna o mês de janeiro de 2003.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna o período paralelo para o mês de outubro de 2003 com um atraso de três períodos, com base no nível do semestre, que retorna o mês de abril de 2002.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
