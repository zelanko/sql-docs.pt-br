---
title: Função Data (XQuery) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6ac37c6d3a55be4f11a4ad925a950724d5d791d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62934837"
---
# <a name="data-accessor-functions---data-xquery"></a>Funções do Acessador de Dados – data (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o valor digitado para cada item especificado por *$arg*.  
  
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
  
-   Se o nó de atributo é digitado, seu valor digitado é igual a seu valor de cadeia de caracteres que é retornado como uma instância do **XDT: untypedatomic**.  
  
-   Se o nó de elemento não tiver sido tipado, seu valor digitado é igual a seu valor de cadeia de caracteres que é retornado como uma instância do **XDT: untypedatomic**.  
  
 As descrições a seguir aplicam-se a nós de elemento digitados:  
  
-   Se o elemento tem um tipo de conteúdo simple **Data ()** retorna o valor digitado do elemento.  
  
-   Se o nó for do tipo complexo, inclusive xs: anyType, **Data ()** retorna um erro estático.  
  
 Embora o uso de **Data ()** função é muitas vezes opcional, conforme mostrado nos exemplos a seguir, especificando as **Data ()** função explicitamente aumenta a legibilidade da consulta. Para obter mais informações, consulte [fundamentos de XQuery](../xquery/xquery-basics.md).  
  
 Não é possível especificar **Data ()** em XML construído, conforme mostrado a seguir:  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. Usando a função data() XQuery para extrair valor com tipo de um nó  
 A consulta a seguir ilustra como o **Data ()** função é usada para recuperar valores de um atributo, um elemento e um nó de texto:  
  
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
  
 Esse é o resultado:  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 Conforme mencionado, o **Data ()** função é opcional quando você está construindo atributos. Se você não especificar o **Data ()** função, ela é assumida implicitamente. A consulta a seguir produz os mesmos resultados da consulta prévia:  
  
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
  
 Os exemplos a seguir ilustram instâncias em que o **Data ()** função é necessária.  
  
 Na consulta a seguir **$pd / PD/P1:specifications/material / Material** retorna o <`Material`> elemento. Além disso, **dados ($pd/PD/P1:specifications/material/Material)** retorna dados de caracteres digitados como XDT: untypedatomic, porque o <`Material`> não é digitado. Quando a entrada não for digitada, o resultado da **Data ()** é digitado como **XDT: untypedatomic**.  
  
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
  
 Esse é o resultado:  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 Na consulta a seguir **data($pd/p1:Features/wm:Warranty)** retorna um erro estático, pois <`Warranty`> é um elemento de tipo complexo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
