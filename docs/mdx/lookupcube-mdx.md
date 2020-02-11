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
ms.openlocfilehash: ec18b600c369de872df5f6eadf06ef6c30c88efa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098509"
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
 Se uma expressão numérica for especificada, a função **LookupCube** avaliará a expressão numérica especificada no cubo especificado e retornará o valor numérico resultante.  
  
 Se uma expressão de cadeia de caracteres for especificada, a função **LookupCube** avaliará a expressão de cadeia de caracteres especificada no cubo especificado e retornará o valor da cadeia de caracteres resultante.  
  
 A função **LookupCube** funciona em cubos no mesmo banco de dados que o cubo de origem no qual a consulta MDX que contém a função **LookupCube** está em execução.  
  
> [!IMPORTANT]  
>  Você deve fornecer todos os membros atuais necessários na expressão numérica ou de cadeia de caracteres porque o contexto da consulta atual não contém o cubo que está sendo consultado.  
  
 Qualquer cálculo usando a função **LookupCube** provavelmente sofrerá de baixo desempenho. Em vez de usar essa função, considere a recriação da solução de forma que todos os dados de que você precisa estejam presentes em um cubo.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir demonstra o uso de LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
