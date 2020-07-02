---
title: Função Contains (XQuery) | Microsoft Docs
description: Saiba como usar a função Contains em um XQuery para determinar se um valor de cadeia de caracteres especificado contém o valor de subcadeia de caracteres especificado.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c1f313a5316059a05cb30a5af6ef7a451353a3d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724219"
---
# <a name="functions-on-string-values---contains"></a>Funções em Valores da Cadeia de Caracteres – contains
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna um valor do tipo xs: booliano que indica se o valor de *$ARG 1* contém um valor de cadeia de caracteres especificado por *$ARG 2*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg 1*  
 Valor da cadeia de caracteres para testar.  
  
 *$arg 2*  
 Subcadeia de caracteres a ser procurada.  
  
## <a name="remarks"></a>Comentários  
 Se o valor de *$ARG 2* for uma cadeia de caracteres de comprimento zero, a função retornará **true**. Se o valor de *$ARG 1* for uma cadeia de caracteres de comprimento zero e o valor de *$ARG 2* não for uma cadeia de caracteres de comprimento zero, a função retornará **false**.  
  
 Se o valor de *$ARG 1* ou *$ARG 2* for a sequência vazia, o argumento será tratado como a cadeia de caracteres de comprimento zero.  
  
 A função contains() usa a ordenação de ponto de código Unicode padrão do XQuery para a comparação de cadeias de caracteres.  
  
 O valor da subcadeia de caracteres especificado para *$ARG 2* deve ser menor ou igual a 4000 caracteres. Se o valor especificado for maior que 4000 caracteres, ocorrerá uma condição de erro dinâmico e a função Contains () retornará uma sequência vazia em vez de um valor booliano de **true** ou **false**. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não gera erros dinâmicos em expressões XQuery.  
  
 Para obter comparações que não diferenciam maiúsculas de minúsculas, as funções [com](../xquery/functions-on-string-values-upper-case.md) letras maiúsculas ou minúsculas podem ser usadas.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "as funções do XQuery são de reconhecimento de substitutos" no tópico [alterações significativas em mecanismo de banco de dados recursos no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também o [nível de compatibilidade de ALTER DATABASE &#40;&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [agrupamento e suporte a Unicode](../relational-databases/collations/collation-and-unicode-support.md)do Transact-SQL.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML armazenadas em várias colunas do tipo XML no banco de dados AdventureWorks.  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>a. Usando a função contains() XQuery para pesquisar uma cadeia de caracteres específica  
 A consulta a seguir localiza produtos que contêm a palavra Aerodynamic nas descrições resumidas. A consulta retorna o ProductID e o <`Summary` elemento> para esses produtos.  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
 `"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
