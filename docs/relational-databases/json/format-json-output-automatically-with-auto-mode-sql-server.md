---
title: "Formatar saída JSON automaticamente com o Modo AUTO (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3a04977311f1f04171caa1de0d15373d0b3cdf15
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>Formatar saída JSON automaticamente com o Modo AUTO (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Para formatar a saída da cláusula **FOR JSON** automaticamente com base na estrutura da instrução **SELECT**, especifique a opção **AUTO**.  
  
Com a opção **AUTO** , o formato da saída JSON é determinado automaticamente com base na ordem das colunas na lista SELECT e suas tabelas de origem. Você não pode alterar esse formato.
 
 A alternativa é usar a opção **PATH** para manter o controle sobre a saída.
 -   Para mais informações sobre a opção **PATH**, consulte [Formatar a saída JSON aninhada com o modo PATH](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).
 -   Para obter uma visão geral de ambas as opções, consulte [Formatar resultados da consulta como JSON com FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).
  
 Uma consulta que usa a opção **FOR JSON AUTO** deve ter uma cláusula **FROM** .  
  
 Aqui estão alguns exemplos da cláusula **FOR JSON** com a opção **AUTO** .  
  
## <a name="examples"></a>Exemplos  
 **Consulta 1**  
  
Os resultados da cláusula FOR JSON AUTO serão semelhantes aos da FOR JSON PATH quando apenas uma tabela for usada na consulta. Nesse caso, FOR JSON AUTO não criará objetos aninhados. A única diferença é que a FOR JSON AUTO gera aliases separadas por pontos (por exemplo, `Info.MiddleName` no exemplo a seguir) como chaves com pontos, não como objetos aninhados.  
  
```tsql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **Resultado 1**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info.MiddleName": "J"
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info.MiddleName": "Lee"
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info.Title": "Ms.",
    "Info.MiddleName": "A"
}]
```  
  
 **Consulta 2**  
  
 Quando você une tabelas, as colunas na primeira tabela são geradas como propriedades do objeto raiz. As colunas na segunda tabela são geradas como propriedades de um objeto aninhado. O nome da tabela ou o alias da segunda tabela (por exemplo, `D` no exemplo a seguir) é usado como o nome da matriz aninhada.  
  
```tsql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
 **Resultado 2**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO43659",
    "D": [{
        "UnitPrice": 34.40
    }, {
        "UnitPrice": 134.24,
        "OrderQty": 5
    }]
}]
```  
 
 **Consulta 3**  
 Em vez de usar o FOR JSON AUTO, você pode aninhar uma subconsulta FOR JSON PATH na instrução SELECT, conforme mostrado no exemplo a seguir. Este exemplo produz o mesmo resultado do exemplo anterior.  
  
```tsql  
SELECT TOP 2  
    SalesOrderNumber,  
    OrderDate,  
    (SELECT UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail AS D  
      WHERE H.SalesOrderID = D.SalesOrderID  
     FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
 **Resultado 3**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO4390",
    "D": [{
        "UnitPrice": 24.99
    }]
}]
```  
  
## <a name="see-also"></a>Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

