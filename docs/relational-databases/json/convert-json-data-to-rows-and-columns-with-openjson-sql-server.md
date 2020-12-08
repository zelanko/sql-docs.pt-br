---
description: Analisar e transformar dados JSON com OPENJSON (SQL Server)
title: Analisar e transformar dados JSON com OPENJSON
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 519d66511b71cb0045623b239cc82d0e80791968
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595065"
---
# <a name="parse-and-transform-json-data-with-openjson-sql-server"></a>Analisar e transformar dados JSON com OPENJSON (SQL Server)
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

A função de conjunto de linhas **OPENJSON** converte o texto JSON em um conjunto de linhas e colunas. Depois de transformar uma coleção JSON em um conjunto de linhas com **OPENJSON**, é possível executar qualquer consulta SQL nos dados retornados ou inseri-los em uma tabela do SQL Server. 
  
A função **OPENJSON** obtém um único objeto JSON ou uma coleção de objetos JSON e transforma-os em uma ou mais linhas. Por padrão, a função **OPENJSON** retorna os dados a seguir:
-   De um objeto JSON, a função retorna todos os pares chave-valor localizados no primeiro nível.
-   De uma matriz JSON, a função retorna todos os elementos da matriz com seus índices.  

É possível adicionar uma cláusula opcional **WITH** para fornecer um esquema que define explicitamente a estrutura da saída.  
  
## <a name="option-1---openjson-with-the-default-output"></a>Opção 1 – OPENJSON com a saída padrão
Ao usar a função **OPENJSON** sem fornecer um esquema explícito para os resultados, ou seja, sem uma cláusula **WITH** após **OPENJSON**, a função retorna uma tabela com as três colunas a seguir:
1.  O **nome** da propriedade no objeto de entrada (ou o índice do elemento na matriz de entrada).
2.  O **valor** da propriedade ou o elemento da matriz.
3.  O **tipo** (por exemplo, cadeia de caracteres, número, booliano, matriz ou objeto).

O **OPENJSON** retorna cada propriedade do objeto JSON ou cada elemento da matriz como uma linha separada.  

Veja um exemplo rápido que usa **OPENJSON** com o esquema padrão, ou seja, sem a cláusula opcional **WITH**, e retorna uma linha para cada propriedade do objeto JSON.  

**Exemplo**

```sql
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**Resultados**
  
|chave|value|type|  
|---------|-----------|----------|  
|name|John|1|  
|sobrenome|Doe|1|  
|age|45|2|  
|habilidades|["SQL","C#","MVC"]|4|

### <a name="more-info-about-openjson-with-the-default-schema"></a>Mais informações sobre OPENJSON com o esquema padrão

Para obter mais informações e exemplos, consulte [Usar OPENJSON com o esquema padrão &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md).

Para sintaxe e uso, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

## <a name="option-2---openjson-output-with-an-explicit-structure"></a>Opção 2 – Saída OPENJSON com uma estrutura explícita

Quando você especificar um esquema para os resultados usando a cláusula **WITH** da função **OPENJSON**, a função retornará uma tabela com apenas as colunas que você definir na cláusula **WITH**. Na cláusula opcional **WITH**, especifique um conjunto de colunas de saída, seus tipos e os caminhos das propriedades de origem do JSON para cada valor de saída. **OPENJSON** itera na matriz de objetos JSON, lê o valor no caminho especificado para cada coluna e converte o valor no tipo especificado.  

Veja um exemplo rápido que usa **OPENJSON** com um esquema para a saída especificada explicitamente na cláusula **WITH**.  
  
**Exemplo**
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =   
  N'[  
       {  
         "Order": {  
           "Number":"SO43659",  
           "Date":"2011-05-31T00:00:00"  
         },  
         "AccountNumber":"AW29825",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":1  
         }  
       },  
       {  
         "Order": {  
           "Number":"SO43661",  
           "Date":"2011-06-01T00:00:00"  
         },  
         "AccountNumber":"AW73565",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":3  
         }  
      }  
 ]'  
   
SELECT * FROM  
 OPENJSON ( @json )  
WITH (   
              Number   varchar(200) '$.Order.Number' ,  
              Date     datetime     '$.Order.Date',  
              Customer varchar(200) '$.AccountNumber',  
              Quantity int          '$.Item.Quantity'  
 ) 
```  
  
**Resultados**
  
|Número|Data|Cliente|Quantidade|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
Essa função retorna e formata os elementos de uma matriz JSON.  
  
-   Para cada elemento na matriz JSON, **OPENJSON** gera uma nova linha na tabela de saída. Os dois elementos na matriz JSON são convertidos em duas linhas na tabela retornada.  
  
-   Para cada coluna especificada usando a sintaxe `colName type json_path`, **OPENJSON** converte o valor encontrado em cada elemento da matriz do caminho especificado no tipo especificado. Neste exemplo, os valores para a coluna `Date` são tirados de cada elemento no caminho `$.Order.Date` e convertidos em valores de data/hora.  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>Mais informações sobre o OPENJSON com um esquema explícito

Para obter mais informações e exemplos, consulte [Usar OPENJSON com o esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).

Para sintaxe e uso, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).

## <a name="openjson-requires-compatibility-level-130"></a>O OPENJSON requer o nível de compatibilidade 130

A função **OPENJSON** está disponível somente no **nível de compatibilidade 130**. Se o nível de compatibilidade do banco de dados for inferior a 130, o SQL Server não poderá localizar e executar a função **OPENJSON**. Outras funções internas do JSON estão disponíveis em todos os níveis de compatibilidade.

É possível verificar o nível de compatibilidade na exibição `sys.databases` ou nas propriedades do banco de dados.

É possível alterar o nível de compatibilidade de um banco de dados usando o seguinte comando:   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

- [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

- [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

- [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
