---
title: Função local-name (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3844608511c847d1ae87d8ca966d920fbb3cc658
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-nodes---local-name"></a>Funções em nós - local-name
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna a parte local do nome do *$arg* como xs: String que será a cadeia de caracteres de comprimento zero ou terá a forma léxica de um xs: NCName. Se o argumento não for fornecido, o padrão será o nó de contexto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nome de nó cuja parte local-name será recuperada.  
  
## <a name="remarks"></a>Remarks  
  
-   No SQL Server, **fn:local-name()** sem um argumento só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, ele só pode ser usado entre parênteses (`[ ]`).  
  
-   Se o argumento for fornecido e a sequência for vazia, a função retornará a cadeia de caracteres de comprimento zero.  
  
-   Se o nó designado não tiver nome, por ser um nó de documento, um comentário ou um nó de texto, a função retornará a cadeia de caracteres de comprimento zero.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. Recuperar o nome local de um nó específico  
 A consulta a seguir é especificada em uma instância XML não digitada. A expressão de consulta, `local-name(/ROOT[1])`, recupera a parte do nome local do nó especificado.  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 A consulta a seguir é especificada contra a coluna Instructions, uma coluna xml digitada, da tabela ProductModel. A expressão, `local-name(/AWMI:root[1]/AWMI:Location[1])`, retorna o nome local, `Location`, do nó especificado.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. Usando o local-name sem argumento em um predicado  
 A consulta a seguir é especificada na coluna Instructions, digitada **xml** coluna da tabela ProductModel. A expressão retorna todos os filhos do elemento do elemento <`root`> cuja parte do nome local do QName é "Location". O **example** função é especificada no predicado e não tem argumentos do nó de contexto é usado pela função.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 A consulta retorna todos os filhos do elemento <`Location`> do elemento <`root`>.  
  
## <a name="see-also"></a>Consulte também  
 [Funções em nós](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Função namespace-uri &#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
