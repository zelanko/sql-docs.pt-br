---
description: Formatar a saída JSON aninhada com modo PATH (SQL Server)
title: Formatar a saída JSON aninhada com modo PATH
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e95ffd1cf5e75f95cc79dc127ac154abc4253a0d
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595099"
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>Formatar a saída JSON aninhada com modo PATH (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sqlserver2016-asdb.md)]

Para manter o controle total sobre a saída da cláusula **FOR JSON**, especifique a opção **PATH**.  
  
O modo **PATH** permite criar objetos wrapper e aninhar propriedades complexas. Os resultados são formatados como uma matriz de objetos JSON.  
  
A alternativa é usar a opção **AUTO** para formatar a saída automaticamente com base na estrutura da instrução **SELECT**.
 -   Para mais informações sobre a opção **AUTO**, consulte [Formatar a saída JSON automaticamente com o modo AUTO](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).
 -   Para obter uma visão geral de ambas as opções, consulte [Formatar resultados da consulta como JSON com FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).
 
Aqui estão alguns exemplos da cláusula **FOR JSON** com a opção **PATH** . Formate resultados aninhados usando nomes de colunas separados por ponto ou por meio de consultas aninhadas, conforme mostrado nos exemplos a seguir. Por padrão, os valores nulos não são incluídos na saída **FOR JSON**.  O [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) é o editor de consulta recomendado para consultas JSON porque ele formata automaticamente os resultados JSON (como visto neste artigo) em vez de exibir uma cadeia de caracteres simples.

## <a name="example---dot-separated-column-names"></a>Exemplo: nomes de colunas separadas por pontos  
A consulta a seguir formata as primeiras cinco linhas da tabela AdventureWorks `Person` como JSON.  

A cláusula **FOR JSON PATH** usa o alias ou nome da coluna para determinar o nome da chave na saída JSON. Se um alias contiver pontos, a opção PATH criará objetos aninhados.  

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
    "LastName": "Sanchez",
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
Se mais de uma tabela for referenciada em uma consulta, o **FOR JSON PATH** aninhará cada coluna usando seu alias. A consulta a seguir cria um objeto JSON por par (OrderHeader, OrderDetails) inserido na consulta. 
  
 **Consulta**  
  
```sql  
SELECT TOP 2 H.SalesOrderNumber AS 'Order.Number',  
        H.OrderDate AS 'Order.Date',  
        D.UnitPrice AS 'Product.Price',  
        D.OrderQty AS 'Product.Quantity'  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>Consulte Também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
