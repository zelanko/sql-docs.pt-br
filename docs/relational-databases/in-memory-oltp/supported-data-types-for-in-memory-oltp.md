---
title: Tipos de dados com suporte para o OLTP in-memory | Microsoft Docs
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a928c1f77586198fd0d33cafa445ea406a437c6b
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="supported-data-types-for-in-memory-oltp"></a>Tipos de Dados com Suporte para o OLTP na Memória
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este artigo lista os tipos de dados que não têm suporte para os recursos do OLTP na Memória:  
  
-   Tabelas com otimização de memória  
  
-   Procedimentos armazenados e compilados de modo nativo  
  
## <a name="unsupported-data-types"></a>Tipos de dados sem-suporte  
 Não há suporte para os seguintes tipos de dados:  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry &#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|Tipos definidos pelo usuário|.|  
  
## <a name="notable-supported-data-types"></a>Tipos de Dados com Suporte Importantes  
 A maioria dos tipos de dados é suportada pelos recursos do OLTP na Memória. Vale a pena observar explicitamente o seguinte:  
  
|Tipos de cadeia de caracteres e binários|Para obter mais informações|  
|-----------------------------|--------------------------|  
|binary e varbinary*|[binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char e varchar*|[char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar e nvarchar*|[nchar and nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
Para os tipos de dados da cadeia de caracteres e binários anteriores, começando com o SQL Server 2016:  
  
- Uma tabela individual com otimização de memória também pode ter várias colunas longas, como `nvarchar(4000)`, mesmo que seus tamanhos somem mais do que o tamanho físico da linha com 8.060 bytes.  
  
- Uma tabela com otimização de memória pode ter colunas da cadeia de caracteres e binárias com um tamanho máximo dos tipos de dados, como `varchar(max)`.  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>Identificar LOBs e outras colunas que estão fora de linha

A instrução SELECT do Transact-SQL a seguir relata todas as colunas que estão fora de linha em tabelas com otimização de memória. Observe que:

- Todas as colunas de chave de índice são armazenadas em linha.
  - Chaves de índice não exclusivas agora podem incluir colunas que permitem valor nulo, em tabelas com otimização de memória.
  - Índices podem ser declarados como UNIQUE em uma tabela com otimização de memória.
- Todas as colunas LOB são armazenadas fora de linha.
- Um max_length de -1 indica uma coluna LOB (objeto grande).


```tsql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


#### <a name="natively-compiled-modules-support-for-lobs"></a>Suporte para módulos compilados de modo nativo em LOBs


Quando você usa uma função de cadeia de caracteres interna em módulos compilados de modo nativo, como um procedimento nativo, a função pode aceitar um tipo de cadeia de caracteres LOB. Por exemplo, em um procedimento nativo, a função LTrim pode inserir um parâmetro do tipo nvarchar(max) ou varbinary(max).

Esses LOBs podem ser o tipo de retorno de uma UDF (função definida pelo usuário) escalar compilada de modo nativo.


### <a name="other-data-types"></a>Outros tipos de dados


|Outros Tipos|Para obter mais informações|  
|-----------------|--------------------------|  
|tipos de tabela|[Variáveis de tabela com otimização de memória](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao Transact-SQL para OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementando Colunas LOB em uma tabela com otimização de memória](http://msdn.microsoft.com/en-us/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [Implementando SQL_VARIANT em uma tabela com otimização de memória](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  

