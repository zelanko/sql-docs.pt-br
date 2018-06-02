---
title: Função ParallelPeriod (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cde031af19fff309520cd72e145b6c04dc19d9c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580818"
---
# <a name="parallelperiod-mdx"></a>Função ParallelPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 Embora seja similar do [primo](../mdx/cousin-mdx.md) função, o **ParallelPeriod** função está mais relacionada à série temporal. O **ParallelPeriod** função aproveita o ancestral do membro especificado no nível especificado, encontra o irmão do ancestral com a latência especificada e, finalmente, retorna o período paralelo do membro especificado entre os descendentes do irmão.  
  
 O **ParallelPeriod** função tem os seguintes padrões:  
  
-   Se nem uma expressão de nível nem uma expressão de membro for especificada, o valor do membro padrão será o membro atual da primeira hierarquia na primeira dimensão com um tipo de *tempo* no grupo de medidas.  
  
-   Se uma expressão de nível for especificada, mas uma expressão de membro não for especificada, o valor do membro padrão é *Level_Expression*. **Hierarchy.CurrentMember**.  
  
-   O valor de índice padrão é 1.  
  
-   O nível padrão é o nível do pai do membro especificado.  
  
 O **ParallelPeriod** função é equivalente à instrução MDX a seguir:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
