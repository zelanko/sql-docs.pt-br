---
title: Função (XQuery) substring | Microsoft Docs
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 2188cff20411fe90d4858763f65cff7f6fe9c9d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004644"
---
# <a name="functions-on-string-values---substring"></a>Funções em Valores da Cadeia de Caracteres – substring
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna a parte do valor de *$sourceString*, começando na posição indicada pelo valor da *$startingLoc,* e continua para o número de caracteres indicado pelo valor de *$ comprimento*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$sourceString*  
 Cadeia de caracteres de origem.  
  
 *$startingLoc*  
 Ponto de partida na cadeia de caracteres de origem do qual a subcadeia de caracteres é iniciada. Se esse valor for negativo ou 0, apenas aqueles caracteres em posições maiores que zero serão retornados. Se ele for maior que o tamanho de *$sourceString*, a cadeia de caracteres de comprimento zero será retornada.  
  
 *$length*  
 [opcional] Número de caracteres a recuperar. Se não for especificado, ele retorna todos os caracteres do local especificado na *$startingLoc* até o fim da cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 A versão de três argumentos da função retorna os caracteres em `$sourceString` cuja posição `$p` obedece:  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 O valor de *$length* pode ser maior que o número de caracteres no valor da *$sourceString* após a posição inicial. Nesse caso, a subcadeia retorna os caracteres até o final da *$sourceString*.  
  
 O primeiro caractere de uma cadeia de caracteres está situado na posição 1.  
  
 Se o valor de *$sourceString* é a sequência vazia, ela é tratada como a cadeia de caracteres de comprimento zero. Caso contrário, se qualquer um dos *$startingLoc* ou *$length* é a sequência vazia, a sequência vazia será retornada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "XQuery funções têm consciência de substitutos" no tópico [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também [nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 O SQL Server requer o *$startingLoc* e *$length parâmetros* seja do tipo xs: decimal em vez de xs: Double.  
  
 O SQL Server permite *$startingLoc* e *$length* como a sequência vazia, porque a sequência vazia é um valor possível como resultado de erros dinâmicos sendo mapeados para ().  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo a [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. Usando uma função substring() XQuery para recuperar descrições resumidas parciais de modelos de produtos  
 A consulta recupera os primeiros 50 caracteres do texto que descreve o modelo de produto, o <`Summary`> elemento no documento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O **String ()** função retorna o valor de cadeia de caracteres da <`Summary`> elemento. Essa função é usada, porque o <`Summary`> elemento contém o texto e os subelementos (html que formata elementos), e porque você ignorará esses elementos e recuperará todo o texto.  
  
-   O **substring ()** função recupera os primeiros 50 caracteres do valor de cadeia de caracteres recuperado pelo **String ()** .  
  
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
  
  
