---
title: DrilldownLevelTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bdb07daea5b48ac2627f23d9149e590e1fe35b48
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971504"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  Faz uma busca detalhada dos principais membros de um conjunto, em um nível especificado, para um nível abaixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Count*  
 Uma expressão numérica válida que especifica o número de tuplas a ser retornado.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *Include_Calc_Members*  
 Uma palavra-chave para adicionar membros calculados para resultados da busca detalhada.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for especificada, a função **DrilldownLevelTop** classificará, em ordem decrescente, os filhos de cada membro no conjunto especificado de acordo com o valor da expressão numérica, conforme avaliado sobre o conjunto de membros filho. Se não for especificada uma expressão numérica, a função classificará, em ordem decrescente, os filhos de cada membro no conjunto especificado de acordo com os valores das células representadas pelo conjunto de membros filho, conforme determinado pelo contexto da consulta.  
  
 Após a classificação, a função **DrilldownLevelTop** retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem,* com o valor mais alto.  
  
 A função **DrilldownLevelTop** é semelhante à função [DrilldownLevel](../mdx/drilldownlevel-mdx.md) , mas em vez de incluir todos os filhos de cada membro no nível especificado, a função **DrilldownLevelTop** retorna o número mais alto de membros filho.  
  
 Consultar a propriedade XMLA MdpropMdxDrillFunctions permite que você verifique o nível de suporte que o servidor fornece para as funções de análise; consulte [Propriedades XMLA com suporte &#40;&#41;XMLA](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obter detalhes.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os três filhos superiores do nível Categoria do Produto, com base na medida padrão. No cubo de exemplo do Adventure Works, os três filhos superiores de Acessórios são Bicicletário, Suporte para bicicleta e Garrafas e compartimentos. No Management Studio, na janela de consulta do MDX, você pode navegar para Produtos | Categorias de Produto | Membros | Todos os Produtos | Acessórios para exibir a lista completa. Você pode aumentar o argumento Contagem para retornar mais membros.  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 O exemplo a seguir ilustra o uso do sinalizador **include_calc_members** , usado para incluir membros calculados no nível de busca detalhada. A medida [contagem de pedidos do revendedor] é incluída na instrução **DrilldownLevelTop** para garantir que os valores de retorno sejam classificados por essa medida.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DrilldownLevel&#41;MDX &#40;](../mdx/drilldownlevel-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
