---
title: Criando no escopo da consulta calculado membros (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dd315d5c7c7cc2e3cc9839c8831c5356fa3e8ac5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62802678"
---
# <a name="mdx-calculated-members---query-scoped-calculated-members"></a>Membros - membros calculados no escopo da consulta calculados MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Se um membro calculado for necessário para uma única consulta de expressões multidimensionais (MDX), é possível defini-lo usando a palavra-chave WITH. O membro calculado criado com a palavra-chave WITH deixará de existir ao fim da execução da consulta.  
  
 Como discutido neste tópico, a sintaxe da palavra-chave WITH é bem flexível, permitindo até que um membro calculado baseie-se em outro membro calculado.  
  
> [!NOTE]  
>  Para obter mais informações sobre membros calculados, consulte [Criando membros calculados no MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Instrução SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Criando membros calculados no escopo da sessão &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)  
  
  
