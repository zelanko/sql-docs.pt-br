---
title: Raiz (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8dd99d852ab33088d4af6df9bd06386b0e8877ab
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580728"
---
# <a name="root-mdx"></a>Root (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna uma tupla que consiste o **todos os** membros de cada hierarquia de atributo dentro do escopo atual em um cubo, dimensão ou tupla. Para obter mais informações sobre escopo, consulte [instrução SCOPE &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Se uma hierarquia de atributo não tem um **todos os** membro, tupla contém o membro padrão para a hierarquia.  
  
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
  
## <a name="remarks"></a>Remarks  
 Se nenhum nome de dimensão ou uma expressão de tupla for especificada, o **raiz** função retorna uma tupla que contém o **todos os** membro (ou o membro padrão se o **todos os** membro não existir) de cada hierarquia de atributo no cubo. A ordem dos membros na tupla se baseia na sequência na qual as hierarquias de atributo são definidas no cubo.  
  
 Se um nome de dimensão for especificado, o **raiz** função retorna uma tupla que contém o **todos os** membro (ou o membro padrão se o **todos os** membro não existir) de cada hierarquia de atributo na dimensão especificada com base no contexto do membro atual. A ordem dos membros na tupla se baseia na sequência na qual as hierarquias de atributo são definidas na dimensão.  
  
> [!NOTE]  
>  Se um nome de hierarquia for especificado, o **tupla** função escolherá o nome da dimensão do nome da hierarquia especificada.  
  
 Se uma expressão de tupla for especificada, o **raiz** função retorna uma tupla que contém a interseção da tupla especificada e o **todos os** membros de todos os outros atributos de dimensão não incluídos explicitamente na tupla especificada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a tupla que contém o **todos os** membro (ou o padrão se o **todos os** membro não existir) de cada hierarquia no cubo Adventure Works.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna a tupla que contém o **todos os** membro (ou o padrão se o **todos os** membro não existir) de cada hierarquia na dimensão data no cubo Adventure Works e o valor do membro especificado da dimensão de medidas que faz interseção com esses membros padrão.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 O exemplo a seguir retorna a tupla que contém o membro da tupla especificado (1º de julho de 2001, junto com o **todos os** membro (ou o padrão se o **todos os** membro não existir) de cada hierarquia não especificada na data dimensão cubo Adventure Works e o valor do membro especificado da dimensão de medidas que faz interseção com esses membros.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
