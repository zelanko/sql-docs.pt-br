---
title: "Usar OPENJSON com o esquema padr&#227;o (SQL Server) | Microsoft Docs"
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
  - "OPENJSON, com o esquema padrão"
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Usar OPENJSON com o esquema padr&#227;o (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use **OPENJSON** com o esquema padrão para retornar uma tabela com uma linha para cada propriedade do objeto ou para cada elemento na matriz.  
  
 Aqui estão alguns exemplos que usam **OPENJSON** com o esquema padrão. Para obter mais informações e mais exemplos, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## Exemplo – retornar cada propriedade de um objeto  
 **Consulta**  
  
```tsql  
SELECT * FROM OPENJSON('{"name":"John","surname":"Doe","age":45}')  
```  
  
 **Resultados**  
  
|Chave|Valor|  
|---------|-----------|  
|name|John|  
|sobrenome|Doe|  
|idade|45|  
  
## Exemplo – retornar cada elemento de uma matriz  
 **Consulta**  
  
```tsql  
SELECT [key], value FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]')  
```  
  
 **Resultados**  
  
|Chave|Valor|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## Exemplo – converter JSON em uma tabela temporária  
 A consulta a seguir retorna todas as propriedades do objeto **informações** .  
  
```tsql  
SET @json = N'{  
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
  
SELECT * FROM OPENJSON(@json, N'lax $.info')  
```  
  
 **Resultados**  
  
|Chave|Valor|Tipo|  
|---------|-----------|----------|  
|tipo|1|0|  
|address|{"cidade": "Bristol", "região": "Avon", "país": "Inglaterra"}|5|  
|marcas|["Esporte", "Polo aquático"]|4|  
  
## Exemplo – combinar dados relacionais combinar e dados JSON  
 No exemplo a seguir, a tabela SalesOrderHeader tem uma coluna de texto SalesReason que contém uma matriz de SalesOrderReasons no formato JSON. Os objetos SalesOrderReasons contêm propriedades como "Fabricante" e "Qualidade". O exemplo cria um relatório que une cada linha do pedido de venda aos motivos de vendas relacionados expandindo a matriz JSON de motivos de vendas como se os motivos estivessem armazenados em uma tabela filho separada.  
  
```tsql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
    CROSS APPLY OPENJSON (SalesReasons)  
  
```  
  
 Neste exemplo, OPENJSON retorna uma tabela de motivos de vendas em que as razões aparecem como a coluna de valor. O operador CROSS APPLY une cada linha do pedido de venda às linhas retornadas pela função com valor de tabela OPENJSON.  
  
## Consulte também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  