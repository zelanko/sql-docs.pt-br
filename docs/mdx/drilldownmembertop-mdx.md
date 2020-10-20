---
description: DrilldownMemberTop (MDX)
title: DrilldownMemberTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d90c382ca34316225760c1a25288034ba26ab726
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193499"
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
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Recursiva*  
 Uma palavra-chave que indica comparação recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Uma palavra-chave para habilitar membros calculados a serem incluídos nos resultados de busca detalhada.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, a função **DrilldownMemberTop** classificará, em ordem decrescente, os filhos de cada membro no primeiro conjunto de acordo com o valor da expressão numérica, conforme avaliado sobre o conjunto de membros filho. Se não for especificada uma expressão numérica, a função classificará, em ordem decrescente, os filhos de cada membro no primeiro conjunto de acordo com os valores das células representadas pelo conjunto de membros filho, conforme determinado pelo contexto da consulta. Este comportamento é semelhante às funções TopCount e Head (MDX), que retornam um conjunto de membros em ordem natural, sem qualquer classificação.  
  
 Após a classificação, a função **DrilldownMemberTop** retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem,* com o valor mais alto e estão contidos em ambos os conjuntos.  
  
 Se **recursivo** for especificado, a função classifica o primeiro conjunto conforme descrito anteriormente e, em seguida, compara recursivamente os membros do primeiro conjunto, conforme organizado em uma hierarquia, no segundo conjunto. A função recupera o número mais alto de filhos para cada membro no primeiro conjunto que também está presente no segundo conjunto.  
  
 O primeiro conjunto pode conter tuplas em vez de membros. O detalhamento de tupla é uma extensão de OLE DB e retorna um conjunto de tuplas em vez de membros.  
  
 A função **DrilldownMemberTop** é semelhante à função [DrilldownMember](../mdx/drilldownmember-mdx.md) , mas em vez de incluir todos os filhos de cada membro no primeiro conjunto que também está presente no segundo conjunto, a função **DrilldownMemberTop** retorna o número mais alto de membros filho para cada membro.  
  
 Consultar a propriedade XMLA MdpropMdxDrillFunctions permite que você verifique o nível de suporte que o servidor fornece para as funções de análise; consulte [Propriedades XMLA com suporte &#40;&#41;XMLA ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
