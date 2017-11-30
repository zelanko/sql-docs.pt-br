---
title: IsEmpty (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ISEMPTY
dev_langs: kbMDX
helpviewer_keywords: IsEmpty function
ms.assetid: b4a50996-61d1-4e23-8003-7d530195ea72
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c012af7c0df0ccc2507fb41097b9bcf58b97739c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna se a expressão avaliada for o valor de célula vazio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Value_Expression*  
 Uma linguagem MDX válida que retorna tipicamente as coordenadas de célula de um membro ou uma tupla.  
  
## <a name="remarks"></a>Comentários  
 O **IsEmpty** função retorna **true** se a expressão avaliada for um valor de célula vazia. Caso contrário, essa função retorna **false**.  
  
> [!NOTE]  
>  A propriedade padrão para um membro é o valor do membro.  
  
 O **IsEmpty** função é a única maneira de testar confiavelmente uma célula vazia porque o valor de célula vazia tem um significado especial [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
