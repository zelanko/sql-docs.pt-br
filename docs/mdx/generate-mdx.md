---
title: Generate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 222479dd03263f61a603e30202f2abf54307b0bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224878"
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
  
 *delimitador*  
 Um delimitador válido expresso como uma expressão de cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Se um segundo conjunto for especificado, o **Generate** função retorna um conjunto gerado aplicando as tuplas do segundo conjunto a cada tupla no primeiro conjunto *,* e, em seguida, associando os conjuntos resultantes por união. Se **todos os** for especificado, a função preservará as duplicações no conjunto resultante.  
  
 Se uma expressão de cadeia de caracteres for especificada, o **Generate** função retorna uma cadeia de caracteres gerada avaliando a expressão de cadeia de caracteres especificada em relação a cada tupla no primeiro conjunto *,* e, em seguida, concatenar a resultados. Opcionalmente, a cadeia de caracteres pode ser delimitada, separando-se cada resultado na cadeia de caracteres concatenada resultante.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="set"></a>Defina  
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
  
 O uso prático mais comum de **gerar** é avaliar um complexo definido expressão, como TopCount, ao longo de um conjunto de membros. A consulta de exemplo a seguir exibe os 10 Produtos principais para cada Ano Civil em Linhas:  
  
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
  
 Observe que um diferente top 10 é exibida para cada ano e que o uso de **gerar** é a única maneira de obter esse resultado. Simplesmente unir os Anos Civis e o conjunto dos 10 Produtos principais exibirá os 10 Produtos principais para todo o período, repetido em cada ano, como mostra o exemplo a seguir:  
  
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
  
### <a name="string"></a>Cadeia de caracteres  
 O exemplo a seguir mostra o uso de **gerar** para retornar uma cadeia de caracteres:  
  
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
>  Essa forma do **gerar** função pode ser útil ao depurar cálculos, pois ele permite que você retorne uma cadeia de caracteres que exibe os nomes de todos os membros em um conjunto. Isso pode ser mais fácil de ler do que a representação MDX rígida de um conjunto que o [SetToStr &#40;MDX&#41; ](../mdx/settostr-mdx.md) retornos de função.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
