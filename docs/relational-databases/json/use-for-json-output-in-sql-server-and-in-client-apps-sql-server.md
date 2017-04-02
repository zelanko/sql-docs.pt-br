---
title: "Usar a sa&#237;da FOR JSON no SQL Server e em aplicativos cliente (SQL Server) | Microsoft Docs"
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
  - "FOR JSON, usando em aplicativos cliente"
  - "FOR JSON, usando no SQL Server"
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Usar a sa&#237;da FOR JSON no SQL Server e em aplicativos cliente (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Os exemplos a seguir demonstram algumas maneiras de usar a cláusula **FOR JSON** ou sua saída em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em aplicativos cliente.  
  
## Use a saída FOR JSON em variáveis do SQL Server  
 A saída da cláusula FOR JSON é do tipo NVARCHAR(MAX), portanto pode ser atribuída a qualquer variável, conforme mostrado no exemplo a seguir.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## Usar a saída FOR JSON em funções definidas pelo usuário do SQL Server  
 Você pode criar funções definidas pelo usuário que formate conjuntos de resultados como JSON e retornam essa saída JSON. O exemplo a seguir cria uma função definida pelo usuário que busca linhas de detalhes de um pedido de vendas e formata como uma matriz JSON.  
  
```tsql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
  RETURN (SELECT UnitPrice, OrderQty  
          FROM Sales.SalesOrderDetail  
          WHERE SalesOrderID = @salesOrderId  
          FOR JSON AUTO)  
END  
```  
  
 Você pode usar essa função em um lote ou consulta, como mostrado no exemplo a seguir.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)  
PRINT dbo.GetSalesOrderDetails(43659)  
SELECT TOP 10 H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details  
FROM Sales.SalesOrderHeader H  
```  
  
## Mesclar dados pai e filho em uma única tabela  
 No exemplo a seguir, cada conjunto de linhas filho é formatado como uma matriz JSON e torna-se o valor da coluna de detalhes na tabela pai.  
  
```tsql  
select top 10 SalesOrderId, OrderDate,  
     (select top 3 UnitPrice, OrderQty  
        from Sales.SalesOrderDetail D  
        where H.SalesOrderId = D.SalesOrderID  
        for json auto) as Details  
into SalesOrder  
from Sales.SalesOrderHeader H  
```  
  
## Atualizar os dados nas colunas JSON  
 O exemplo a seguir demonstra que você pode atualizar o valor das colunas que contêm texto JSON.  
  
```tsql  
UPDATE SalesOrder  
SET Details =  
    (SELECT TOP 1 UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail D  
      WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
     FOR JSON AUTO)  
```  
  
## Use a saída JSON em um aplicativo cliente C#  
 O exemplo a seguir mostra como recuperar a saída JSON de uma consulta em um objeto StringBuilder em um aplicativo cliente C#. Suponha que a variável queryWithForJson contém o texto de uma instrução SELECT com uma cláusula FOR JSON.  
  
```csharp  
var cmd = new SqlCommand(queryWithForJson, conn);  
conn.Open();  
var jsonResult = new StringBuilder();  
var reader = cmd.ExecuteReader();  
if (!reader.HasRows)  
{  
    jsonResult.Append("[]");  
}  
else  
{  
    while (reader.Read())  
    {  
        jsonResult.Append(reader.GetValue(0).ToString());  
    }  
}  
```  
  
## Consulte também  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  