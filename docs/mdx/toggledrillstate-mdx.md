---
title: ToggleDrillState (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d027a76a82de3fd82b6c0c81c54ace08167039b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036614"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


  Alterna o estado de busca de membros entre os modos de busca detalhada e drillllup.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Recursiva*  
 (Opcional). Uma palavra-chave que indica comparação recursiva de conjuntos. A função **ToggleDrillState** é uma combinação das funções **DrillupMember** e **DrilldownMember** . A recursão só se aplica quando o membro está no estado **DrilldownMember** .  
  
 *Include_calc_members*  
 (Opcional). Um sinalizador que indica se deve-se incluir membros calculados, caso existam, no nível de drill down.  
  
## <a name="remarks"></a>Comentários  
 A função **ToggleDrillState** alterna o estado de análise de cada membro do segundo conjunto que está presente no primeiro conjunto. O primeiro conjunto pode conter tuplas com qualquer dimensionalidade, mas o segundo deve conter membros de uma única dimensão. A função **ToggleDrillState** é uma combinação das funções **DrillupMember** e **DrilldownMember** . Se o membro, *m*, do segundo conjunto estiver presente no primeiro conjunto e esse membro for resumido (ou seja, tiver um descendente imediatamente após ele), `DrillupMember(Set_Expression1, {m})` será aplicado ao membro ou à tupla no primeiro conjunto. Se esse membro *m* for drill up (ou seja, não há nenhum descendente de *m* que imediatamente segue *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` será aplicado ao primeiro conjunto.  
  
 Se o sinalizador **recursivo** opcional for usado, Drill up e Drill down serão aplicados recursivamente. Para obter mais informações sobre o sinalizador recursivo, consulte as funções [DrillupMember](../mdx/drillupmember-mdx.md) e [DrilldownMember](../mdx/drilldownmember-mdx.md) .  
  
 Consultar a propriedade XMLA MdpropMdxDrillFunctions permite que você verifique o nível de suporte que o servidor fornece para as funções de análise; consulte [Propriedades XMLA com suporte &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
 Consulte [diário de banco de dados: funções de conjunto MDX: a função ToggleDrillState ()](https://go.microsoft.com/fwlink/?LinkId=517759) para cenários e exemplos que envolvem essa função.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir faz uma busca detalhada no membro Austrália do primeiro conjunto e faz drill up no membro Estados Unidos do primeiro conjunto.  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
