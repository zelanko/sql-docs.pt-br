---
title: Propriedades (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c29d9b29078d6097b512acb93ff47eef018592c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278448"
---
# <a name="properties-mdx"></a>Properties (MDX)


  Retorna uma cadeia de caracteres ou um valor com rigidez de tipos que contém um valor de propriedade do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Property_Name*  
 Uma expressão de cadeia de caracteres válida de um nome de propriedade de membro.  
  
## <a name="remarks"></a>Comentários  
 O **propriedades** função retorna o valor do membro especificado para a propriedade do membro especificado. A propriedade do membro pode ser qualquer uma das propriedades intrínsecas do membro, como **nome**, **ID**, **chave**, ou **legenda**, ou pode ser um propriedade do membro definidas pelo usuário. Para obter mais informações, consulte [propriedades intrínsecas do membro &#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) e [propriedades do membro definidas pelo usuário &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 Por padrão, o valor é forçado a ser uma cadeia de caracteres. Se **TYPED** for especificado, o valor de retorno é fortemente tipado.  
  
-   Se o tipo de propriedade for intrínseco, a função retornará o tipo original de membro.  
  
-   Se o tipo de propriedade é definida pelo usuário, o tipo do valor de retorno é o mesmo que o tipo do valor de retorno de **MemberValue** função.  
  
> [!NOTE]  
>  Propriedades ('Key') retornam o mesmo resultado como Key0 com exceção de chaves compostas. Propriedades ('Key') retornarão nulo para chaves compostas. Use a tecla*x* sintaxe para chaves compostas, conforme ilustrado no exemplo. Propriedades ('Key0'), Propriedades ('Key1'), Propriedades ('Key2') etc. formam coletivamente a chave composta.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna propriedades de membro intrínsecas e definidas pelo usuário, utilizando o argumento TYPED para retornar o valor com rigidez de tipos para a propriedade de membro Dia Nome.  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir mostra o uso da chave*x* propriedade.  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usando propriedades do membro &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
