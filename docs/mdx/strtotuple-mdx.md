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
ms.openlocfilehash: 054786440afaf2b7ab458b4704bd5f8e2e26c135
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136167"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  Retorna a tupla especificada por uma cadeia de caracteres formatada para MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Specification*  
 Uma expressão de cadeia de caracteres válida especificando, direta ou indiretamente, uma tupla.  
  
## <a name="remarks"></a>Comentários  
 O **StrToTuple** função retorna o conjunto especificado. O **StrToTuple** função normalmente é usada com funções definidas pelo usuário para retornar uma especificação de tupla de uma função externa para uma instrução MDX.  
  
-   Quando o sinalizador CONSTRAINED for usado, a especificação de tupla deverá conter nomes de membros qualificados ou não qualificados. Esse sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma cadeia de caracteres for fornecida que não é nomes de membros diretamente resolvido para qualificados ou não qualificados, surge o seguinte erro: "As restrições impostas pelo CONSTRAINED sinalizador na função STRTOVALUE foram violadas."  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
