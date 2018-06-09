---
title: DrilldownMemberTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f2e055d0d05d6c111b52d2f23f3248e96de11966
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740845"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  Faz uma busca detalhada dos membros de um determinado conjunto que estejam presentes em um segundo conjunto especificado, limitando o conjunto de resultado a um número especificado de membros. Alternativamente, essa função faz uma busca detalhada em um conjunto de tuplas usando a primeira hierarquia de tuplas ou a hierarquia especificada opcionalmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Contagem*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *Hierarchy*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Recursiva*  
 Uma palavra-chave que indica comparação recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Uma palavra-chave para habilitar os membros calculados a serem incluídas nos resultados da busca detalhada.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão numérica for especificada, o **DrilldownMemberTop** função classificará, em ordem decrescente, os filhos de cada membro no primeiro conjunto de acordo com o valor da expressão numérica, conforme avaliado sobre o conjunto de membros filho. Se não for especificada uma expressão numérica, a função classificará, em ordem decrescente, os filhos de cada membro no primeiro conjunto de acordo com os valores das células representadas pelo conjunto de membros filho, conforme determinado pelo contexto da consulta. Este comportamento é semelhante às funções TopCount e Head (MDX), que retornam um conjunto de membros em ordem natural, sem qualquer classificação.  
  
 Depois da classificação, o **DrilldownMemberTop** função retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem,* com o valor mais alto e que estão contidos em dois conjuntos.  
  
 Se **RECURSIVA** for especificado, a função classificará o primeiro conjunto, conforme descrito anteriormente, em seguida, compara recursivamente os membros do primeiro conjunto, conforme organizado em uma hierarquia, em relação ao segundo conjunto *.* A função recupera o número mais alto de filhos para cada membro no primeiro conjunto que também está presente no segundo conjunto.  
  
 O primeiro conjunto pode conter tuplas em vez de membros. Busca detalhada de tupla é uma extensão de OLE DB e retorna um conjunto de tuplas em vez de membros.  
  
 O **DrilldownMemberTop** função é semelhante ao [DrilldownMember](../mdx/drilldownmember-mdx.md) funcionarão, mas em vez de incluir todos os filhos de cada membro no primeiro conjunto que também está presente no segundo conjunto, o **DrilldownMemberTop** função retorna o número mais alto de membros filho para cada membro.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; consulte [propriedades com suporte do XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obter detalhes.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir faz um detalhamento na categoria de vestuário para retornar as três subcategorias de vestuário com a quantidade superior de pedidos enviados.  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
