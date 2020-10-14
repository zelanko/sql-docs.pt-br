---
title: namespace-função URI (XQuery) | Microsoft Docs
description: Saiba como usar a função namespace-URI em um XQuery para retornar o URI do namespace de um QName especificado.
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
author: rothja
ms.author: jroth
ms.openlocfilehash: ed19a835b6df605a6ec735a8063a192ea32148fd
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034829"
---
# <a name="functions-on-nodes---namespace-uri"></a>Funções em Nós – namespace-uri
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  Retorna o URI do namespace do QName especificado em *$ARG* como um xs: String.  
  
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
  
-   Em SQL Server, **fn: namespace-URI ()** sem um argumento só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, só pode ser usado entre parênteses ([]).  
  
-   Se *$ARG* for a sequência vazia, a cadeia de caracteres de comprimento zero será retornada.  
  
-   Se *$ARG* for um nó de elemento ou atributo cujo QName de expansão não está em um namespace, a função retornará a cadeia de caracteres de comprimento zero  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>a. Recuperar o URI do namespace de um nó específico  
 A consulta a seguir é especificada em uma instância XML não digitada. A expressão de consulta, `namespace-uri(/ROOT[1])`, recupera a parte do namespace URI do nó especificado.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 Em razão do QName especificado não possuir a parte do namespace URI, mas só a parte de nome local, o resultado será uma cadeia de caracteres de comprimento zero.  
  
 A consulta a seguir é especificada em relação à coluna **XML** de instruções tipadas. A expressão, `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` , retorna o URI do namespace do primeiro <`Location`> filho do elemento <`root`>.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Este é o resultado:  
  
```  
https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. Usando um namespace-uri() sem argumento em um predicado  
 A consulta a seguir está especifica em uma coluna digitada CatalogDescription xml. A expressão retorna todos os nós de elementos cujo namespace URI seja `https://www.adventure-works.com/schemas/OtherFeatures`. A função namespace-**URI ()** é especificada sem um argumento e usa o nó de contexto.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "https://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é um resultado parcial:  
  
```  
<p1:wheel xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="https://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
...  
```  
  
 Você pode alterar o namespace URI na consulta anterior para `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`. Em seguida, você receberá todos os filhos do nó de elemento do <`ProductDescription`> elemento cuja parte do URI do namespace do QName expandido é `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` .  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **namespace-URI ()** retorna instâncias do tipo xs: String em vez de xs: anyURI.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções em nós](./xquery-functions-against-the-xml-data-type.md)   
 [Função de nome local &#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
