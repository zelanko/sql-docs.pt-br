---
title: "Função Contains (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 025d47883976e0cf17ef9435d7bf127677a7b5b1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-string-values---contains"></a>Funções em valores de cadeia de caracteres - contém
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna um valor do tipo xs: Boolean indicando se o valor de *$arg1* contém um valor de cadeia de caracteres especificado por *$arg2*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg1*  
 Valor da cadeia de caracteres para testar.  
  
 *$arg2*  
 Subcadeia de caracteres a ser procurada.  
  
## <a name="remarks"></a>Comentários  
 Se o valor de *$arg2* for uma cadeia de caracteres de comprimento zero, a função retornará **True**. Se o valor de *$arg1* é uma cadeia de caracteres de comprimento zero e o valor de *$arg2* não é uma cadeia de caracteres de comprimento zero, a função retorna **False**.  
  
 Se o valor de *$arg1* ou *$arg2* é a sequência vazia, o argumento é tratado como a cadeia de caracteres de comprimento zero.  
  
 A função contains() usa o agrupamento de ponto de código Unicode padrão do XQuery para a comparação de cadeias de caracteres.  
  
 O valor de subcadeia de caracteres especificado para *$arg2* deve ser menor ou igual a 4000 caracteres. Se o valor especificado é maior que 4000 caracteres, ocorrerá uma condição de erro dinâmico e a função Contains () retorna uma sequência vazia em vez de um valor booliano de **True** ou **False**. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não gera erros dinâmicos em expressões XQuery.  
  
 Para obter comparações de maiusculas e minúsculas, o [maiusculas](../xquery/functions-on-string-values-upper-case.md) ou minúsculas funções podem ser usadas.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "XQuery funções têm consciência de substitutos" no tópico [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também [nível de compatibilidade de ALTER DATABASE &#40; Transact-SQL &#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias colunas de tipo xml no banco de dados AdventureWorks.  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>A. Usando a função contains() XQuery para pesquisar uma cadeia de caracteres específica  
 A consulta a seguir localiza produtos que contêm a palavra Aerodynamic nas descrições resumidas. A consulta retorna o ProductID e o elemento <`Summary`> para tais produtos.  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
   /pd:ProductDescription/pd:Summary//text()  
    [contains(., "Aerodynamic")]') = 1  
```  
  
 Resultados  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `28     <Prod ProductModelID="28">`  
  
 `<pd:Summary xmlns:pd=`  
  
 `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
