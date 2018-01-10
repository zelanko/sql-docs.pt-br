---
title: "Usar OPENJSON com o esquema padrão (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3da875380580bcf7151db13c0b14280a9790d5dc
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>Usar OPENJSON com o esquema padrão (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Use **OPENJSON** com o esquema padrão para retornar uma tabela com uma linha para cada propriedade do objeto ou para cada elemento na matriz.  
  
 Aqui estão alguns exemplos que usam **OPENJSON** com o esquema padrão. Para obter mais informações e mais exemplos, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="example---return-each-property-of-an-object"></a>Exemplo – retornar cada propriedade de um objeto  
 **Consulta**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **Resultados**  
  
|Chave|Valor|  
|---------|-----------|  
|NAME|John|  
|sobrenome|Doe|  
|idade|45|  
  
## <a name="example---return-each-element-of-an-array"></a>Exemplo – retornar cada elemento de uma matriz  
 **Consulta**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **Resultados**  
  
|Chave|Valor|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## <a name="example---convert-json-to-a-temporary-table"></a>Exemplo – converter JSON em uma tabela temporária  
 A consulta a seguir retorna todas as propriedades do objeto **informações** .  
  
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json=N'{  
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

SELECT *
FROM OPENJSON(@json,N'lax $.info')
```  
  
 **Resultados**  
  
|Chave|Valor|Tipo|  
|---------|-----------|----------|  
|Tipo|1|0|  
|address|{"cidade": "Bristol", "região": "Avon", "país": "Inglaterra"}|5|  
|marcas|["Esporte", "Polo aquático"]|4|  
  
## <a name="example---combine-relational-data-and-json-data"></a>Exemplo – combinar dados relacionais combinar e dados JSON  
 No exemplo a seguir, a tabela SalesOrderHeader tem uma coluna de texto SalesReason que contém uma matriz de SalesOrderReasons no formato JSON. Os objetos SalesOrderReasons contêm propriedades como "Fabricante" e "Qualidade". O exemplo cria um relatório que une cada linha do pedido de venda aos motivos de vendas relacionados expandindo a matriz JSON de motivos de vendas como se os motivos estivessem armazenados em uma tabela filho separada.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
 Neste exemplo, OPENJSON retorna uma tabela de motivos de vendas em que as razões aparecem como a coluna de valor. O operador CROSS APPLY une cada linha do pedido de venda às linhas retornadas pela função com valor de tabela OPENJSON.  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para ver várias soluções específicas, casos de uso e recomendações, consulte as [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no Banco de Dados SQL do Azure por Jovan Popovic, gerente de programas da Microsoft.
  
## <a name="see-also"></a>Consulte Também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  
