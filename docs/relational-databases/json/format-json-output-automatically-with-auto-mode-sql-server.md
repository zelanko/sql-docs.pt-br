---
description: Formatar saída JSON automaticamente com o Modo AUTO (SQL Server)
title: Formatar Saída JSON Automaticamente com o Modo AUTO
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7161ce97faa4d1baab514df45429592629e2518b
ms.sourcegitcommit: 346a37242f889d76cd783f55aeed98023c693610
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91765733"
---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>Formatar saída JSON automaticamente com o Modo AUTO (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Para formatar a saída da cláusula **FOR JSON** automaticamente com base na estrutura da instrução **SELECT**, especifique a opção **AUTO**.  
  
Ao especificar a opção **AUTO**, o formato da saída JSON é determinado automaticamente com base na ordem das colunas na lista SELECT e suas tabelas de origem. Você não pode alterar esse formato.
 
A alternativa é usar a opção **PATH** para manter o controle sobre a saída.
-   Para mais informações sobre a opção **PATH**, consulte [Formatar a saída JSON aninhada com o modo PATH](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).
-   Para obter uma visão geral de ambas as opções, consulte [Formatar resultados da consulta como JSON com FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

Uma consulta que usa a opção **FOR JSON AUTO** deve ter uma cláusula **FROM** .  
  
Aqui estão alguns exemplos da cláusula **FOR JSON** com a opção **AUTO** . O [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) é o editor de consulta recomendado para consultas JSON porque ele formata automaticamente os resultados JSON (como visto neste artigo) em vez de exibir uma cadeia de caracteres simples.
  
## <a name="examples"></a>Exemplos

### <a name="example-1"></a>Exemplo 1
 **Consulta**  
  
Quando uma consulta referencia somente uma tabela, os resultados da cláusula FOR JSON AUTO são semelhantes aos da FOR JSON PATH. Nesse caso, FOR JSON AUTO não criará objetos aninhados. A única diferença é que a FOR JSON AUTO gera aliases separadas por pontos (por exemplo, `Info.MiddleName` no exemplo a seguir) como chaves com pontos, não como objetos aninhados.  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **Resultado**  
  
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

### <a name="example-2"></a>Exemplo 2

**Consulta**  
  
Quando você une tabelas, as colunas na primeira tabela são geradas como propriedades do objeto raiz. As colunas na segunda tabela são geradas como propriedades de um objeto aninhado. O nome da tabela ou o alias da segunda tabela (por exemplo, `D` no exemplo a seguir) é usado como o nome da matriz aninhada.  
  
```sql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
**Resultado**  
  
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

### <a name="example-3"></a>Exemplo 3:
 
**Consulta**  
Em vez de usar o FOR JSON AUTO, você pode aninhar uma subconsulta FOR JSON PATH na instrução SELECT, conforme mostrado no exemplo a seguir. Este exemplo produz o mesmo resultado do exemplo anterior.  
  
```sql  
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
  
**Resultado**  
  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>Consulte Também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
