---
title: Solução de problemas dos índices de hash para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: in-memory-oltp
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: caff40911c06bcf57ae1eb39f042de12b8157405
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34331717"
---
# <a name="troubleshooting-hash-indexes-for-memory-optimized-tables"></a>Solução de problemas dos índices de hash para tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="prerequisite"></a>Pré-requisito  
  
Informações de contexto importantes para entender este artigo estão disponíveis em:  
  
- [Índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)
- [Índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index) 
 
## <a name="practical-numbers"></a>Números práticos  
  
Ao criar um índice de hash para uma tabela com otimização de memória, o número de buckets deve ser especificado durante a criação. Na maioria dos casos, o ideal é que a contagem de buckets deve estar entre 1 e 2 vezes o número de valores distintos na chave de índice. 

Entretanto, mesmo que o **BUCKET_COUNT** esteja moderadamente abaixo ou acima do intervalo preferencial, o desempenho do índice de hash provavelmente será tolerável ou aceitável. No mínimo, considere dar ao índice de hash um **BUCKET_COUNT** aproximadamente igual ao número total de linhas previsto para a tabela com otimização de memória.  
Suponha que a tabela em crescimento tenha dois milhões de linhas, com previsão de aumentar dez vezes, chegando a 20 milhões de linhas. Comece com um número de buckets que seja dez vezes o número de linhas na tabela. Assim haverá espaço para uma quantidade maior de linhas.  
  
- O ideal é aumentar a contagem de buckets quando a quantidade de linhas atingir a contagem inicial de buckets.  
- Mesmo que a quantidade de linhas aumente 5 vezes mais do que a contagem de buckets, o desempenho ainda será bom na maioria das situações.  
  
Suponha que um índice de hash tenha dez milhões de valores de chave distintos.  
  
- Um número de buckets igual a dois milhões seria o menor aceitável. O grau de degradação de desempenho seria tolerável.  
  
## <a name="too-many-duplicate-values-in-the-index"></a>Há muitos valores duplicados no índice?  
  
Se os valores de hash indexados tiverem uma alta taxa de duplicados, os buckets de hash terão cadeias mais longas.  
  
Considere a mesma tabela SupportEvent do bloco de código da sintaxe T-SQL anterior. O código T-SQL a seguir demonstra como você pode localizar e exibir a proporção de *todos* os valores para valores *exclusivos* :  
  
```sql
-- Calculate ratio of:  Rows / Unique_Values.  
DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
  
SELECT @allValues = Count(*) FROM SupportEvent;  
  
SELECT @uniqueVals = Count(*) FROM  
  (SELECT DISTINCT SupportEngineerName  
      FROM SupportEvent) as d;  
  
    -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
go  
```
  
- Uma proporção de 10,0 ou superior significa que o hash seria um tipo ruim de índice. Em vez disso, considere o uso de um índice não clusterizado.   
  
## <a name="troubleshooting-hash-index-bucket-count"></a>Solução de problemas de contagem de buckets do índice de hash  
  
Esta seção aborda como solucionar problemas de contagem de buckets do índice de hash.  
  
### <a name="monitor-statistics-for-chains-and-empty-buckets"></a>Monitorar estatísticas de cadeias e buckets vazios  
  
Você pode monitorar a integridade estatística dos índices de hash, executando o T-SQL SELECT a seguir. O SELECT usa a DMV (exibição de gerenciamento de dados) denominada **sys.dm_db_xtp_hash_index_stats**.  
  
```sql
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
  
### <a name="demonstration-of-chains-and-empty-buckets"></a>Demonstração de cadeias e buckets vazios  
  
O seguinte bloco de código T-SQL fornece uma maneira fácil de testar um `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`. O bloco de código é concluído em 1 minuto. Estas estão as fases do seguinte bloco de código:  
  
1. Cria uma tabela com otimização de memória com alguns índices de hash.  
2. Preenche a tabela com milhares de linhas.  
    A. Um operador de módulo é usado para configurar a taxa de valores duplicados na coluna StatusCode.  
    B. O loop insere 262.144 linhas em aproximadamente 1 minuto.  
3. Imprime uma mensagem pedindo para executar o SELECT anterior de **sys.dm_db_xtp_hash_index_stats**.  
  
```sql
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
  
SET NOCOUNT ON;  
  
-- Same as PK bucket_count.  68 seconds to complete.  
DECLARE @i int = 262144;  
  
BEGIN TRANSACTION;  
  
WHILE @i > 0  
BEGIN  
  
  INSERT SalesOrder_Mem  
      (OrderSequence, OrderDate, StatusCode)  
    Values  
      (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
  
  SET @i -= 1;  
END  
COMMIT TRANSACTION;  
  
PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
go  
```  
  
O loop `INSERT` anterior faz o seguinte:  
  
- Insere valores exclusivos para o índice de chave primária e para *ix_OrderSequence*.  
- Insere algumas centenas de milhares de linhas que representam apenas oito valores distintos de `StatusCode`. Portanto, há uma alta taxa de duplicação de valor no índice *ix_StatusCode*.  
  
Para solucionar problemas quando o número de buckets não é ideal, examine a seguinte saída do SELECT de **sys.dm_db_xtp_hash_index_stats**. Para esses resultados, adicionamos `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` à SELECT copiada da seção D.1.  
  
Nossos resultados de `SELECT` são exibidos após o código, artificialmente divididos em duas tabelas de resultados mais estreitos para melhor exibição.  
  
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
  
### <a name="balancing-the-trade-off"></a>Balanceando a compensação  
  
As cargas de trabalho OLTP concentram-se em linhas individuais. Geralmente, as verificações completas de tabelas não estão no caminho crítico de desempenho para cargas de trabalho OLTP. Portanto, a compensação que deve ser balanceada é entre **quantidade de utilização de memória** versus **desempenho de testes de equidade e operações de inserção**.  
  
**Se a utilização de memória for a maior preocupação:**  
  
- Escolha um número de buckets próximo do número de registros da chave de índice.  
- O número de buckets não deve ser significativamente menor do que o número de valores de chave de índice, pois isso afeta a maioria das operações de DML, bem como o tempo necessário para recuperar o banco de dados após a reinicialização do servidor.  
  
**Se o desempenho de testes de igualdade for a maior preocupação:**  
  
- Será apropriado um número de buckets maior, com duas ou três vezes o número de valores de índice exclusivos. Uma contagem maior significa:  
  - Recuperações mais rápidas ao procurar um valor específico.  
  - Um aumento de utilização de memória.  
  - Um aumento do tempo necessário para uma verificação completa do índice de hash.  
  

##  <a name="Additional_Reading"></a> Leitura adicional  
 [Índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [Índices não clusterizados para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)  
