---
title: TopPercent (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8c92a4b6a76cb9d15048d6f058038363970cb8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036587"
---
# <a name="toppercent-mdx"></a>TopPercent (MDX)


  Classifica um conjunto em ordem decrescente e retorna um conjunto de tuplas com os valores mais altos, cujo total cumulativo é igual ou maior do que um percentual especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Percentual*  
 Uma expressão numérica válida que especifica o percentual de tuplas a ser retornado.  
  
> [!IMPORTANT]  
>  O *percentual* precisa ser um valor positivo; os valores negativos geram um erro.  
  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
## <a name="remarks"></a>Comentários  
 A função **TopPercent** calcula a soma da expressão numérica especificada avaliada sobre o conjunto especificado, classificando o conjunto em ordem decrescente. A função retorna os elementos com os valores mais altos, cujo percentual cumulativo do valor total somado seja pelo menos o percentual especificado. Essa função retorna o subconjunto menor de um conjunto cujo total cumulativo é pelo menos o percentual especificado. Os elementos retornados são classificados do maior para menor.  
  
> [!WARNING]  
>  Se *Numeric_Expression* retornar qualquer valor negativo, **TopPercent** retornará apenas uma (1) linha.  
>   
>  Consulte o segundo exemplo para obter uma apresentação detalhada desse comportamento.  
  
> [!IMPORTANT]  
>  Assim como a função [BottomPercent](../mdx/bottompercent-mdx.md) , a função **TopPercent** sempre interrompe a hierarquia.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna as melhores cidades que ajudam a fazer os 10% principais das vendas do revendedor para a categoria Bike. O resultado é classificado em ordem decrescente, começando com a cidade que tem o valor mais alto de vendas.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 A expressão acima produz os seguintes resultados:  
  
||Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|$3508904.84|  
|London|$1521530.09|  
|Seattle|$1209418.16|  
|Paris|$1170425.18|  
  
 O conjunto original de dados pode ser obtido com a consulta seguinte e retorna 588 linhas:  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
## <a name="example"></a>Exemplo  
 O passo a seguir ajudará a entender o efeito de valores negativos no *Numeric_Expression*. Primeiro, vamos criar algum contexto onde podemos apresentar o comportamento.  
  
 A consulta a seguir retorna uma tabela de Resellers 'Sales Amount', 'Total Product Cost' e 'Gross Profit', em ordem decrescente de lucro. Observe que somente há valores negativos para lucro; portanto, a menor perda aparecerá no início.  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 A consulta acima retorna os resultados a seguir; as linhas da seção intermediária foram removidas para proporcionar legibilidade.  
  
||Reseller Sales Amount|Custo do produto total do revendedor|Lucro bruto do revendedor|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157444.56|$163112.57|($5668.01)|  
|Touring-2000 azul, 46|$321027.03|$333021.50|($11994.47)|  
|Touring-3000 azul, 62|$87773.61|$100133.52|($12359.91)|  
|...|...|...|...|  
|Touring-1000 amarelo, 46|$1016312.83|$1234454.27|($218141.44)|  
|Touring-1000 Yellow, 60|$1184363.30|$1443407.51|($259044.21)|  
  
 Agora, se pedissem a você para apresentar as principais bicicletas 100% por lucro, seria necessário escrever uma consulta como:  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 Observe que a consulta solicita um percentual de 100%; o que significa que todas as linhas devem ser retornadas. No entanto, como há valores negativos no *Numeric_Expression* , apenas uma linha é retornada.  
  
||Reseller Sales Amount|Custo do produto total do revendedor|Lucro bruto do revendedor|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157444.56|$163112.57|($5668.01)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
