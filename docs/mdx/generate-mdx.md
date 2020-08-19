---
description: Generate (MDX)
title: Gerar (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9746d83589464f75bbc951c20dc15d04b7b2037d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429948"
---
# <a name="generate-mdx"></a>Generate (MDX)


  Aplica um conjunto a cada membro de outro conjunto e une os conjuntos resultantes por união. Opcionalmente, essa função retorna uma cadeia de caracteres concatenada criada avaliando-se uma expressão de cadeia de caracteres sobre um conjunto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida que, normalmente, é o nome do membro atual (CurrentMember.Name) de cada tupla no conjunto especificado.  
  
 *Delimitador*  
 Um delimitador válido expresso como uma expressão de cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Se um segundo conjunto for especificado, a função **Generate** retornará um conjunto gerado aplicando as tuplas no segundo conjunto para cada tupla no primeiro conjunto e, em seguida, unindo os conjuntos resultantes por Union. Se **All** for especificado, a função retém duplicatas no conjunto resultante.  
  
 Se uma expressão de cadeia de caracteres for especificada, a função **gerar** retornará uma cadeia de caracteres gerada pela avaliação da expressão de cadeia de caracteres especificada em cada tupla no primeiro conjunto e, em seguida, concatenando os resultados. Opcionalmente, a cadeia de caracteres pode ser delimitada, separando-se cada resultado na cadeia de caracteres concatenada resultante.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="set"></a>Definir  
 No exemplo a seguir, a consulta retorna um conjunto que contém a quantidade de vendas pela Internet quatro vezes, pois existem quatro membros no conjunto [Data].[Ano Civil].[Ano Civil].MEMBERS:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 A remoção de ALL altera a consulta, de modo que a Quantidade de Vendas pela Internet é retornada somente uma vez:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 O uso prático mais comum de **gerar** é avaliar uma expressão de conjunto complexo, como TopCount, em um conjunto de membros. A consulta de exemplo a seguir exibe os 10 Produtos principais para cada Ano Civil em Linhas:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 Observe que os 10 principais diferentes são exibidos para cada ano e que o uso de **Generate** é a única maneira de obter esse resultado. Simplesmente unir os Anos Civis e o conjunto dos 10 Produtos principais exibirá os 10 Produtos principais para todo o período, repetido em cada ano, como mostra o exemplo a seguir:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 O exemplo a seguir mostra o uso de **Generate** para retornar uma cadeia de caracteres:  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Essa forma da função **Generate** pode ser útil ao depurar cálculos, pois permite que você retorne uma cadeia de caracteres exibindo os nomes de todos os membros em um conjunto. Isso pode ser mais fácil de ler do que a representação MDX estrita de um conjunto que a função [SetToStr &#40;MDX&#41;](../mdx/settostr-mdx.md) retorna.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
