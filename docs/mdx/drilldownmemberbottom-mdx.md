---
title: DrilldownMemberBottom (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DRILLDOWNMEMBERBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownMemberBottom function
ms.assetid: 603927ba-68f6-4e7a-b17f-44cad33bdfb0
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: d32b801dddb85255ad01b827071e5bc325f23a49
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 *Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Recursiva*  
 Uma palavra-chave que indica comparação recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Uma palavra-chave para habilitar os membros calculados a serem incluídas nos resultados da busca detalhada.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão numérica for especificada, o **DrilldownMemberBottom** função classificará, em ordem crescente, os filhos de cada membro no primeiro conjunto, de acordo com o valor da expressão numérica, conforme avaliado sobre o conjunto de membros filho. Se não for especificada uma expressão numérica, a função classificará, em ordem crescente, os filhos de cada membro no primeiro conjunto de acordo com os valores das células representadas pelo conjunto de membros filho, conforme determinado pelo contexto da consulta. Este comportamento é semelhante às funções BottomCount e Tail (MDX), que retornam um conjunto de membros em ordem natural, sem qualquer classificação.  
  
 Depois da classificação, o **DrilldownMemberBottom** função retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem,* com o valor mais baixo e que estão contidos em ambos os conjuntos.  
  
 Se **RECURSIVA** for especificado, a função classificará o primeiro conjunto, conforme descrito anteriormente, em seguida, compara recursivamente os membros do primeiro conjunto, conforme organizado em uma hierarquia, em relação ao segundo conjunto. A função recupera o número mais baixo dos filhos para cada membro no primeiro conjunto que também está presente no segundo conjunto.  
  
 O primeiro conjunto pode conter tuplas em vez de membros. Busca detalhada de tupla é uma extensão de OLE DB e retorna um conjunto de tuplas em vez de membros.  
  
 O **DrilldownMemberBottom** função é semelhante ao [DrilldownMember](../mdx/drilldownmember-mdx.md) funcionarão, mas em vez de incluir todos os filhos de cada membro no primeiro conjunto que também está presente no segundo conjunto, o **DrilldownMemberBottom** função retorna o número mais baixo de membros filho para cada membro.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; consulte [propriedades com suporte do XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obter detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
