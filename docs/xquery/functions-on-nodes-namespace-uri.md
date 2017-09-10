---
title: "Função namespace-uri (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
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
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89c8cf916143a1041c340aeea48642c87c1d17cd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-nodes---namespace-uri"></a>Funções em nós - namespace-uri
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o namespace URI do QName especificado em *$arg* como xs: String.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nome de nó cuja parte do namespace URI será recuperada.  
  
## <a name="remarks"></a>Comentários  
  
-   Se o argumento for omitido, o padrão será o nó de contexto.  
  
-   No SQL Server, **fn:namespace-uri()** sem um argumento só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, só pode ser usado entre parênteses ([]).  
  
-   Se *$arg* é a sequência vazia, a cadeia de caracteres de comprimento zero será retornada.  
  
-   Se *$arg* é um elemento ou nó de atributo cujo expanded-QName não está em um namespace, a função retorna a cadeia de caracteres de comprimento zero  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. Recuperar o URI do namespace de um nó específico  
 A consulta a seguir é especificada em uma instância XML não digitada. A expressão de consulta, `namespace-uri(/ROOT[1])`, recupera a parte do namespace URI do nó especificado.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 Em razão do QName especificado não possuir a parte do namespace URI, mas só a parte de nome local, o resultado será uma cadeia de caracteres de comprimento zero.  
  
 A consulta a seguir é especificada em digitada Instructions **xml** coluna. A expressão, `namespace-uri(/AWMI:root[1]/AWMI:Location[1])`, retorna o namespace URI do primeiro elemento filho <`Location`> do elemento <`root`>.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Este é o resultado:  
  
```  
http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. Usando um namespace-uri() sem argumento em um predicado  
 A consulta a seguir está especifica em uma coluna digitada CatalogDescription xml. A expressão retorna todos os nós de elementos cujo namespace URI seja `http://www.adventure-works.com/schemas/OtherFeatures`. O namespace -**URI ()** função é especificada sem um argumento e usa o nó de contexto.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "http://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é um resultado parcial:  
  
```  
<p1:wheel xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="http://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
…  
```  
  
 Você pode alterar o namespace URI na consulta anterior para `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`. Você receberá todas as crianças de nó do elemento <`ProductDescription`> cuja parte do namespace URI do QName expandido seja `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`.  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **namespace-uri()** função retorna instâncias do tipo xs: String em vez de xs: anyURI.  
  
## <a name="see-also"></a>Consulte também  
 [Funções em nós](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Função &#40; de nome local XQuery &#41;](../xquery/functions-on-nodes-local-name.md)  
  
  

