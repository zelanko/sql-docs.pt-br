---
title: DrilldownLevelBottom (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLDOWNLEVELBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownLevelBottom function
ms.assetid: c00a6a02-e618-4713-805a-870e042f2d51
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9ff1ff6edc4bd145b29c1158c843ba8ae1642705
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Faz uma busca detalhada dos membros mais inferiores de um conjunto, em um nível especificado, para um nível abaixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Numeric_Expression*  
 Opcional. Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *Include_Calc_Members*  
 Opcional. Uma palavra-chave que adiciona membros calculados aos resultados da busca detalhada.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, o **DrilldownLevelBottom** função classificará, em ordem crescente, os filhos de cada membro no conjunto especificado, de acordo com o valor especificado, conforme avaliado sobre o conjunto de membros filho. Se uma expressão numérica não for especificada, a função classificará, em ordem crescente, os filhos de cada membro no conjunto especificado, de acordo com os valores das células representados pelo conjunto de membros filho, como determinados pelo contexto de consulta; esse comportamento é semelhante às funções BottomCount e Tail (MDX), que retornam um conjunto de membros em ordem natural, sem qualquer classificação.  
  
 Depois da classificação, o **DrilldownLevelBottom** função retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem*, com o menor valor.  
  
 O **DrilldownLevelBottom** função é semelhante ao [DrilldownLevel](../mdx/drilldownlevel-mdx.md) função, mas em vez de incluir todos os filhos de cada membro no nível especificado, o **DrilldownLevelBottom** função retorna o número mais baixo de membros filho.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; consulte [suporte para propriedades de XMLA &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obter detalhes.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os três filhos inferiores do nível Categoria do Produto, com base na medida padrão. No cubo de exemplo do Adventure Works, os três filhos inferiores de Acessórios são Pneus e tubos, Bombas e Alforjes. No Management Studio, na janela de consulta do MDX, você pode navegar para Produtos | Categorias de Produto | Membros | Todos os Produtos | Acessórios para exibir a lista completa. Você pode aumentar o argumento Contagem para retornar mais membros.  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 O exemplo a seguir ilustra o uso de **include_calc_members** sinalizador, usado para incluir membros calculados no nível de detalhamento. A medida [contagem dos pedidos do revendedor] é adicionada para o **DrilldownLevelBottom** instrução para garantir que os resultados são classificados por essa medida. Para ver o membro calculado, é necessário aumentar a Contagem para pelo menos 9.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [DrilldownLevel &#40; MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

