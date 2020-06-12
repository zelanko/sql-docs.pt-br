---
title: Função maiúscula (XQuery) | Microsoft Docs
description: Saiba como usar a função do XQuery em maiúsculas (), que converte caracteres para o equivalente em maiúsculas.
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
- upper-case
- upper-case Function (XQuery)
ms.assetid: 5bd01ad2-7adf-48fb-bf42-41e200419d37
author: rothja
ms.author: jroth
ms.openlocfilehash: c757e46f861d6652b3c8c151c3e002dba13e84ef
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689490"
---
# <a name="functions-on-string-values---upper-case"></a>Funções em Valores da Cadeia de Caracteres – upper-case
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Essa função converte cada caractere em *$ARG* em seu equivalente em maiúsculas. No Microsoft Windows, a conversão binária de maiúsculas e minúsculas para pontos de código Unicode especifica como os caracteres são convertidos em letras maiúsculas. Esse padrão é diferente do mapeamento para o padrão de ponto de código padrão Unicode.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:upper-case($arg as xs:string?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
  
|||  
|-|-|  
|Termo|Definição|  
|*$arg*|O valor de cadeia de caracteres a ser convertido para letras maiúsculas.|  
  
## <a name="remarks"></a>Comentários  
 Se o valor de *$ARG* estiver vazio, uma cadeia de caracteres de comprimento zero será retornada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-a-string-to-upper-case"></a>a. Alterando uma cadeia de caracteres para letras maiúsculas  
 O exemplo a seguir altera a cadeia de caracteres de entrada ' abcDEF! @4 ' para letras maiúsculas.  
  
```  
DECLARE @x xml = N'abcDEF!@4';  
SELECT @x.value('fn:upper-case(/text()[1])', 'nvarchar(10)');  
```  
  
### <a name="b-search-for-a-specific-character-string"></a>B. Pesquisar uma cadeia de caracteres específica  
 Este exemplo mostra como usar a função upper-case para executar uma pesquisa sem diferenciação de maiúsculas e minúsculas.  
  
```  
USE AdventureWorks  
GO  
--WITH XMLNAMESPACES clause specifies the namespace prefix  
--to use.   
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
--The XQuery contains() function is used to determine whether  
--any of the text nodes below the <Summary> element contain  
--the word 'frame'. The upper-case() function is used to make  
--the search case-insensitive.  
  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
/pd:ProductDescription/pd:Summary//text()[  
          contains(upper-case(.), "FRAME")]')  = 1  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `19     <Prod ProductModelID="19">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike.`  
  
 `Performance-enhancing options include the innovative HL Frame,`  
  
 `super-smooth front suspension, and traction for all terrain.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
 `25     <Prod ProductModelID="25">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">This bike is ridden by race winners. Developed with the`  
  
 `Adventure Works Cycles professional race team, it has a extremely light`  
  
 `heat-treated aluminum frame, and steering that allows precision control.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
