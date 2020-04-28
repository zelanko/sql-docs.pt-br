---
title: Função de dados (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
ms.openlocfilehash: 7376c57f809fa97168b27b158678d931a696b5df
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038974"
---
# <a name="data-accessor-functions---data-xquery"></a>Funções do Acessador de Dados – data (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o valor digitado para cada item especificado por *$ARG*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de itens cujos valores digitados serão retornados.  
  
## <a name="remarks"></a>Comentários  
 As descrições a seguir aplicam-se a valores digitados:  
  
-   O valor digitado de um valor atômico é o valor atômico.  
  
-   O valor digitado de um nó de texto é o valor da cadeia de caracteres do nó de texto.  
  
-   O valor digitado de um comentário é o valor da cadeia de caracteres do comentário.  
  
-   O valor digitado de uma instrução de processamento é o conteúdo da instrução de processamento, sem o nome de destino da instrução de processamento.  
  
-   O valor digitado de um nó de documento é seu valor de cadeia de caracteres.  
  
 As descrições a seguir aplicam-se a atributo e nós de elemento:  
  
-   Se um nó de atributo é digitado com um tipo de esquema XML, seu valor digitado será o valor digitado.  
  
-   Se o nó de atributo for não tipado, seu valor tipado será igual ao valor da cadeia de caracteres retornado como uma instância de **xdt: untypedAtomic**.  
  
-   Se o nó do elemento não tiver sido digitado, seu valor tipado será igual ao valor da cadeia de caracteres retornado como uma instância de **xdt: untypedAtomic**.  
  
 As descrições a seguir aplicam-se a nós de elemento digitados:  
  
-   Se o elemento tiver um tipo de conteúdo simples, **Data ()** retornará o valor tipado do elemento.  
  
-   Se o nó for de tipo complexo, incluindo xs: anyType, **Data ()** retornará um erro estático.  
  
 Embora o uso da função **Data ()** geralmente seja opcional, conforme mostrado nos exemplos a seguir, especificar a função **Data ()** aumenta explicitamente a legibilidade da consulta. Para obter mais informações, consulte [noções básicas do XQuery](../xquery/xquery-basics.md).  
  
 Você não pode especificar **dados ()** em XML construído, conforme mostrado a seguir:  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. Usando a função data() XQuery para extrair valor com tipo de um nó  
 A consulta a seguir ilustra como a função **Data ()** é usada para recuperar valores de um atributo, um elemento e um nó de texto:  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Este é o resultado:  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 Conforme mencionado, a função **Data ()** é opcional quando você está construindo atributos. Se você não especificar a função **Data ()** , ela será implicitamente assumida. A consulta a seguir produz os mesmos resultados da consulta prévia:  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Os exemplos a seguir ilustram as instâncias nas quais a função **Data ()** é necessária.  
  
 Na consulta a seguir, **$PD/P1: Specifications/material** retorna o `Material` elemento <>. Além disso, **os dados ($PD/P1: especificações/material)** retornam dados de caractere digitados como xdt `Material` : untypedAtomic, porque <> é não tipado. Quando a entrada é não tipada, o resultado de **Data ()** é digitado como **xdt: untypedAtomic**.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Este é o resultado:  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 Na consulta a seguir, os **dados ($PD/P1: Features/WM: warrantion)** retorna um erro estático, `Warranty` porque <> é um elemento de tipo complexo.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
