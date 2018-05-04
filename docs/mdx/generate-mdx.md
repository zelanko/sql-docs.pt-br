---
title: Gerar (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GENERATE
dev_langs:
- kbMDX
helpviewer_keywords:
- Generate function
ms.assetid: 696a229d-c2f1-47b7-9dca-7b0a6b547d9b
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b352fe818402cbad25af99a4ca336704b331a4f9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="generate-mdx"></a>Generate (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 Se um segundo conjunto for especificado, o **gerar** função retorna um conjunto gerado aplicando as tuplas do segundo conjunto a cada tupla no primeiro conjunto *,* e, em seguida, associando os conjuntos resultantes por união. Se **todos os** for especificado, a função preservará as duplicações no conjunto resultante.  
  
 Se uma expressão de cadeia de caracteres for especificada, o **gerar** função retorna uma cadeia de caracteres gerada avaliando a expressão de cadeia de caracteres especificada em relação a cada tupla no primeiro conjunto *,* e concatenando os resultados. Opcionalmente, a cadeia de caracteres pode ser delimitada, separando-se cada resultado na cadeia de caracteres concatenada resultante.  
  
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
  
 O uso prático mais comum de **gerar** é para avaliar um complexo conjunto de expressão, como TopCount, em um conjunto de membros. A consulta de exemplo a seguir exibe os 10 Produtos principais para cada Ano Civil em Linhas:  
  
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
  
 Observe que a parte superior 10 diferente é exibido para cada ano e que o uso de **gerar** é a única maneira de obter esse resultado. Simplesmente unir os Anos Civis e o conjunto dos 10 Produtos principais exibirá os 10 Produtos principais para todo o período, repetido em cada ano, como mostra o exemplo a seguir:  
  
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
>  Essa forma do **gerar** função pode ser útil ao depurar cálculos, pois permite retornar uma cadeia de caracteres que exibe os nomes de todos os membros em um conjunto. Isso pode ser mais fácil de ler do que a representação MDX rígida de um conjunto que o [SetToStr &#40;MDX&#41; ](../mdx/settostr-mdx.md) função retorna.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
