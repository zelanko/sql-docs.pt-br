---
title: Drilldownmemberbottom=1=«conjunto1 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 79bea49705c4f2fb66b8c9866be335433cbb783f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049262"
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)


  Faz uma busca detalhada dos membros de um determinado conjunto que estejam presentes em um segundo conjunto especificado, limitando o conjunto de resultado a um número especificado de membros. Alternativamente, essa função também faz uma busca detalhada em um conjunto de tuplas usando a primeira hierarquia de tuplas ou a hierarquia especificada opcionalmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
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
  
 *Hierarchy*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Recursiva*  
 Uma palavra-chave que indica comparação recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Uma palavra-chave para habilitar a ser incluído nos resultados da busca detalhada dos membros calculados.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, o **DrilldownMemberBottom** função classificará, em ordem crescente, os filhos de cada membro no primeiro conjunto, de acordo com o valor da expressão numérica, conforme avaliado sobre o conjunto de filho membros. Se não for especificada uma expressão numérica, a função classificará, em ordem crescente, os filhos de cada membro no primeiro conjunto de acordo com os valores das células representadas pelo conjunto de membros filho, conforme determinado pelo contexto da consulta. Este comportamento é semelhante às funções BottomCount e Tail (MDX), que retornam um conjunto de membros em ordem natural, sem qualquer classificação.  
  
 Depois da classificação, o **DrilldownMemberBottom** função retorna um conjunto que contém os membros pai e o número de membros filho, especificados na *contagem,* com o valor mais baixo e que estão contidos pelas duas define.  
  
 Se **RECURSIVA** for especificado, a função classificará o primeiro conjunto, conforme descrito anteriormente e, em seguida, compara recursivamente os membros do primeiro conjunto, conforme organizado em uma hierarquia, em relação ao segundo conjunto. A função recupera o número mais baixo dos filhos para cada membro no primeiro conjunto que também está presente no segundo conjunto.  
  
 O primeiro conjunto pode conter tuplas em vez de membros. Busca detalhada de tupla é uma extensão de OLE DB e retorna um conjunto de tuplas em vez de membros.  
  
 O **DrilldownMemberBottom** função é semelhante ao [DrilldownMember](../mdx/drilldownmember-mdx.md) funcionar, mas em vez de incluir todos os filhos de cada membro no primeiro conjunto que também está presente no segundo conjunto, o  **Drilldownmemberbottom=1=«conjunto1** função retorna o número mais baixo dos membros filho para cada membro.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; ver [propriedades XMLA com suporte &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
