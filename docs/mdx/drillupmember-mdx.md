---
title: DrillupMember (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLUPMEMBER
dev_langs: kbMDX
helpviewer_keywords: DrillupMember function
ms.assetid: debcd966-ea4e-4ecf-8600-0a4d346d03f8
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 45840536ffa58ac62a5961338a8b0902eebb8e2b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os membros em um conjunto especificado não descendentes de membros em um segundo conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 O **DrillupMember** retorna um conjunto de membros com base nos membros especificados no primeiro conjunto de descendentes de membros no segundo conjunto. O primeiro conjunto pode ter qualquer dimensionalidade, mas o segundo deve conter um conjunto unidimensional. A ordem é preservada entre os membros originais no primeiro conjunto. A função constrói o conjunto incluindo apenas aqueles membros do primeiro conjunto que sejam descendentes imediatos de membros do segundo conjunto. Se o ancestral imediato de um membro no primeiro conjunto não estiver presente no segundo conjunto, o membro no primeiro conjunto será incluído no conjunto retornado por essa função.  Descendentes no primeiro conjunto que precedem um membro ancestral no segundo conjunto também são incluídos.  
  
 O primeiro conjunto pode conter tuplas em vez de membros. Busca detalhada de tupla é uma extensão de OLE DB e retorna um conjunto de tuplas em vez de membros.  
  
> [!IMPORTANT]  
>  Um membro será buscado somente se for seguido imediatamente por um filho ou um descendente. A ordem dos membros do conjunto é importante para a busca detalhada\* e Drillup\* famílias de funções. Considere o uso de **Hierarchize** função ordenar adequadamente os membros do primeiro conjunto.  
  
## <a name="example"></a>Exemplo  
 Os três exemplos a seguir são idênticos, exceto o segundo conjunto. No primeiro exemplo, o segundo conjunto são os Estados Unidos. Como resultado, Colorado é excluído do conjunto de resultados. É um descendente dos Estados Unidos.  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 O exemplo dois mostra a importância de ordem do membro. Como **DrillupMember** faz drill up somente nos membros seguidos imediatamente por descendentes no primeiro conjunto, ele não fará drill up do membro Canadá. Canadá é separado de seus descendentes pelos Estados Unidos e pelo Colorado. Se você reordenar os membros para que o Canadá fique diretamente acima de Alberta, então Alberta e Brunswick serão excluídas do conjunto de linhas.  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 Exemplo três mostra como o uso de **Hierarchize** pode reduzir os efeitos de ordem de membro e fazer o drill up do membro Canadá.  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
