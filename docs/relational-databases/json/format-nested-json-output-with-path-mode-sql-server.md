---
title: "Formatar a saída JSON aninhada com modo PATH (SQL Server) | Microsoft Docs"
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
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6deec926bf016b43ee1476a09cbe2b75c3166239
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>Formatar a saída JSON aninhada com modo PATH (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para manter o controle total sobre a saída da cláusula **FOR JSON**, especifique a opção **PATH**.  
  
 O modo**PATH** permite criar objetos wrapper e aninhar propriedades complexas. Os resultados são formatados como uma matriz de objetos JSON.  
  
A alternativa é usar a opção **AUTO** para formatar a saída automaticamente com base na estrutura da instrução **SELECT**.
 -   Para mais informações sobre a opção **AUTO**, consulte [Formatar a saída JSON automaticamente com o modo AUTO](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).
 -   Para obter uma visão geral de ambas as opções, consulte [Formatar resultados da consulta como JSON com FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).
 
Aqui estão alguns exemplos da cláusula **FOR JSON** com a opção **PATH** . Formate resultados aninhados usando nomes de colunas separados por ponto ou por meio de consultas aninhadas, conforme mostrado nos exemplos a seguir. Por padrão, os valores nulos não são incluídos na saída **FOR JSON**.  

## <a name="example---dot-separated-column-names"></a>Exemplo: nomes de colunas separadas por pontos  
 A consulta a seguir formata as primeiras cinco linhas da tabela AdventureWorks Person como JSON.  

A cláusula FOR JSON PATH usa o nome da coluna ou o alias da coluna para determinar o nome da chave na saída JSON. Se um alias contiver pontos, a opção PATH criará objetos aninhados.  

 **Consulta**  
  
```sql  
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
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
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
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>Exemplo: várias tabelas  
 Se você referenciar mais de uma tabela em uma consulta, o FOR JSON PATH aninhará cada coluna usando seu alias. A consulta a seguir cria um objeto JSON por par (OrderHeader, OrderDetails) inserido na consulta. 
  
 **Consulta**  
  
```sql  
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
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  
  
## <a name="see-also"></a>Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

