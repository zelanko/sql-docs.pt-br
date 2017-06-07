---
title: "Validar, consultar e alterar dados JSON com funções internas (SQL Server) | Microsoft Docs"
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
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d9cdb66be3f6831ad5c2a61258c25425f98c0988
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Validar, consultar e alterar dados JSON com funções internas (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  O suporte interno para JSON inclui as funções internas a seguir, descritas neste tópico.  
  
-   [ISJSON](#ISJSON) testa se uma cadeia de caracteres contém JSON válido.  
  
-   [JSON_VALUE](#VALUE) extrai um valor escalar de uma cadeia de caracteres JSON.  
  
-   [JSON_QUERY](#QUERY) extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.  
  
-   [JSON_MODIFY](#MODIFY) atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Texto JSON para os exemplos nesta página
O exemplos nesta página usam o texto JSON a seguir, que contém um elemento complexo.

```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }' 
``` 

##  <a name="ISJSON"></a> Validar texto JSON por meio da função ISJSON  
 A função **ISJSON** testa se uma cadeia de caracteres contém JSON válido.  
  
 O exemplo a seguir retorna o texto JSON se a coluna contiver JSON válido.  
  
```sql  
SELECT id,json_col
FROM tab1
WHERE ISJSON(json_col)>0 
```  
  
 Para obter mais informações, veja [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extrair um valor de texto JSON por meio da função JSON_VALUE  
 A função **JSON_VALUE** extrai um valor escalar de uma cadeia de caracteres JSON.  
  
 O exemplo a seguir extrai o valor de uma propriedade JSON para uma variável local.  
  
```sql  
SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')  
```  
  
 Para obter mais informações, veja [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extrair um objeto ou uma matriz de texto JSON por meio da função JSON_QUERY  
 A função **JSON_QUERY** extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.  
 
 O exemplo a seguir mostra como retornar um fragmento JSON nos resultados da consulta.  
  
```sql  
SELECT FirstName,LastName,JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
 Para obter mais informações, veja [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
##  <a name="JSONCompare"></a> Comparar JSON_VALUE e JSON_QUERY  
 A principal diferença entre **JSON_VALUE** e **JSON_QUERY** é que **JSON_VALUE** retorna um valor escalar, enquanto **JSON_QUERY** retorna um objeto ou uma matriz.  
  
 Considere o seguinte texto JSON de exemplo.  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
 Neste texto JSON de exemplo, membros de dados "a" e "c" são valores de cadeia de caracteres, enquanto o membro de dados "b" é uma matriz. **JSON_VALUE** e **JSON_QUERY** retornam os seguintes resultados:  
  
|Consulta|**JSON_VALUE** retorna|**JSON_QUERY** retorna|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL ou erro|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL ou erro|  
|**. $b**|NULL ou erro|[1,2]|  
|**$.b[0]**|1|NULL ou erro|  
|**$.c**|hi|NULL ou erro|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>Teste JSON_VALUE e JSON_QUERY com o banco de dados de exemplo AdventureWorks  
 Teste as funções internas descritas neste tópico, executando os exemplos a seguir com o banco de dados de exemplo AdventureWorks, que contém dados JSON. Para obter o banco de dados de exemplo AdventureWorks [clique aqui](http://www.microsoft.com/en-us/download/details.aspx?id=49502).  
  
 Nos exemplos a seguir, a coluna de informações na tabela de SalesOrder_json contém texto JSON.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Exemplo 1 - Retornar dados JSON e colunas padrão  
 A consulta a seguir retorna os valores e colunas relacionais padrão de uma coluna JSON.  
  
```sql  
SELECT SalesOrderNumber,OrderDate,Status,ShipDate,Status,AccountNumber,TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info)>0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Exemplo 2- Agregar e filtrar valores JSON  
 A consulta a seguir agrega subtotais por nome do cliente (armazenado em JSON) e status (armazenado em uma coluna comum). Em seguida, ela filtra os resultados por cidade (armazenado em JSON) e OrderDate (armazenado em uma coluna comum).  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info,'$.Customer.Name') AS Customer,Status,SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info,'$.ShippingInfo.City')=@city
 AND OrderDate>'1/1/2015'
GROUP BY JSON_VALUE(Info,'$.Customer.Name'),Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> Atualizar valores de propriedade em texto JSON por meio da função JSON_MODIFY  
 A função **JSON_MODIFY**  atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.  
  
 O exemplo a seguir atualiza o valor de uma propriedade em uma variável que contém JSON.  
  
```sql  
SET @info=JSON_MODIFY(@jsonInfo,"$.info.address[0].town",'London')    
```  
  
 Para obter mais informações, veja [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-built-in-json-support-in-sql-server"></a>Saiba mais sobre suporte interno a JSON no SQL Server  
 [Postagens no blog por Jovan Popovic, gerente de programas da Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>Consulte também  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [Expressões de caminho JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  

