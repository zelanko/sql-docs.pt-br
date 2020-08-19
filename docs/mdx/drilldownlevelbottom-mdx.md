---
description: DrilldownLevelBottom (MDX)
title: DrilldownLevelBottom (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d77e40e322ab3489070061b1fc466f2e212ba36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483989"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


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
 Se uma expressão numérica for especificada, a função **DrilldownLevelBottom** classificará, em ordem crescente, os filhos de cada membro no conjunto especificado, de acordo com o valor especificado, conforme avaliado sobre o conjunto de membros filho. Se uma expressão numérica não for especificada, a função classificará, em ordem crescente, os filhos de cada membro no conjunto especificado, de acordo com os valores das células representados pelo conjunto de membros filho, como determinados pelo contexto de consulta; esse comportamento é semelhante às funções BottomCount e Tail (MDX), que retornam um conjunto de membros em ordem natural, sem qualquer classificação.  
  
 Após a classificação, a função **DrilldownLevelBottom** retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem*, com o menor valor.  
  
 A função **DrilldownLevelBottom** é semelhante à função [DrilldownLevel](../mdx/drilldownlevel-mdx.md) , mas em vez de incluir todos os filhos de cada membro no nível especificado, a função **DrilldownLevelBottom** retorna o número mais baixo de membros filho.  
  
 Consultar a propriedade XMLA MdpropMdxDrillFunctions permite que você verifique o nível de suporte que o servidor fornece para as funções de análise; consulte [Propriedades XMLA com suporte &#40;&#41;XMLA ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
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
  
 O exemplo a seguir ilustra o uso do sinalizador **include_calc_members** , usado para incluir membros calculados no nível de busca detalhada. A medida [contagem de pedidos do revendedor] é adicionada à instrução **DrilldownLevelBottom** para garantir que os resultados sejam classificados por essa medida. Para ver o membro calculado, é necessário aumentar a Contagem para pelo menos 9.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [DrilldownLevel&#41;MDX &#40;](../mdx/drilldownlevel-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
