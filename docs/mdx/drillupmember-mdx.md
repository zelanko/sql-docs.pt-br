---
title: DrillupMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31981669d5d08e63a853b8daa530b886f9b7dfbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690761"
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)


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
 O **DrillupMember** função retorna um conjunto de membros com base nos membros especificados no primeiro conjunto que são descendentes de membros no segundo conjunto. O primeiro conjunto pode ter qualquer dimensionalidade, mas o segundo deve conter um conjunto unidimensional. A ordem é preservada entre os membros originais no primeiro conjunto. A função constrói o conjunto incluindo apenas aqueles membros do primeiro conjunto que sejam descendentes imediatos de membros do segundo conjunto. Se o ancestral imediato de um membro no primeiro conjunto não estiver presente no segundo conjunto, o membro no primeiro conjunto será incluído no conjunto retornado por essa função. Descendentes no primeiro conjunto que precedem um membro ancestral no segundo conjunto também são incluídos.  
  
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
  
 O exemplo dois mostra a importância de ordem do membro. Uma vez que **DrillupMember** faz drill up somente nos membros seguidos imediatamente por descendentes no primeiro conjunto, ele não fará drill up do membro Canadá. Canadá é separado de seus descendentes pelos Estados Unidos e pelo Colorado. Se você reordenar os membros para que o Canadá fique diretamente acima de Alberta, então Alberta e Brunswick serão excluídas do conjunto de linhas.  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
