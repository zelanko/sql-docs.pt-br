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
manager: kfile
ms.openlocfilehash: 652afb0595634d7fb4474ed9042edda26f83a52a
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147301"
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
 (Opcional). Uma palavra-chave que indica comparação recursiva de conjuntos. O **ToggleDrillState** função é uma combinação da **DrillupMember** e **DrilldownMember** funções. Recursão só se aplica quando o membro se encontra o **DrilldownMember** estado.  
  
 *Include_calc_members*  
 (Opcional). Um sinalizador que indica se deve-se incluir membros calculados, caso existam, no nível de drill down.  
  
## <a name="remarks"></a>Comentários  
 O **ToggleDrillState** função alterna o estado de busca de cada membro do segundo conjunto que está presente no primeiro conjunto. O primeiro conjunto pode conter tuplas com qualquer dimensionalidade, mas o segundo deve conter membros de uma única dimensão. O **ToggleDrillState** função é uma combinação da **DrillupMember** e **DrilldownMember** funções. Se o membro *m*, do segundo conjunto estiver presente no primeiro conjunto e que o membro for buscado (ou seja, tiver um descendente imediatamente após ele), em seguida, `DrillupMember(Set_Expression1, {m})` é aplicado no membro ou na tupla no primeiro conjunto. Se esse *m* membro for buscado (ou seja, não há nenhum descendente de *m* imediatamente após *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` é aplicado ao primeiro conjunto.  
  
 Se o opcional **RECURSIVA** sinalizador é usado, fazer drill up e fazer drill down são aplicadas recursivamente. Para obter mais informações sobre o sinalizador recursivo, consulte o [DrillupMember](../mdx/drillupmember-mdx.md) e [DrilldownMember](../mdx/drilldownmember-mdx.md) funções.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; ver [propriedades XMLA com suporte &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
 Ver [diário do banco de dados: funções de conjunto MDX: A função de toggledrillstate ()](http://go.microsoft.com/fwlink/?LinkId=517759) para cenários e exemplos que envolvem essa função.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
