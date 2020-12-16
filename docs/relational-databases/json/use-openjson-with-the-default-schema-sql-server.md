---
description: Usar OPENJSON com o esquema padrão
title: Usar OPENJSON com o esquema padrão
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f68c6097cf07152292f2ac5f27d3e080c4b4b449
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481117"
---
# <a name="use-openjson-with-the-default-schema"></a>Usar OPENJSON com o esquema padrão 
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

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
|name|John|  
|sobrenome|Doe|  
|age|45|  
  
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
  
|Chave|Valor|Type|  
|---------|-----------|----------|  
|type|1|0|  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
