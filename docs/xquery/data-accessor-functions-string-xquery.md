---
title: Função String (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c20973cdaa3b3d80124a9713a104d7294d6c20f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076473"
---
# <a name="data-accessor-functions---string-xquery"></a>Funções do acessador de dados - cadeia de caracteres (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o valor de *$arg* representado como uma cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 É um nó ou um valor atômico.  
  
## <a name="remarks"></a>Remarks  
  
-   Se *$arg* é a sequência vazia, a cadeia de caracteres de comprimento zero será retornada.  
  
-   Se *$arg* é um nó, a função retornará o valor de cadeia de caracteres do nó que é obtido usando o acessador de valor de cadeia de caracteres. Isso está definido nas especificações do W3C XQuery 1.0 e do XPath 2.0 Data Model.  
  
-   Se *$arg* é um valor atômico, a função retorna a mesma cadeia de caracteres que é retornada pela expressão convertida como **xs: string**, *$arg*, exceto quando indicado em contrário.  
  
-   Se o tipo de *$arg* é **xs: anyURI**, o URI é convertido em uma cadeia de caracteres sem escapar caracteres especiais.  
  
-   Nessa implementação, **fn:string()** sem um argumento só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, só pode ser usado entre parênteses ([]).  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-string-function"></a>A. Usando a função string  
 A consulta a seguir recupera o nó do elemento filho <`Features`> do elemento <`ProductDescription`>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é o resultado parcial:  
  
```  
<PD:Features xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 Se você especificar o **String ()** função, você receberá o valor de cadeia de caracteres do nó especificado.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
 No exemplo a seguir, uma instância XML é atribuída a uma variável do tipo xml. Consultas são especificadas para ilustrar o resultado da aplicação **String ()** em vários nós.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
