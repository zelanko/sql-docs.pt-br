---
title: LookupCube (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOOKUPCUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- LookupCube function
ms.assetid: 243fa101-328a-4016-86e0-d8b5977e15a9
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41aed2def9e470d39f006b314f51dbb61bf63b47
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 O **LookupCube** função funciona em cubos no mesmo banco de dados, como o cubo de origem no qual a consulta MDX que contém o **LookupCube** função está sendo executado.  
  
> [!IMPORTANT]  
>  Você deve fornecer todos os membros atuais necessários na expressão numérica ou de cadeia de caracteres porque o contexto da consulta atual não contém o cubo que está sendo consultado.  
  
 Qualquer cálculo usando o **LookupCube** função é provavelmente haverá um desempenho insatisfatório. Em vez de usar essa função, considere a recriação da solução de forma que todos os dados de que você precisa estejam presentes em um cubo.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir demonstra o uso de LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

