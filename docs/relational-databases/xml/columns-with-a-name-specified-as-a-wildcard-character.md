---
title: Colunas com um nome especificado como um caractere curinga | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f49fdac97f1a580a24bc50840ec58fc6efe0d65a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113057"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Colunas com um nome especificado como um caractere curinga

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Se o nome da coluna especificado for um caractere curinga (\*), o conteúdo dessa coluna será inserido como se não houvesse nenhum nome de coluna especificado. Se essa for uma coluna de tipo não**xml** , o conteúdo da coluna será inserido como um nó de texto, conforme mostrado no exemplo a seguir:  
  
```sql
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

```xml
<row EmpID="1">KenJSánchez</row>
```

 Se a coluna for de tipo **xml** , a árvore XML correspondente será inserida. Por exemplo, a coluna a seguir especifica "*" para o nome da coluna que contém o XML retornado pelo XQuery em relação à coluna Instructions.  
  
```sql
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
```  
  
 Este é o resultado. O XML retornado por XQuery é inserido sem um elemento de encapsulamento.  

```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location LocationID="10">...</MI:Location>
  <MI:Location LocationID="20">...</MI:Location>
  ...
</row>
```

## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
