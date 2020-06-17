---
title: Função de cadeia de caracteres (XQuery) | Microsoft Docs
description: Saiba mais sobre a cadeia de caracteres da função XQuery () que retorna o valor de seu argumento representado como uma cadeia de caracteres.
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
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 59c90ce7e0bdbe46fa1ca577e2b16e6576650751
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84881893"
---
# <a name="data-accessor-functions---string-xquery"></a>Funções do Acessador de Dados – string (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o valor de *$ARG* representado como uma cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 É um nó ou um valor atômico.  
  
## <a name="remarks"></a>Comentários  
  
-   Se *$ARG* for a sequência vazia, a cadeia de caracteres de comprimento zero será retornada.  
  
-   Se *$ARG* for um nó, a função retornará o valor da cadeia de caracteres do nó que é obtido usando o acessador de valor de cadeia de caracteres. Isso está definido nas especificações do W3C XQuery 1.0 e do XPath 2.0 Data Model.  
  
-   Se *$ARG* for um valor atômico, a função retornará a mesma cadeia de caracteres retornada pela expressão CAST como **xs: String**, *$ARG*, exceto quando indicado de outra forma.  
  
-   Se o tipo de *$ARG* for **xs: anyURI**, o URI é convertido em uma cadeia de caracteres sem escape de caracteres especiais.  
  
-   Essa implementação, **fn: String ()** sem um argumento, só pode ser usada no contexto de um predicado dependente de contexto. Mais precisamente, só pode ser usado entre parênteses ([]).  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-string-function"></a>a. Usando a função string  
 A consulta a seguir recupera o <`Features`> nó de elemento filho do `ProductDescription` elemento <>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é o resultado parcial:  
  
```  
<PD:Features xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 Se você especificar a função **String ()** , receberá o valor da cadeia de caracteres do nó especificado.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é o resultado parcial.  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. Usando a função string em vários nós  
 No exemplo a seguir, uma instância XML é atribuída a uma variável do tipo xml. As consultas são especificadas para ilustrar o resultado da aplicação de **String ()** a vários nós.  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 A consulta a seguir recupera o valor da cadeia de caracteres do nó do documento. Esse valor é formado pela concatenação do valor da cadeia de caracteres de todos os seus nós de texto descendentes.  
  
```  
select @x.query('string(/)')  
```  
  
 Este é o resultado:  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 A consulta a seguir tenta recuperar o valor da cadeia de caracteres de um nó de instrução de processamento. O resultado é uma sequência vazia, porque não contém um nó de texto.  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 A consulta a seguir recupera o valor da cadeia de caracteres do nó de comentário e retorna o nó de texto.  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 Este é o resultado:  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
