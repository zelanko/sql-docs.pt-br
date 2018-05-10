---
title: Colunas com o nome de um teste de nó XPath | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
- XPath node test
ms.assetid: b48adccd-3b6b-486a-b326-20f57170186f
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1f4c869966c59893ec84e91d73f145facd4ebc06
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="columns-with-the-name-of-an-xpath-node-test"></a>Colunas com o nome de um teste de nó XPath
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Se o nome da coluna for um dos testes de nó XPath, o conteúdo será mapeado conforme mostrado na tabela a seguir. Quando o nome de coluna é um teste de nó XPath, o conteúdo é mapeado para o nó correspondente. Se o tipo da coluna SQL for **xml**, um erro será retornado.  
  
|Nome da coluna|Comportamento|  
|-----------------|--------------|  
|text()|Para uma coluna com o nome de text(), o valor da cadeia de caracteres daquela coluna é adicionado a um nó de texto.|  
|comment()|Para uma coluna com o nome de comment(), o valor da cadeia de caracteres daquela coluna é adicionado a um nó de texto.|  
|node()|Para uma coluna com o nome de node(), o resultado é o mesmo que quando o nome da coluna é um caractere curinga (*).|  
|instrução-de-processamento(nome)|Para uma coluna com o nome de uma instrução de processamento, o valor da cadeia de caracteres daquela coluna é adicionado como o valor de PI do nome de destino da instrução de processamento.|  
  
 A consulta a seguir mostra o uso dos testes de nó como nomes de coluna. Ela adiciona nós de texto e comentários no XML resultante.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
        'Example of using node tests such as text(), comment(), processing-instruction()'                as "comment()",  
        'Some PI'                   as "processing-instruction(PI)",  
        'Employee name and address data' as "text()",  
        'middle name is optional'        as "EmpName/text()",  
        FirstName                        as "EmpName/First",   
        MiddleName                       as "EmpName/Middle",   
        LastName                         as "EmpName/Last",  
        AddressLine1                     as "Address/AddrLine1",  
        AddressLine2                     as "Address/AddrLIne2",  
        City                             as "Address/City"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P   
    ON P.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS BAE  
    ON BAE.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BAE.AddressID = A.AddressID  
WHERE  E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Este é o resultado:  
  
 `<row EmpID="1">`  
  
 `<!--Example of using node tests such as text(), comment(), processing-instruction() -->`  
  
 `<?PI Some PI?>`  
  
 `Employee name and address data`  
  
 `<EmpName>middle name is optional`  
  
 `<First>Ken</First>`  
  
 `<Last>Sánchez</Last>`  
  
 `</EmpName>`  
  
 `<Address>`  
  
 `<AddrLine1>4350 Minute Dr.</AddrLine1>`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</row>`  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
