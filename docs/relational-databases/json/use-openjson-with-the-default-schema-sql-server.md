---
title: Usar OPENJSON com o esquema padrão (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea2154045da369c045eea39591266cfb02f53722
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630214"
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-blog-posts"></a>Postagens no blog da Microsoft  
  
Para ver soluções específicas, casos de uso e recomendações, consulte as [postagens no blog](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre o suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure.  

### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
