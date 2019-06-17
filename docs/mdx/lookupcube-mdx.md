---
title: LookupCube (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8f8338a542bf9e15816205930704c45a536a5629
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208515"
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)


  Retorna o valor de uma expressão MDX (Multidimensional Expressions) avaliada em outro cubo especificado no mesmo banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que especifica o nome de um cubo.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida, geralmente uma expressão MDX válida de coordenadas de célula, que retorna uma cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, o **LookupCube** função avalia a expressão numérica especificada no cubo especificado e retorna o valor numérico resultante.  
  
 Se uma expressão de cadeia de caracteres for especificada, o **LookupCube** função avalia a expressão de cadeia de caracteres especificada no cubo especificado e retorna o valor de cadeia de caracteres resultante.  
  
 O **LookupCube** função funciona em cubos do mesmo banco de dados, como o cubo de origem no qual a consulta MDX que contém o **LookupCube** função está em execução.  
  
> [!IMPORTANT]  
>  Você deve fornecer todos os membros atuais necessários na expressão numérica ou de cadeia de caracteres porque o contexto da consulta atual não contém o cubo que está sendo consultado.  
  
 Qualquer cálculo usando o **LookupCube** função é provavelmente sofrerá um desempenho insatisfatório. Em vez de usar essa função, considere a recriação da solução de forma que todos os dados de que você precisa estejam presentes em um cubo.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir demonstra o uso de LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
