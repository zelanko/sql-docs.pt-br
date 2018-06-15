---
title: Função (XQuery) substring | Microsoft Docs
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
caps.latest.revision: 42
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4bf01599d3144ca6eb3ebbfa74435ab16b25176a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077263"
---
# <a name="functions-on-string-values---substring"></a>Funções em valores de cadeia de caracteres - subcadeia de caracteres
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna a parte do valor de *$sourceString*, começando na posição indicada pelo valor de *$startingLoc,* e continue para o número de caracteres indicado pelo valor de *$ comprimento*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc  as as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$sourceString*  
 Cadeia de caracteres de origem.  
  
 *$startingLoc*  
 Ponto de partida na cadeia de caracteres de origem do qual a subcadeia de caracteres é iniciada. Se esse valor for negativo ou 0, apenas aqueles caracteres em posições maiores que zero serão retornados. Se for maior que o comprimento do *$sourceString*, a cadeia de caracteres de comprimento zero será retornada.  
  
 *$length*  
 [opcional] Número de caracteres a recuperar. Se não for especificado, ele retorna todos os caracteres do local especificado em *$startingLoc* até o fim da cadeia de caracteres.  
  
## <a name="remarks"></a>Remarks  
 A versão de três argumentos da função retorna os caracteres em `$sourceString` cuja posição `$p` obedece:  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 O valor de *$length* pode ser maior que o número de caracteres no valor do *$sourceString* após a posição inicial. Nesse caso, a subcadeia retorna os caracteres até o fim da *$sourceString*.  
  
 O primeiro caractere de uma cadeia de caracteres está situado na posição 1.  
  
 Se o valor de *$sourceString* é a sequência vazia, ela é tratada como a cadeia de caracteres de comprimento zero. Caso contrário, se qualquer *$startingLoc* ou *$length* é a sequência vazia, a sequência vazia será retornada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "XQuery funções têm consciência de substitutos" no tópico [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também [nível de compatibilidade do banco de dados ALTER &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 O SQL Server requer o *$startingLoc* e *$length parâmetros* ser do tipo xs: decimal em vez de xs: Double.  
  
 O SQL Server permite *$startingLoc* e *$length* sejam a sequência vazia, pois a sequência vazia é um valor possível como resultado de erros dinâmicos sendo mapeados para ().  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. Usando uma função substring() XQuery para recuperar descrições resumidas parciais de modelos de produtos  
 A consulta recupera os primeiros 50 caracteres do texto que descreve o modelo de produto, o elemento <`Summary`> no documento.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O **String ()** função retorna o valor da cadeia de <`Summary`> elemento. Essa função é usada, porque o elemento <`Summary`> contém o texto e os subelementos (html que formata elementos), e porque você ignorará esses elementos e recuperará todo o texto.  
  
-   O **substring** função recupera os primeiros 50 caracteres do valor de cadeia de caracteres recuperado pelo **String ()**.  
  
 Este é um resultado parcial:  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
