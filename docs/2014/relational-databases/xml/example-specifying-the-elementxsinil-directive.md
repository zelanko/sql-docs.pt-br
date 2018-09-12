---
title: 'Exemplo: especificando a diretiva ELEMENTXSINIL | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 91b05e3b4ff33e9c426b24b4c55e86958ae88647
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889152"
---
# <a name="example-specifying-the-elementxsinil-directive"></a>Exemplo: Especificando a diretiva ELEMENTXSINIL
  Quando você especifica a política ELEMENT para recuperar o XML centrado em elemento, se a coluna tiver um valor NULL, o elemento correspondente não será gerado pelo modo EXPLICIT. Opcionalmente, é possível especificar a diretiva ELEMENTXSINIL para solicitar o elemento gerador de valores NULL em que o atributo `xsi:nil` é definido com o valor TRUE.  
  
 A consulta a seguir constrói XML que inclui um endereço de funcionário. Para colunas `AddressLine2` e `City` , os nomes das colunas especificam a diretiva `ELEMENTXSINIL` . Isso gera o elemento para valores NULL nas colunas `AddressLine2` e `City` do conjunto de linhas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID  as [Employee!1!EmpID],  
       BEA.AddressID as [Employee!1!AddressID],  
       NULL        as [Address!2!AddressID],  
       NULL        as [Address!2!AddressLine1!ELEMENT],  
       NULL        as [Address!2!AddressLine2!ELEMENTXSINIL],  
       NULL        as [Address!2!City!ELEMENTXSINIL]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       BEA.AddressID,  
       A.AddressID,  
       AddressLine1,   
       AddressLine2,  
       City   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BEA.AddressID = A.AddressID  
ORDER BY [Employee!1!EmpID],[Address!2!AddressID]  
FOR XML EXPLICIT;  
```  
  
 Este é o resultado parcial:  
  
 `<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `EmpID="1" AddressID="249">`  
  
 `<Address AddressID="249">`  
  
 `<AddressLine1>4350 Minute Dr.</AddressLine1>`  
  
 `<AddressLine2 xsi:nil="true" />`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo EXPLICIT com FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
