---
title: "Formatar a sa&#237;da JSON aninhada com modo PATH (SQL Server) | Microsoft Docs"
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
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Formatar a sa&#237;da JSON aninhada com modo PATH (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para manter o controle total sobre o formato da saída JSON, especifique a opção **PATH** com uma cláusula **FOR JSON** .  
  
 O modo**PATH** permite criar objetos wrapper e aninhar propriedades complexas. Os resultados são formatados como uma matriz de objetos JSON.  
  
 Aqui estão alguns exemplos da cláusula **FOR JSON** com a opção **PATH** . Formate resultados aninhados usando nomes de colunas separados por ponto ou por meio de consultas aninhadas, conforme mostrado nos exemplos a seguir. Por padrão, os valores nulos não são incluídos na saída.  
  
## Exemplo: nomes de colunas separadas por pontos  
 A consulta a seguir formata as primeiras cinco linhas da tabela AdventureWorks Person como JSON.  
  
 **Consulta**  
  
```tsql  
SELECT TOP 5   
      BusinessEntityID As Id,  
      FirstName, LastName,  
      Title As 'Info.Title',  
      MiddleName As 'Info.MiddleName'  
  FROM Person.Person  
  FOR JSON PATH  
```  
  
 **Resultado**  
  
```json  
[  
    {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
    {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
    {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
    {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
    {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
]  
```  
  
 A cláusula FOR JSON PATH usará o nome da coluna ou o alias da coluna para determinar o nome da chave na saída JSON. Se algum alias contiver pontos, a cláusula FOR JSON PATH criará objeto aninhado. Observe que as células com valores NULL não serão geradas na saída.  
  
## Exemplo: várias tabelas  
 Se você referenciar mais de uma tabela na consulta, os resultados serão representados como uma lista simples e, em seguida, o FOR JSON PATH aninha cada coluna usando seu alias. A consulta a seguir cria um objeto JSON por par (OrderHeader OrderDetails) inserido na consulta:  
  
 **Consulta**  
  
```tsql  
SELECT TOP 2 SalesOrderNumber AS 'Order.Number',  
       OrderDate AS 'Order.Date',  
       UnitPrice AS 'Product.Price',  
       OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
  INNER JOIN Sales.SalesOrderDetail D  
    ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH  
```  
  
 **Resultado**  
  
```json  
[  
  {  
    "Order":{  
        "Number":"SO43659",  
        "Date":"2011-05-31T00:00:00"  
      },  
    "Product":{  
         "Price":2024.9940,  
         "Quantity":1  
     }  
  },  
  {  
    "Order":{ "Number":"SO43659“ },  
    "Product":{"Price":2024.9940}  
  }  
]  
```  
  
## Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  