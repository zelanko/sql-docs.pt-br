---
title: "Formatar sa&#237;da JSON automaticamente com o Modo AUTO (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON AUTO"
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# Formatar sa&#237;da JSON automaticamente com o Modo AUTO (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para formatar a saída JSON automaticamente com base na estrutura da instrução **SELECT** , especifique a opção  **AUTO** com a cláusula **FOR JSON** .  
  
 Com a opção **AUTO** , o formato da saída JSON é determinado automaticamente com base na ordem das colunas na lista SELECT e suas tabelas de origem. Você não pode alterar esse formato.  
  
 Uma consulta que usa a opção **FOR JSON AUTO** deve ter uma cláusula **FROM** .  
  
 Aqui estão alguns exemplos da cláusula **FOR JSON** com a opção **AUTO** .  
  
## Exemplos  
 **Consulta 1**  
  
 Os resultados da cláusula FOR JSON AUTO serão semelhantes aos da FOR JSON PATH se uma tabela for usada na consulta. Nesse caso, FOR JSON AUTO não criará objetos aninhados. A única diferença é que os aliases separados por ponto serão gerados como chaves com pontos (ou seja, FOR JSON AUTO não usará aliases de coluna para a formatação).  
  
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
[  
      {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info.MiddleName":"J"},  
      {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info.MiddleName":"Lee"},  
      {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
      {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
      {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info.Title":"Ms.","Info.MiddleName":"A"}  
]  
```  
  
 **Consulta 2**  
  
 Quando você une tabelas, as colunas na primeira tabela são geradas como propriedades do objeto raiz. As colunas na segunda tabela são geradas como propriedades de um objeto aninhado. O nome da tabela ou alias da segunda tabela é usado como um nome da matriz aninhada.  
  
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
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            {"UnitPrice":24.99, "OrderQty":1  }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO43659" ,  
       "D":[  
          { "UnitPrice":34.40  },  
          { "UnitPrice":134.24, "OrderQty":5 }  
        ]  
  }  
]  
  
```  
  
## Exemplos - Gerar uma saída JSON aninhada  
 Em vez de FOR JSON AUTO, você pode escrever consultas FOR JSON aninhadas colocadas na parte SELECT da consulta principal com a cláusula FOR JSON PATH, conforme mostrado nos exemplos a seguir.  
  
 **Consulta 1**  
  
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
  
 **Resultado 1**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            { "UnitPrice":24.99,  "OrderQty":1 }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO4390" ,  
       "D":[  
            { "UnitPrice":24.99 }  
        ]  
  }  
]  
  
```  
  
## Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  