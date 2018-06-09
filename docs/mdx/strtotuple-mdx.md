---
title: StrToTuple (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35cd9cf849ce35bf82c839f0bbeeb657a75e990c
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743225"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  Retorna a tupla especificada por uma cadeia de caracteres formatada em linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Specification*  
 Uma expressão de cadeia de caracteres válida especificando, direta ou indiretamente, uma tupla.  
  
## <a name="remarks"></a>Remarks  
 O **StrToTuple** função retorna o conjunto especificado. O **StrToTuple** função geralmente é usada com funções definidas pelo usuário para retornar uma especificação de tupla de uma função externa para uma instrução MDX.  
  
-   Quando o sinalizador CONSTRAINED for usado, a especificação de tupla deverá conter nomes de membros qualificados ou não qualificados. Esse sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma cadeia de caracteres fornecida não for totalmente resolvida para nomes de membros qualificados ou não qualificados, surge o seguinte erro: "As restrições impostas pelo sinalizador CONSTRAINED na função STRTOVALUE foram violadas".  
  
-   Quando o sinalizador CONSTRAINED não for usado, a tupla especificada pode ser resolvida como uma expressão MDX que retorna uma tupla.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para o membro Bayern para o ano fiscal de 2004. A especificação de tupla fornecida contém uma linguagem de tupla MDX válida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para o membro Bayern para o ano fiscal de 2004. A especificação de tupla fornecida contém nomes de membros qualificados, conforme exigido pelo sinalizador CONSTRAINED.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para o membro Bayern para o ano fiscal de 2004. A especificação de tupla fornecida contém uma linguagem de tupla MDX válida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna um erro devido ao sinalizador CONSTRAINED. Enquanto a especificação de tupla fornecida contém uma linguagem de tupla MDX válida, o sinalizador CONSTRAINED exige nomes de membros qualificados ou não qualificados na especificação de tupla.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
