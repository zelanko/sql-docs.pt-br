---
title: Raiz (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: be687d5cbfd4fdbb706ef5c10778a4f3e3f93197
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037042"
---
# <a name="root-mdx"></a>Root (MDX)


  Retorna uma tupla que consiste em **todos** os membros de cada hierarquia de atributo dentro do escopo atual em um cubo, dimensão ou tupla. Para obter mais informações sobre escopo, consulte [instrução scope &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Se uma hierarquia de atributo não tiver um membro **All** , a tupla conterá o membro padrão para essa hierarquia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Name*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de dimensão.  
  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
## <a name="remarks"></a>Comentários  
 Se nem um nome de dimensão nem uma expressão de tupla forem especificados, a função **root** retornará uma tupla que contém o membro **All** (ou o membro padrão se o membro **All** não existir) de cada hierarquia de atributo no cubo. A ordem dos membros na tupla se baseia na sequência na qual as hierarquias de atributo são definidas no cubo.  
  
 Se um nome de dimensão for especificado, a função **root** retornará uma tupla que contém o membro **All** (ou o membro padrão se o membro **All** não existir) de cada hierarquia de atributo na dimensão especificada com base no contexto do membro atual. A ordem dos membros na tupla se baseia na sequência na qual as hierarquias de atributo são definidas na dimensão.  
  
> [!NOTE]  
>  Se um nome de hierarquia for especificado, a função de **tupla** escolherá o nome da dimensão do nome da hierarquia especificado.  
  
 Se uma expressão de tupla for especificada, a função **root** retornará uma tupla que contém a interseção da tupla especificada e **todos** os membros de todos os outros atributos de dimensão não explicitamente incluídos na tupla especificada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a tupla que contém o membro **All** (ou o padrão se o membro **All** não existir) de cada hierarquia no cubo Adventure Works.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna a tupla que contém o membro **All** (ou o padrão se o membro **All** não existir) de cada hierarquia na dimensão Date no cubo Adventure Works e o valor do membro especificado da dimensão Measures que cruza com esses membros padrão.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 O exemplo a seguir retorna a tupla que contém o membro de tupla especificado (1º de julho de 2001, juntamente com o membro **All** (ou o padrão se o membro **All** não existir) de cada hierarquia não especificada no cubo de data Dimension Adventure Works e o valor do membro especificado da dimensão Measures que cruza esses membros.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
