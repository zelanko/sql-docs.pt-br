---
title: Colunas com um nome especificado como um caractere curinga | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e03000db7890bd87e22799b6bf525b9a1194c2a4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Colunas com um nome especificado como um caractere curinga
  Se o nome da coluna especificado for um caractere curinga (\*), o conteúdo dessa coluna será inserido como se não houvesse nenhum nome de coluna especificado. Se essa for uma coluna de tipo não**xml** , o conteúdo da coluna será inserido como um nó de texto, conforme mostrado no exemplo a seguir:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Este é o resultado:  
  
 `<row EmpID="1">KenJSánchez</row>`  
  
 Se a coluna for de tipo **xml** , a árvore XML correspondente será inserida. Por exemplo, a coluna a seguir especifica "*" para o nome da coluna que contém o XML retornado pelo XQuery em relação à coluna Instructions.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 Este é o resultado. O XML retornado por XQuery é inserido sem um elemento de encapsulamento.  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
