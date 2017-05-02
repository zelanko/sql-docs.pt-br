---
title: "Índices de hash para tabelas com otimização de memória | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de23d5625c883792f5c99de75dc90ccd1cabe326
ms.lasthandoff: 04/11/2017

---
# <a name="hash-indexes-for-memory-optimized-tables"></a>Índices de hash para tabelas com otimização de memória
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
Este artigo descreve o tipo de índice de *hash* disponível para uma tabela com otimização de memória. O artigo:  
  
- Fornece exemplos de códigos curtos para demonstrar a sintaxe Transact-SQL.  
- Descreve os conceitos básicos de índices de hash.  
- Descreve [como estimar uma contagem de buckets apropriada](#configuring_bucket_count).  
- Descreve como criar e gerenciar índices de hash.  
  
  
#### <a name="prerequisite"></a>Pré-requisito  
  
Informações de contexto importantes para entender este artigo estão disponíveis em:  
  
- [Índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. Sintaxe para índices com otimização de memória  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 Exemplo de código de sintaxe  
  
Esta subseção contém um bloco de códigos Transact-SQL que demonstra as sintaxes disponíveis para criar um índice hash em uma tabela com otimização de memória:  
  
- A amostra indica que o índice de hash é declarado dentro da instrução CREATE TABLE.  
  - Em vez disso, você pode declarar o índice de hash em uma instrução [ALTER TABLE...ADD INDEX](#h3-b2-declaration-limitations) separada.  
  
  
  
    DROP TABLE IF EXISTS SupportEventHash;  
    go  
      
    CREATE TABLE SupportIncidentRating_Hash  
    (  
      SupportIncidentRatingId   int      not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
      
      RatingLevel          int           not null,  
      
      SupportEngineerName  nvarchar(16)  not null,  
      Description          nvarchar(64)      null,  
      
      INDEX ix_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 100000)  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_ONLY);  
    go  
  

Para determinar a `BUCKET_COUNT` certa para seus dados, consulte [Configurando a contagem de buckets do índice de hash](#configuring_bucket_count). 
  
## <a name="b-hash-indexes"></a>B. Índices de hash  
  
  
### <a name="b1-performance-basics"></a>B.1 Noções básicas de desempenho  
  
O desempenho de um índice de hash é:  
  
- Excelente quando a cláusula WHERE especifica um valor *exato* para cada coluna na chave de índice de hash.  
- Fraco quando a cláusula WHERE procura um *intervalo* de valores na chave de índice.  
- Fraco quando a cláusula WHERE define um valor específico para a primeira coluna de uma chave de índice de hash de duas colunas, mas não define um valor para a *segunda* coluna da chave.  
  
  
<a name="h3-b2-declaration-limitations"></a>  
  
### <a name="b2-declaration-limitations"></a>B.2 Limitações de declaração  
  
Um índice de hash apenas pode existir em uma tabela com otimização de memória. Ele não pode existir em uma tabela baseada em disco.  
  
Um índice de hash pode ser declarado como:  
  
- UNIQUE ou pode usar Nonunique como padrão.  
- NONCLUSTERED, que é o padrão.   
  
  
Este é um exemplo da sintaxe para criar um índice de hash fora da instrução CREATE TABLE:  
  
  
    ALTER TABLE MyTable_memop  
      ADD INDEX ix_hash_Column2 UNIQUE  
        HASH (Column2) WITH (BUCKET_COUNT = 64);  
  
  
  
### <a name="b3-buckets-and-hash-function"></a>B.3 Buckets e a função de hash  
  
Um índice de hash ancora seus valores de chave em uma matriz de *bucket* :  
  
- Cada bucket tem 8 bytes, que são usados para armazenar o endereço de memória de uma lista de links de entradas de chave.  
- Cada entrada é um valor de uma chave de índice, mais o endereço de sua linha correspondente na tabela com otimização de memória subjacente.  
  - Cada um dos pontos de entrada para a próxima entrada em uma lista de links de entradas, todos encadeados no bucket atual.  
  
  
O algoritmo de hash tenta distribuir todos os valores de chave exclusivos ou distintos de maneira uniforme entre seus buckets, mas a uniformidade total é um ideal inalcançado. Todas as instâncias de determinado valor de chave são encadeadas no mesmo bucket. O bucket também poderá combinado todas as instâncias de um valor de chave diferente.  
  
- Essa combinação é chamada uma *colisão de hash*. Colisões são comuns, mas não são ideais.  
- Uma meta realista é que 30% dos buckets contenham dois valores de chave diferentes.  
  
  
Declare quantos buckets um índice de hash deverá ter.  
  
- Quanto menor a proporção de buckets para linhas ou valores distintos, maior será a lista média de links de bucket.  
- Listas de links curtas executam com mais rapidez do que listas de links longas.  
  
  
O SQL Server tem uma única função de hash usada para todos os índices de hash:  
  
- A função de hash é determinística: dado o mesmo valor de chave de entrada, ela emite consistentemente o mesmo slot de bucket.  
- Com chamadas repetidas, as saídas da função de hash tendem a formar uma distribuição de Poisson ou em curva de sino, não uma distribuição linear simples.  
  
  
A interação entre o índice de hash e os buckets é resumida na imagem a seguir.  
  
  
![hekaton_tables_23d](../../relational-databases/in-memory-oltp/media/hekaton-tables-23d.png "Chaves de índice, inseridos na função de hash, a saída é o endereço de um bucket de hash, que aponta para o início da cadeia.")  
  
  
  
### <a name="b4-row-versions-and-garbage-collection"></a>B.4 Versões de linha e coleta de lixo  
  
  
Em uma tabela com otimização de memória, quando uma linha é afetada por um SQL UPDATE, a tabela cria uma versão atualizada da linha. Durante a transação de atualização, é possível que outras sessões consigam ler a versão mais antiga da linha, evitando a lentidão de desempenho associada a um bloqueio de linha.  
  
O índice de hash também pode ter versões diferentes de suas entradas para acomodar a atualização.  
  
Posteriormente, quando as versões mais antigas não forem mais necessárias, um thread de GC (coleta de lixo) percorrerá os buckets e suas listas de links para limpar as entradas antigas. A execução do thread da GC é melhor se os tamanhos de cadeia de lista de link são curtos.   
  
<a name="configuring_bucket_count"></a>
  
## <a name="c-configuring-the-hash-index-bucket-count"></a>C. Configurando a contagem de buckets do índice de hash  
  
A contagem de bucket do índice de hash é especificada no momento de criação do índice e pode ser alterada com a sintaxe ALTER TABLE...ALTER INDEX REBUILD.  
  
Na maioria dos casos, o ideal é que a contagem de buckets deve estar entre 1 e 2 vezes o número de valores distintos na chave de índice.   
Você não pode sempre prever quantos valores determinada chave de índice tem ou terá. Em geral, o desempenho ainda será bom se o valor de **BUCKET_COUNT** estiver dentro de 10 vezes o número real de valores de chave, e valores superestimados são geralmente melhores que os subestimados.  
  
Um *número muito pequeno* de buckets tem as seguintes desvantagens:  
  
- Mais colisões de hash de valores de chave distintos.  
  - Cada valor distinto é forçado a compartilhar o mesmo bucket com um valor distinto diferente.  
  - O comprimento médio de cadeia por bucket aumenta.  
  - Quanto maior é a cadeia de bucket, mais lentas são as pesquisas de igualdade no índice e.  
  
Um *número muito grande* de buckets tem as seguintes desvantagens:  
  
- Um número de buckets muito alto pode resultar em mais buckets vazios.  
  - Buckets vazios afetam o desempenho de verificações de índice completas. Se elas forem executadas regularmente, considere escolher uma contagem de buckets próximo ao número de valores de chave de índice distintos.  
  - Buckets vazios usam a memória, embora cada bucket use apenas 8 bytes.  
    
  
> [!NOTE]
> A adição de mais buckets não contribui para reduzir o encadeamento de entradas que compartilham um valor duplicado. A taxa de duplicação de valor é usada para decidir se um hash é o tipo de índice apropriado, não para calcular o número de buckets.  
  
  
  
### <a name="c1-practical-numbers"></a>C.1 Números práticos  
  
Mesmo que o **BUCKET_COUNT** esteja moderadamente abaixo ou acima do intervalo preferencial, o desempenho do índice de hash provavelmente será tolerável ou aceitável. Nenhuma crise é criada.  
  
Dê ao índice de hash um **BUCKET_COUNT** aproximadamente igual ao número de linhas previsto para o crescimento da tabela com otimização de memória.  
  
Suponha que a tabela em crescimento tenha dois milhões de linhas, com previsão de que a quantidade aumente dez vezes, chegando a 20 milhões de linhas. Comece com um número de buckets que seja dez vezes o número de linhas na tabela. Assim haverá espaço para uma quantidade maior de linhas.  
  
- O ideal é aumentar a contagem de buckets quando a quantidade de linhas atingir a contagem inicial de buckets.  
- Mesmo que a quantidade de linhas aumente 5 vezes mais do que a contagem de buckets, o desempenho ainda será bom na maioria das situações.  
  
Suponha que um índice de hash tenha dez milhões de valores de chave distintos.  
  
- Um número de buckets igual a dois milhões seria o menor aceitável. O grau de degradação de desempenho seria tolerável.  
  
### <a name="c2-too-many-duplicate-values-in-the-index"></a>C.2 Há muitos valores duplicados no índice?  
  
Se os valores de hash indexados tiverem uma alta taxa de duplicados, os buckets de hash terão cadeias mais longas.  
  
Considere a mesma tabela SupportEvent do bloco de código da sintaxe T-SQL anterior. O código T-SQL a seguir demonstra como você pode localizar e exibir a proporção de *todos* os valores para valores *exclusivos* :  
  
        -- Calculate ratio of:  Rows / Unique_Values.  
    DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
      
    SELECT @allValues = Count(*) FROM SupportEvent;  
      
    SELECT @uniqueVals = Count(*) FROM  
      (SELECT DISTINCT SupportEngineerName  
         FROM SupportEvent) as d;  
      
        -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
    SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
    go  
  
- Uma proporção de 10,0 ou superior significa que o hash seria um tipo ruim de índice. Em vez disso, considere o uso de um índice não clusterizado.   
  
## <a name="d-troubleshooting-hash-index-bucket-count"></a>D. Solução de problemas de contagem de buckets do índice de hash  
  
Esta seção aborda como solucionar problemas de contagem de buckets do índice de hash.  
  
### <a name="d1-monitor-statistics-for-chains-and-empty-buckets"></a>D.1 Monitorar estatísticas de cadeias e buckets vazios  
  
Você pode monitorar a integridade estatística dos índices de hash, executando o T-SQL SELECT a seguir. O SELECT usa a DMV (exibição de gerenciamento de dados) denominada **sys.dm_db_xtp_hash_index_stats**.  
  
  
```t-sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
      
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM  
         sys.dm_db_xtp_hash_index_stats  as h   
    JOIN sys.indexes                     as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
```
  
  
Compare os resultados do SELECT com as seguintes recomendações estatísticas:  
  
- Buckets vazios:  
  - 33% é um bom valor de destino, mas geralmente um percentual maior é satisfatório (até 90%).  
  - Quando o número de buckets é igual ao número de valores de chave distintos, aproximadamente 33% dos buckets estão vazios.  
  - Um valor inferior a 10% é muito baixo.  
- Cadeias dentro de buckets:  
  - Um tamanho de cadeia médio de 1 será ideal caso não haja valores de chave de índice duplicados. Em geral, tamanhos de cadeia de até 10 são aceitáveis.  
  - Quando o comprimento médio da cadeia é maior que dez e o percentual de buckets vazios é maior que 10%, os dados têm tantos duplicados que o índice de hash pode não ser o tipo mais apropriado.  
  

  
### <a name="d2-demonstration-of-chains-and-empty-buckets"></a>D.2 Demonstração de cadeias e buckets vazios  
  
  
O seguinte bloco de código T-SQL fornece uma maneira fácil de testar um `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`. O bloco de código é concluído em 1 minuto. Estas estão as fases do seguinte bloco de código:  
  
  
1. Cria uma tabela com otimização de memória com alguns índices de hash.  
2. Preenche a tabela com milhares de linhas.  
    A. Um operador de módulo é usado para configurar a taxa de valores duplicados na coluna StatusCode.  
    B. O loop insere 262.144 linhas em aproximadamente 1 minuto.  
3. Imprime uma mensagem pedindo para executar o SELECT anterior de **sys.dm_db_xtp_hash_index_stats**.  
  
  
```t-sql
    DROP TABLE IF EXISTS SalesOrder_Mem;  
    go  
      
      
    CREATE TABLE SalesOrder_Mem  
    (  
      SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
      OrderSequence  int               NOT NULL,  
      OrderDate      datetime2(3)      NOT NULL,  
      StatusCode     tinyint           NOT NULL,  
      
      PRIMARY KEY NONCLUSTERED  
          HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
      
      INDEX ix_OrderSequence  
          HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
      
      INDEX ix_StatusCode  
          HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
      
      INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
    )  
      WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    go  
      
        --------------------  
      
    SET NoCount ON;  
      
      -- Same as PK bucket_count.  68 seconds to complete.  
    DECLARE @i int = 262144;  
      
    BEGIN TRANSACTION;  
      
    WHILE @i > 0  
    Begin  
      
      INSERT SalesOrder_Mem  
          (OrderSequence, OrderDate, StatusCode)  
        Values  
          (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
      
      SET @i -= 1;  
    End  
    COMMIT TRANSACTION;  
      
    PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
    go  
```  
  
  
O loop INSERT anterior faz o seguinte:  
  
- Insere valores exclusivos para o índice de chave primária e para ix_OrderSequence.  
- Insere duas centenas de milhares de linhas que representam apenas oito valores distintos de StatusCode. Portanto, há uma alta taxa de duplicação de valor no índice ix_StatusCode.  
  
Para solucionar problemas quando o número de buckets não é ideal, examine a seguinte saída do SELECT de **sys.dm_db_xtp_hash_index_stats**. Para esses resultados, adicionamos `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` à SELECT copiada da seção D.1.  
  
  
  
Nossos resultados de SELECT são exibidos após o código, artificialmente divididos em duas tabelas de resultados mais estreitos para melhor exibição.  
  
- Estes são os resultados da *contagem de buckets*.  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
  
- Veja a seguir os resultados do *tamanho da cadeia*.  
  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
  
  
  
Vamos interpretar os três índices de hash das tabelas de resultados anteriores:  
  
*ix_StatusCode:*  
  
- 50% dos buckets estão vazios, o que é bom.  
- Porém, o comprimento médio da cadeia é muito alto (65536).  
  - Isso indica uma alta taxa de valores duplicados.  
  - Portanto, usar um índice de hash não é apropriado nesse caso. Deve-se utilizar índice não clusterizado.  
  
*ix_OrderSequence:*  
  
- 0% dos buckets estão vazios, o que é muito baixo.  
- O comprimento médio da cadeia é 8, embora todos os valores nesse índice sejam exclusivos.  
  - Portanto, o número de buckets deve ser aumentado para reduzir o comprimento médio da cadeia, aproximando-o de 2 ou 3.  
- Como a chave de índice tem 262144 valores exclusivos, o número de buckets deve ser pelo menos 262144.  
  - Caso seja esperado um futuro crescimento, o número de buckets deverá ser mais alto.  
  
*Índice de chave primária (PK_SalesOrd_...):*  
  
- 36% dos buckets estão vazios, o que é bom.  
- O comprimento médio da cadeia é 1, o que também é bom. Nenhuma alteração é necessária.  
  
  
### <a name="d3-balancing-the-trade-off"></a>D.3 Balanceando a compensação  
  
As cargas de trabalho OLTP concentram-se em linhas individuais. Geralmente, as verificações completas de tabelas não estão no caminho crítico de desempenho para cargas de trabalho OLTP. Portanto, a compensação que você deve balancear é entre:  
  
- A quantidade de utilização de memória com relação ao  
- Desempenho de testes de igualdade e de operações de inserção.  
  
  
*Se a utilização de memória for a maior preocupação:*  
  
- Escolha um número de buckets próximo do número de registros da chave de índice.  
- O número de buckets não deve ser significativamente menor do que o número de valores de chave de índice, pois isso afeta a maioria das operações de DML, bem como o tempo necessário para recuperar o banco de dados após a reinicialização do servidor.  
  
  
*Se o desempenho de testes de igualdade for a maior preocupação:*  
  
- Será apropriado um número de buckets maior, com duas ou três vezes o número de valores de índice exclusivos. Uma contagem maior significa:  
  - Recuperações mais rápidas ao procurar um valor específico.  
  - Um aumento de utilização de memória.  
  - Um aumento do tempo necessário para uma verificação completa do índice de hash.  
  
  
  
  
## <a name="e-strengths-of-hash-indexes"></a>E. Pontos fortes dos índices de hash  
  
  
Um índice de hash é preferível em vez de um índice não clusterizado quando:  
  
- As consultas testam a coluna indexada usando uma cláusula WHERE com uma igualdade, como a seguir:  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="e1-multi-column-hash-index-keys"></a>E.1 Chaves de índice de hash com várias colunas  
  
  
O índice de duas colunas pode ser um índice não clusterizado ou um índice de hash. Suponha que as colunas de índice sejam col1 e col2. Devido à seguinte instrução SQL SELECT, apenas o índice não clusterizado será útil para o otimizador de consulta:  
  
  
    SELECT col1, col3  
        FROM MyTable_memop  
        WHERE col1 = 'dn';  
  
  
O índice de hash precisa da cláusula WHERE para especificar um teste de igualdade para cada uma das colunas de sua chave. Caso contrário, o índice de hash não será útil para o otimizador.  
  
Nenhum tipo de índice é útil se a cláusula WHERE especifica somente a segunda coluna na chave de índice.  
  
  
  
\<!--   
Hash_Indexes_for_Memory-Optimized_Tables.md, que é....  
Guid de CAPS: {e922cc3a-3d6e-453b-8d32-f4b176e98488}  
O guid de CAPS do pai é: {eecc5821-152b-4ed5-888f-7c0e6beffed9}  
  
  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent | avg_chain_length | max_chain_length |  
| :-------- | -----------------: | -----------------: | -----------------: | ---------------: | ---------------: |  
| ix_OrderSequence | 32768 | 13 | 0 | 8 | 26 |  
| ix_StatusCode | 8 | 4 | 50 | 65536 | 65536 |  
| PK_SalesOrd_B14003E308C1A23C | 262144 | 96525 | 36 | 1 | 8 |  
  
  
  
  
GeneMi, quinta-feira, 05/05/2016, 15h01  
-->  
  
  
  


