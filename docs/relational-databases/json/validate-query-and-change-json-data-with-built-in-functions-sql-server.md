---
title: Validar, consultar e alterar dados JSON com funções internas
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ddc5fb198a62374fc43ebacb5fa7423ac9fadd5
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340234"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Validar, consultar e alterar dados JSON com funções internas (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O suporte interno para JSON inclui as funções internas a seguir, descritas brevemente neste tópico.  
  
-   [ISJSON](#ISJSON) testa se uma cadeia de caracteres contém JSON válido.  
  
-   [JSON_VALUE](#VALUE) extrai um valor escalar de uma cadeia de caracteres JSON.  
  
-   [JSON_QUERY](#QUERY) extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.  
  
-   [JSON_MODIFY](#MODIFY) atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Texto JSON para os exemplos nesta página

Os exemplos nesta página usam o texto JSON semelhante ao conteúdo mostrado no exemplo a seguir:

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller",
         "givenName": "Lisa",
         "gender": "female",
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Esse documento JSON, que contém elementos complexos aninhados, é armazenado na seguinte tabela de exemplo:

```sql
CREATE TABLE Families (
   id int identity constraint PK_JSON_ID primary key,
   doc nvarchar(max)
)
``` 

##  <a name="ISJSON"></a> Validar texto JSON por meio da função ISJSON  
 A função **ISJSON** testa se uma cadeia de caracteres contém JSON válido.  
  
O exemplo a seguir retorna linhas nas quais a coluna JSON contém um texto JSON válido. Observe que, sem a restrição JSON explícita, é possível inserir qualquer texto na coluna NVARCHAR:  
  
```sql  
SELECT *
FROM Families
WHERE ISJSON(doc) > 0 
```  

Para obter mais informações, veja [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extrair um valor de texto JSON por meio da função JSON_VALUE  
A função **JSON_VALUE** extrai um valor escalar de uma cadeia de caracteres JSON. A seguinte consulta retornará os documentos em que o campo JSON `id` corresponde ao valor `AndersenFamily`, ordenado pelos campos JSON `city` e `state`:

```sql  
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       JSON_VALUE(f.doc, '$.address.county') AS County
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
ORDER BY JSON_VALUE(f.doc, '$.address.city') DESC, JSON_VALUE(f.doc, '$.address.state') ASC
```  

Os resultados dessa consulta são mostrados na seguinte tabela:

| Nome | City | Município |
| --- | --- | --- |
| AndersenFamily | NOVA IORQUE | Manhattan |

Para obter mais informações, veja [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extrair um objeto ou uma matriz de texto JSON por meio da função JSON_QUERY  

A função **JSON_QUERY** extrai um objeto ou uma matriz de uma cadeia de caracteres JSON. O exemplo a seguir mostra como retornar um fragmento JSON nos resultados da consulta.  
  
```sql
SELECT JSON_QUERY(f.doc, '$.address') AS Address,
       JSON_QUERY(f.doc, '$.parents') AS Parents,
       JSON_QUERY(f.doc, '$.parents[0]') AS Parent0
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
```  
Os resultados dessa consulta são mostrados na seguinte tabela:

| Endereço | Pais | Parent0 |
| --- | --- | --- |
| { "state": "NY", "county": "Manhattan", "city": "NY" } | [{ "familyName": "Wakefield", "givenName": "Robin" }, {"familyName": "Miller", "givenName": "Ben" } ]| { "familyName": "Wakefield", "givenName": "Robin" } |

Para obter mais informações, veja [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  

## <a name="parse-nested-json-collections"></a>Analisar coleção JSON aninhadas

A função `OPENJSON` permite transformar a submatriz JSON no conjunto de linhas e, em seguida, associá-la ao elemento pai. Como um exemplo, é possível retornar todos os documentos da família e “ingressá-los” com seus objetos `children` armazenados como uma matriz JSON interna:

```sql
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       c.givenName, c.grade
FROM Families f
        CROSS APPLY OPENJSON(f.doc, '$.children')
            WITH(grade int, givenName nvarchar(100))  c
```

Os resultados dessa consulta são mostrados na seguinte tabela:

| Nome | City | givenName | grade |
| --- | --- | --- | --- |
| AndersenFamily | NOVA IORQUE | Jesse | 1 |
| AndersenFamily | NOVA IORQUE | Lisa | 8 |

Estamos obtendo duas linhas como um resultado, porque uma linha pai é ingressada com duas linhas filho produzidas analisando dois elementos da submatriz filho. A função `OPENJSON` analisa o fragmento `children` da coluna `doc` e retorna `grade` e `givenName` de cada elemento como um conjunto de linhas. Esse conjunto de linhas pode ser ingressado com o documento pai.
 
## <a name="query-nested-hierarchical-json-sub-arrays"></a>Consultar submatrizes JSON hierárquicas aninhadas

É possível aplicar várias chamadas `CROSS APPLY OPENJSON` para consultar estruturas JSON aninhadas. O documento JSON usado neste exemplo tem uma matriz aninhada chamada `children`, em que cada filho tem uma matriz aninhada de `pets`. A consulta a seguir analisará os filhos de cada documento, retornará cada objeto de matriz como linha e, em seguida, analisará a matriz `pets`:

```sql
SELECT  familyName,
    c.givenName AS childGivenName,
    c.firstName AS childFirstName,
    p.givenName AS petName 
FROM Families f 
    CROSS APPLY OPENJSON(f.doc) 
        WITH (familyName nvarchar(100), children nvarchar(max) AS JSON)
        CROSS APPLY OPENJSON(children) 
        WITH (givenName nvarchar(100), firstName nvarchar(100), pets nvarchar(max) AS JSON) as c
            OUTER APPLY OPENJSON (pets)
            WITH (givenName nvarchar(100))  as p
```

A primeira chamada `OPENJSON` retornará o fragmento da matriz `children` que usa a cláusula AS JSON. Esse fragmento de matriz será fornecido à segunda função `OPENJSON` que retornará `givenName`, `firstName` de cada filho, além da matriz de `pets`. A matriz de `pets` será fornecida à terceira função `OPENJSON` que retornará o `givenName` do animal de estimação.
Os resultados dessa consulta são mostrados na seguinte tabela:

| familyName | childGivenName | childFirstName | petName |
| --- | --- | --- | --- |
| AndersenFamily | Jesse | Merriam | Goofy |
| AndersenFamily | Jesse | Merriam | Shadow |
| AndersenFamily | Lisa | Miller| `NULL` |

O documento raiz é ingressado com duas linhas `children` retornadas pela primeira chamada `OPENJSON(children)` que cria duas linhas (ou tuplas). Em seguida, cada linha será ingressada com as novas linhas geradas por `OPENJSON(pets)` usando o operador `OUTER APPLY`. Jesse tem dois animais de estimação, então `(AndersenFamily, Jesse, Merriam)` é ingressado com duas linhas geradas para Goofy e Shadow. Lisa não tem animais de estimação, portanto não há linhas retornadas por `OPENJSON(pets)` para essa tupla. No entanto, como estamos usando `OUTER APPLY`, estamos obtendo `NULL` na coluna. Se colocássemos `CROSS APPLY` em vez de `OUTER APPLY`, Lisa não seria retornada no resultado, porque não há linhas de animais que pudessem ser ingressadas com essa tupla.

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
  
|Caminho|**JSON_VALUE** retorna|**JSON_QUERY** retorna|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL ou erro|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL ou erro|  
|**. $b**|NULL ou erro|[1,2]|  
|**$.b[0]**|1|NULL ou erro|  
|**$.c**|hi|NULL ou erro|  
  
## <a name="test-json_value-and-json_query-with-the-adventureworks-sample-database"></a>Teste JSON_VALUE e JSON_QUERY com o banco de dados de exemplo AdventureWorks  
Teste as funções internas descritas neste tópico executando os exemplos a seguir com o banco de dados de exemplo AdventureWorks. Para obter informações sobre onde obter o AdventureWorks e sobre como adicionar dados JSON para o teste executando um script, consulte [Fazer um test drive do suporte interno a JSON](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database).
  
Nos exemplos a seguir, a coluna `Info` na tabela `SalesOrder_json` contém texto JSON.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Exemplo 1 - Retornar dados JSON e colunas padrão  
A consulta a seguir retorna os valores de colunas relacionais padrão e de uma coluna JSON.  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Exemplo 2- Agregar e filtrar valores JSON  
A consulta a seguir agrega subtotais por nome do cliente (armazenado em JSON) e status (armazenado em uma coluna comum). Em seguida, ela filtra os resultados por cidade (armazenado em JSON) e OrderDate (armazenado em uma coluna comum).  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> Atualizar valores de propriedade em texto JSON por meio da função JSON_MODIFY  
A função **JSON_MODIFY** atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.  
  
O exemplo a seguir atualiza o valor de uma propriedade JSON em uma variável que contém JSON.  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 Para obter mais informações, veja [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [Expressões de caminho JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
