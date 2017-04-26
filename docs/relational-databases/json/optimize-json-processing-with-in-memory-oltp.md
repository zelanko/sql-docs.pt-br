---
title: Otimizar o processamento JSON com o OLTP in-memory | Microsoft Docs
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-vnext
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4e0331c288665fd9f69444d0d14366dfa69a668f
ms.lasthandoff: 04/11/2017

---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>Otimizar o processamento JSON com o OLTP in-memory
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

O SQL Server e o Banco de Dados SQL do Azure permitem que você trabalhe com um texto formatado como JSON. Para aumentar o desempenho das consultas OLTP que processam dados JSON, é possível armazenar documentos JSON em tabelas com otimização de memória usando colunas de cadeia de caracteres padrão (tipo NVARCHAR).

## <a name="store-json-in-memory-optimized-tables"></a>Armazenar JSON em tabelas com otimização de memória
O exemplo a seguir mostra uma tabela do `Product` com otimização de memória, com duas colunas JSON, `Tags` e `Data`:

```tsql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```
Armazenar dados JSON em tabelas com otimização de memória aumenta o desempenho da consulta com o uso do acesso a dados na memória sem bloqueio.

## <a name="optimize-json-with-additional-in-memory-features"></a>Otimizar o JSON com recursos adicionais na memória
Os novos recursos disponíveis no SQL Server e no Banco de Dados SQL do Azure permitem integrar por completo as funcionalidades do JSON às tecnologias existentes do OLTP in-memory. Por exemplo, você pode fazer o seguinte:
 - Validar a estrutura de documentos JSON armazenados em tabelas com otimização de memória usando restrições CHECK compiladas nativamente.
 - Expor e tipar fortemente os valores armazenados em documentos JSON usando colunas computadas.
 - Indexar valores em documentos JSON usando índices com otimização de memória.
 - Compilar consultas SQL nativamente que usam valores de documentos JSON ou formatar os resultados como um texto JSON.

## <a name="validate-json-columns"></a>Validar colunas JSON
O SQL Server e o Banco de Dados SQL do Azure permitem adicionar restrições CHECK compiladas nativamente que validam o conteúdo de documentos JSON armazenados em uma coluna de cadeia de caracteres, conforme mostrado no exemplo a seguir.

```tsql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

A restrição CHECK compilada nativamente pode ser adicionada em tabelas existentes que contêm colunas JSON:

```tsql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

Com as restrições CHECK JSON compiladas nativamente, é possível garantir que o texto JSON armazenado nas tabelas com otimização de memória está formatado corretamente.

## <a name="expose-json-values-using-computed-columns"></a>Expor valores JSON usando colunas computadas
Colunas computadas permitem expor valores do texto JSON e acessar esses valores sem reavaliar as expressões que buscam um valor do texto JSON e sem analisar a estrutura JSON novamente. Os valores expostos são fortemente tipados e fisicamente persistentes nas colunas computadas. O acesso de valores JSON com colunas computadas persistentes é mais rápido do que o acesso de valores no documento JSON.

O seguinte exemplo mostra como expor estes dois valores por meio da coluna JSON `Data`:
-   O país no qual um produto foi fabricado.
-   O custo de fabricação do produto.

```tsql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

As colunas computadas `MadeIn` e `Cost` são atualizadas sempre que o documento JSON armazenado na coluna `Data` é alterado.

## <a name="index-values-in-json-columns"></a>Valores de índice em colunas JSON
O SQL Server e o Banco de Dados SQL do Azure permitem indexar valores em colunas JSON usando índices com otimização de memória. Os valores JSON que são indexados devem ser expostos e fortemente tipados com colunas computadas, conforme mostrado no exemplo a seguir.

```tsql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```
Os valores em colunas JSON podem ser indexados com índices NONCLUSTERED e HASH padrão.
-   Os índices NONCLUSTERED otimizam consultas que selecionam intervalos de linhas por algum valor JSON ou classifica os resultados por valores JSON.
-   Os índices HASH oferecem um desempenho ideal na busca de uma única linha ou de algumas linhas especificando o valor exato a ser encontrado.

## <a name="native-compilation-of-json-queries"></a>Compilação nativa de consultas JSON
Por fim, a compilação nativa de procedimentos, funções e gatilhos Transact-SQL que contêm consultas com funções JSON aumenta o desempenho de consultas e reduz os ciclos de CPU necessários para execução dos procedimentos. O exemplo a seguir mostra um procedimento compilado nativamente que usa várias funções JSON – JSON_VALUE, OPENJSON e JSON_MODIFY.

```tsql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="next-steps"></a>Próximas etapas
O JSON em módulos nativos do OLTP in-memory oferece uma melhoria de desempenho para a funcionalidade interna do JSON disponível no SQL Server e no Banco de Dados SQL do Azure.

Para saber mais sobre os principais cenários para uso do JSON, confira alguns destes recursos:

-   [Blog do TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
-   [Documentação do MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
-   [Vídeo do Channel 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

Para saber mais sobre os vários cenários para integrar o JSON no aplicativo, confira os seguintes recursos:
-   Assista às demonstrações neste [vídeo do Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds).
-   Encontre um cenário que corresponde ao caso de uso em [postagens de blog do JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).
-   Encontre exemplos em nosso [repositório GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/json/).


