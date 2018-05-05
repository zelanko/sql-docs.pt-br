---
title: DrilldownLevelTop (MDX) | Microsoft Docs
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
- DRILLDOWNLEVELTOP
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownLevelTop function
ms.assetid: b3b45dd6-2ade-4dd7-83dd-849231e2e517
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4b58470ebd068ec211e72d0a2ae2ccaaed0cf2df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 Se uma expressão numérica for especificada, o **DrilldownLevelTop** função classificará, em ordem decrescente, os filhos de cada membro no conjunto especificado de acordo com o valor da expressão numérica, conforme avaliado sobre o conjunto de membros filho. Se não for especificada uma expressão numérica, a função classificará, em ordem decrescente, os filhos de cada membro no conjunto especificado de acordo com os valores das células representadas pelo conjunto de membros filho, conforme determinado pelo contexto da consulta.  
  
 Depois da classificação, o **DrilldownLevelTop** função retorna um conjunto que contém os membros pai e o número de membros filho, especificados em *contagem,* com o valor mais alto.  
  
 O **DrilldownLevelTop** função é semelhante ao [DrilldownLevel](../mdx/drilldownlevel-mdx.md) função, mas em vez de incluir todos os filhos de cada membro no nível especificado, o **DrilldownLevelTop** função retorna o número mais alto de membros filho.  
  
 Consultando a propriedade XMLA MdpropMdxDrillFunctions permite verificar o nível de suporte que o servidor fornece para as funções de detalhamento; consulte [propriedades com suporte do XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obter detalhes.  
  
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
  
 O exemplo a seguir ilustra o uso de **include_calc_members** sinalizador, usado para incluir membros calculados no nível de detalhamento. A medida [contagem dos pedidos do revendedor] está incluída no **DrilldownLevelTop** instrução para garantir que os valores retornados são classificados por essa medida.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [DrilldownLevel & #40; MDX & #41;](../mdx/drilldownlevel-mdx.md)   
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
