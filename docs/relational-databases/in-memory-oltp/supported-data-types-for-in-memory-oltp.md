---
title: "Tipos de Dados com Suporte para o OLTP na Mem&#243;ria | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 26
---
# Tipos de Dados com Suporte para o OLTP na Mem&#243;ria
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este artigo lista os tipos de dados que não têm suporte para os recursos do OLTP na Memória:  
  
-   Tabelas com otimização de memória  
  
-   Procedimentos armazenados e compilados de modo nativo  
  
## Tipos de dados sem-suporte  
 Não há suporte para os seguintes tipos de dados:  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../Topic/geography%20\(Transact-SQL\).md)|[geometry &#40;Transact-SQL&#41;](../Topic/geometry%20\(Transact-SQL\).md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../Topic/hierarchyid%20\(Transact-SQL\).md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|Tipos definidos pelo usuário|.|  
  
## Tipos de Dados com Suporte Importantes  
 A maioria dos tipos de dados é suportada pelos recursos do OLTP na Memória. Vale a pena observar explicitamente o seguinte:  
  
|Tipos de cadeia de caracteres e binários|Para obter mais informações|  
|-----------------------------|--------------------------|  
|binary e varbinary*|[binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char e varchar*|[char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar e nvarchar*|[nchar and nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
Para os tipos de dados da cadeia de caracteres e binários anteriores, começando com o SQL Server 2016:  
  
- Uma tabela individual com otimização de memória também pode ter várias colunas longas, como `nvarchar(4000)`, mesmo que seus tamanhos somem mais do que o tamanho físico da linha com 8.060 bytes.  
  
- Uma tabela com otimização de memória pode ter colunas da cadeia de caracteres e binárias com um tamanho máximo dos tipos de dados, como `varchar(max)`.  


### Identificar LOBs e outras colunas que estão fora de linha

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


#### Suporte para módulos compilados de modo nativo em LOBs


Quando você usa uma função de cadeia de caracteres interna em módulos compilados de modo nativo, como um procedimento nativo, a função pode aceitar um tipo de cadeia de caracteres LOB. Por exemplo, em um procedimento nativo, a função LTrim pode inserir um parâmetro do tipo nvarchar(max) ou varbinary(max).

Esses LOBs podem ser o tipo de retorno de uma UDF (função definida pelo usuário) escalar compilada de modo nativo.


### Outros tipos de dados


|Outros Tipos|Para obter mais informações|  
|-----------------|--------------------------|  
|tipos de tabela|[Variáveis de tabela com otimização de memória](../Topic/Memory-Optimized%20Table%20Variables.md)|  
  
## Consulte também  
 [Suporte ao Transact-SQL para OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementando Colunas LOB em uma tabela com otimização de memória](http://msdn.microsoft.com/pt-br/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [Implementando SQL_VARIANT em uma tabela com otimização de memória](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  