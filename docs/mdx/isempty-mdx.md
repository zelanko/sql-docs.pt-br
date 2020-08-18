---
description: IsEmpty (MDX)
title: IsEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 504df180a15673ecb0982d5a70c2eea1e9f71d11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471858"
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
  
## <a name="remarks"></a>Comentários  
 A função **IsEmpty** retornará **true** se a expressão avaliada for um valor de célula vazio. Caso contrário, essa função retornará **false**.  
  
> [!NOTE]  
>  A propriedade padrão para um membro é o valor do membro.  
  
 A função **IsEmpty** é a única maneira de testar de forma confiável uma célula vazia, pois o valor da célula vazia tem um significado especial no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Se a avaliação da expressão de valor retornar um erro, a função retornará **false**. Uma expressão de valor pode retornar um erro, por exemplo, se uma referência de propriedades se referir a uma propriedade inválida ou não existente.  
  
 Para obter mais informações sobre células vazias, consulte a documentação OLE DB.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retornará TRUE se o Valor de Vendas pela Internet para o membro atual na hierarquia Fiscal da dimensão Data retornar uma célula vazia:  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com valores vazios](../mdx/working-with-empty-values.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
