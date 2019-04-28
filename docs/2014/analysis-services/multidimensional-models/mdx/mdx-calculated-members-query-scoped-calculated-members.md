---
title: Criando no escopo da consulta calculado membros (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- query-scoped calculated members [MDX]
ms.assetid: c4507149-e67b-4e5d-9192-cc911acd9adc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6de68556d6bbd7277324e6083d70f979fa1303fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725540"
---
# <a name="creating-query-scoped-calculated-members-mdx"></a>Criando membros calculados no escopo da consulta (MDX)
  Se um membro calculado for necessário para uma única consulta de expressões multidimensionais (MDX), é possível defini-lo usando a palavra-chave WITH. O membro calculado criado com a palavra-chave WITH deixará de existir ao fim da execução da consulta.  
  
 Como discutido neste tópico, a sintaxe da palavra-chave WITH é bem flexível, permitindo até que um membro calculado baseie-se em outro membro calculado.  
  
> [!NOTE]  
>  Para obter mais informações sobre membros calculados, consulte [Criando membros calculados no MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
## <a name="with-keyword-syntax"></a>Sintaxe da palavra-chave WITH  
 Use a sintaxe a seguir para adicionar a palavra-chave WITH a uma instrução MDX SELECT:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ] SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]FROM <SELECT subcube clause> [ <SELECT slicer axis clause> ][ <SELECT cell property list clause> ]  
<SELECT WITH clause> ::=  
   ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>) | <CREATE MEMBER body clause> ::= Member_Identifier AS 'MDX_Expression'  
   [ <CREATE MEMBER property clause> [ , <CREATE MEMBER property clause> ... ] ]  
<CREATE MEMBER property clause> ::=  
   ( MemberProperty_Identifier = Scalar_Expression )  
  
```  
  
 Na sintaxe da palavra-chave WITH, o valor `Member_Identifier` é o nome totalmente qualificado do membro calculado. Esse nome totalmente qualificado inclui a dimensão ou o nível a que o membro calculado está associado. O valor `MDX_Expression` retorna o valor do membro calculado depois que o valor de expressão foi avaliado. Opcionalmente, os valores de propriedades de células intrínsecas de um membro calculado podem ser especificados fornecendo-se o nome da propriedade de célula no valor `MemberProperty_Identifier` e o valor da propriedade de célula no valor `Scalar_Expression` .  
  
## <a name="with-keyword-examples"></a>Exemplos da palavra-chave WITH  
 A consulta MDX a seguir define um membro calculado, `[Measures].[Special Discount]`, calculando um desconto especial com base no valor de desconto original.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Também é possível criar membros calculados em qualquer ponto de uma hierarquia. Por exemplo, a consulta MDX a seguir define o membro calculado `[BigSeller]` para um cubo Vendas hipotético. Esse membro calculado determina se uma loja especificada possui, no mínimo, 100,00 em vendas unitárias para cerveja e vinho. No entanto, a consulta cria o membro calculado `[BigSeller]` não como um membro filho da dimensão `[Product]` , mas sim como um membro filho do membro `[Beer and Wine]` .  
  
```  
WITH   
   MEMBER [Product].[Beer and Wine].[BigSeller] AS  
  IIf([Product].[Beer and Wine] > 100, "Yes","No")  
SELECT  
   {[Product].[BigSeller]} ON COLUMNS,  
   Store.[Store Name].Members ON ROWS  
FROM Sales  
  
```  
  
 Membros calculados não têm que depender exclusivamente dos membros existentes em um cubo. O membro calculado também pode basear-se em outros membros calculados definidos na mesma expressão MDX. Por exemplo, a consulta MDX a seguir usa o valor criado pelo primeiro membro calculado, `[Measures].[Special Discount]`, para gerar o valor do segundo membro calculado, `[Measures].[Special Discounted Amount]`:  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Percentage] * 1.5,   
   FORMAT_STRING = 'Percent'  
  
   MEMBER [Measures].[Special Discounted Amount] AS  
   [Measures].[Reseller Average Unit Price] * [Measures].[Special Discount],   
   FORMAT_STRING = 'Currency'  
  
SELECT   
   {[Measures].[Special Discount], [Measures].[Special Discounted Amount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [Instrução SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Criando membros calculados no escopo da sessão &#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md)  
  
  
