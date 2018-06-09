---
title: IsEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dbed0eba3fec73d7134b1ce21275c28dbd387fcd
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740165"
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)


  Retorna se a expressão avaliada for o valor de célula vazio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Value_Expression*  
 Uma linguagem MDX válida que retorna tipicamente as coordenadas de célula de um membro ou uma tupla.  
  
## <a name="remarks"></a>Remarks  
 O **IsEmpty** função retorna **true** se a expressão avaliada for um valor de célula vazia. Caso contrário, essa função retorna **false**.  
  
> [!NOTE]  
>  A propriedade padrão para um membro é o valor do membro.  
  
 O **IsEmpty** função é a única maneira de testar confiavelmente uma célula vazia porque o valor de célula vazia tem um significado especial [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Se a avaliação da expressão de valor retorna um erro, a função retornará **false**. Uma expressão de valor pode retornar um erro, por exemplo, se uma referência de propriedades se referir a uma propriedade inválida ou não existente.  
  
 Para obter mais informações sobre células vazias, consulte a documentação OLE DB.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retornará TRUE se o Valor de Vendas pela Internet para o membro atual na hierarquia Fiscal da dimensão Data retornar uma célula vazia:  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com valores vazios](../mdx/working-with-empty-values.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
