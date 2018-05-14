---
title: Otimizar o processamento JSON com o OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b969dac20c3869deb74d70e530d5b97e5fcc30dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>Otimizar o processamento JSON com o OLTP in-memory
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O SQL Server e o Banco de Dados SQL do Azure permitem que você trabalhe com um texto formatado como JSON. Para aumentar o desempenho de consultas que processam dados JSON, é possível armazenar documentos JSON em tabelas com otimização de memória usando colunas de cadeia de caracteres padrão (tipo NVARCHAR). Armazenar dados JSON em tabelas com otimização de memória aumenta o desempenho da consulta com o uso do acesso a dados na memória sem bloqueio.

## <a name="store-json-in-memory-optimized-tables"></a>Armazenar JSON em tabelas com otimização de memória
O exemplo a seguir mostra uma tabela do `Product` com otimização de memória, com duas colunas JSON, `Tags` e `Data`:

```sql
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

## <a name="optimize-json-processing-with-additional-in-memory-features"></a>Otimizar o processamento JSON com recursos adicionais na memória
Os recursos disponíveis no SQL Server e no Banco de Dados SQL do Azure permitem integrar por completo as funcionalidades do JSON às tecnologias existentes do OLTP in-memory. Por exemplo, você pode fazer o seguinte:
 - [Validar a estrutura de documentos JSON](#validate) armazenados em tabelas com otimização de memória usando restrições CHECK compiladas nativamente.
 - [Expor e tipar fortemente os valores](#computedcol) armazenados em documentos JSON usando colunas computadas.
 - [Indexar valores](#index) em documentos JSON usando índices com otimização de memória.
 - [Compilar nativamente consultas SQL](#compile) que usam valores de documentos JSON ou formatar os resultados como um texto JSON.

## <a name="validate"></a> Validar colunas JSON
O SQL Server e o Banco de Dados SQL do Azure permitem adicionar restrições CHECK compiladas nativamente que validam o conteúdo de documentos JSON armazenados em uma coluna de cadeia de caracteres. Com as restrições CHECK JSON compiladas nativamente, é possível garantir que o texto JSON armazenado nas tabelas com otimização de memória está formatado corretamente.

O exemplo a seguir cria uma tabela `Product` com uma coluna JSON `Tags`. A coluna `Tags` tem uma restrição CHECK que utiliza a função `ISJSON` para validar o texto JSON na coluna.

```sql
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

Também é possível adicionar a restrição CHECK compilada nativamente a tabelas existentes que contêm colunas JSON.

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

## <a name="computedcol"></a> Expor valores JSON usando colunas computadas
Colunas computadas permitem expor valores do texto JSON e acessar esses valores sem buscar o valor do texto JSON e sem analisar a estrutura JSON novamente. Os valores expostos dessa maneira são fortemente tipados e fisicamente persistentes nas colunas computadas. O acesso a valores JSON com colunas computadas persistentes é mais rápido do que o acesso a valores diretamente no documento JSON.

O seguinte exemplo mostra como expor estes dois valores por meio da coluna JSON `Data`:
-   O país no qual um produto foi fabricado.
-   O custo de fabricação do produto.

Neste exemplo, as colunas computadas `MadeIn` e `Cost` são atualizadas sempre que o documento JSON armazenado na coluna `Data` é alterado.

```sql
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

## <a name="index"></a> Valores de índice em colunas JSON
O SQL Server e o Banco de Dados SQL do Azure permitem indexar valores em colunas JSON usando índices com otimização de memória. Os valores JSON indexados devem ser expostos e fortemente tipados com colunas computadas, conforme mostrado no exemplo anterior.

Os valores em colunas JSON podem ser indexados com índices NONCLUSTERED e HASH padrão.
-   Os índices NONCLUSTERED otimizam consultas que selecionam intervalos de linhas por algum valor JSON ou classifica os resultados por valores JSON.
-   Os índices HASH otimizam consultas que selecionam uma única linha ou algumas linhas especificando um valor exato a ser encontrado.

O exemplo a seguir cria uma tabela que expõe valores JSON com duas colunas computadas. O exemplo cria um índice NONCLUSTERED em um valor JSON e um índice HASH no outro.

```sql
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

## <a name="compile"></a> Compilação nativa de consultas JSON
Se os procedimentos, funções e gatilhos contêm consultas que usam funções JSON internas, a compilação nativa aumentará o desempenho dessas consultas e reduzirá os ciclos de CPU necessários para executá-los.

O exemplo a seguir mostra um procedimento compilado nativamente que usa várias funções JSON – **JSON_VALUE**, **OPENJSON** e **JSON_MODIFY**.

```sql
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-blog-posts"></a>Postagens no blog da Microsoft  
  
Para ver soluções específicas, casos de uso e recomendações, consulte as [postagens no blog](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre o suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure.  

### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
