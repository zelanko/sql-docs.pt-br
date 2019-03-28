---
title: Determinando o número de buckets correta para índices de Hash | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42fe996b3521316279caf3fcf7adb3e155a83dbd
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536688"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>Determinando o número de buckets correto para índices de hash não clusterizados
  Você deve especificar um valor para o parâmetro `BUCKET_COUNT` quando cria a tabela com otimização de memória. Este tópico faz recomendações para determinar o valor apropriado para o parâmetro `BUCKET_COUNT`. Se você não puder determinar o número de buckets correto, use um índice não clusterizado.  Um valor incorreto de `BUCKET_COUNT`, especialmente muito baixo, pode afetar significativamente o desempenho da carga de trabalho, bem como o tempo de recuperação do banco de dados. É melhor superestimar o número de buckets.  
  
 As chaves de índice duplicadas podem reduzir o desempenho com um índice de hash porque as chaves com hash para o mesmo bucket, fazendo com que a cadeia de bucket aumente.  
  
 Para obter mais informações sobre índices de hash não clusterizados, consulte [Hash Indexes](hash-indexes.md) and [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Uma tabela de hash é alocada para cada índice de hash em uma tabela com otimização de memória. O tamanho da tabela de hash alocada para um índice é especificado o `BUCKET_COUNT` parâmetro no [CREATE TABLE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) ou [CREATE TYPE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql). O número de buckets será arredondado internamente até a próxima potência de dois. Por exemplo, especificar um número de buckets 300.000 resultará em um número real de buckets 524.288.  
  
 Para obter links para um artigo e vídeo sobre contas buckets, consulte [Como determinar a contagem de buckets correta para índices de hash (OLTP na memória)](https://go.microsoft.com/fwlink/p/?LinkId=525853).  
  
## <a name="recommendations"></a>Recomendações  
 Na maioria dos casos, o número de buckets deve estar entre 1 e 2 vezes o número de valores distintos na chave de índice. Se a chave de índice contiver muitos valores duplicados (há, em média, mais de 10 linhas para cada valor de chave de índice), use um índice não clusterizado  
  
 Você não pode sempre prever quantos valores determinada chave de índice tem ou terá. O desempenho deve ser aceitável se o valor `BUCKET_COUNT` é até 5 vezes o número real de valores de chave.  
  
 Para determinar o número de chaves de índice exclusivo nos dados existentes, use consultas semelhantes aos seguintes exemplos:  
  
### <a name="primary-key-and-unique-indexes"></a>Chave primária e índices exclusivos  
 Como o índice de chave primária é exclusivo, o número de valores distintos na chave corresponde ao número de linhas na tabela. Para obter uma chave primária de exemplo em (SalesOrderID, SalesOrderDetailID) na tabela Sales.SalesOrderDetail no banco de dados AdventureWorks, emita a seguinte consulta para calcular o número de valores de chave primária distintos, que corresponde ao número de linhas na tabela:  
  
```sql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 Essa consulta mostra uma contagem de linhas de 121.317. Use um número de buckets de 240.000 caso a contagem de linhas não seja alterada significativamente. Use um número de buckets de 480.000 se esperar que o número de ordens de venda na tabela quadruplique.  
  
### <a name="non-unique-indexes"></a>Índices não exclusivos.  
 Para outros índices, como, por exemplo um índice de várias colunas em (SpecialOfferID, ProductID), emita a seguinte consulta para determinar o número de valores de chaves de índice exclusivo:  
  
```sql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 Esta consulta retorna uma contagem de chaves de índice para (SpecialOfferID, ProductID) de 484, indicando que um índice não clusterizado não deve ser usado em lugar de um índice de hash não clusterizado.  
  
### <a name="determining-the-number-of-duplicates"></a>Determinando o número de duplicatas  
 Para determinar o número médio de valores duplicados para um valor de chave de índice, divida o número total de linhas pelo número de chaves de índice exclusivo.  
  
 Para o índice de exemplo em (SpecialOfferID, ProductID), isso resulta em 121317/484 = 251. Isso significa que valores de chave de índice têm uma média de 251 e, portanto, devem ser um índice não clusterizado.  
  
## <a name="troubleshooting-the-bucket-count"></a>Solucionando problemas no número de buckets  
 Para solucionar problemas de contagem de bucket em tabelas com otimização de memória, use [DM db_xtp_hash_index_stats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql) para obter estatísticas sobre os buckets vazios e o comprimento das cadeias de linha. A consulta a seguir pode ser usada para obter estatísticas sobre todos os índices de hash no banco de dados atual. A consulta poderá levar alguns minutos para ser executada se houver grandes tabelas no banco de dados.  
  
```sql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 Os dois indicadores principais de integridade do índice de hash são:  
  
 *empty_bucket_percent*  
 *empty_bucket_percent* indica o número de buckets vazios no índice de hash.  
  
 Se *empty_bucket_percent* for menor que 10 por cento, é provável que o número de buckets seja muito baixo. O ideal é que *empty_bucket_percent* seja 33 por cento ou mais. Se o número de buckets corresponder ao número de valores de chave de índice, cerca de 1/3 dos bucket ficarão vazios, devido à distribuição de hash.  
  
 *avg_chain_length*  
 *avg_chain_length* indica o comprimento médio das cadeias de linha nos buckets de hash.  
  
 Se *avg_chain_length* é maior que 10 e *empty_bucket_percent* é maior que 10 por cento, provavelmente há muitos valores de chave de índice duplicados e um índice não clusterizado seria mais apropriado. Um comprimento médio ideal de cadeia é 1.  
  
 Há dois fatores que afetam o comprimento de cadeia:  
  
1.  Duplicatas; todas as linhas duplicadas são parte da mesma cadeia no índice de hash.  
  
2.  Vários valores de chave são mapeados para o mesmo bucket. Quanto menor o número de buckets, mais buckets terão diversos valores mapeados para eles.  
  
 Como exemplo, considere a seguinte tabela e script para inserir linhas de exemplo na tabela:  
  
```sql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 O script insere 262.144 linhas na tabela. Ele insere valores exclusivos no índice de chave primária e em IX_OrderSequence. Ele insere muitos valores duplicados no índice IX_Status: o script gera apenas 8 valores distintos.  
  
 A saída da consulta de solução de problemas BUCKET_COUNT é a seguinte:  
  
|nome do índice|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 Considere os três índices de hash nesta tabela:  
  
-   IX_Status: 50 por cento dos buckets estão vazios, o que é bom. Porém, o comprimento médio da cadeia é muito alto (65.536). Isso indica um grande número de valores duplicados. Portanto, usar um índice de hash não clusterizado não é apropriado nesse caso. Deve-se utilizar índice não clusterizado.  
  
-   IX_OrderSequence: 0 por cento dos buckets estão vazios, um valor muito baixo. Além disso, o comprimento médio de cadeia é 8. Como os valores nesse índice são exclusivos, isso significa que, em média, 8 valores são mapeados para cada bucket. O número de buckets deve ser aumentado. Como a chave de índice tem 262.144 valores exclusivos, o número de buckets deve ser pelo menos 262.144. Se é esperado um futuro crescimento, o número deve ser mais alto.  
  
-   Índice de chave primária (... PK uma de SalesOrder): 36 por cento dos buckets estão vazios, o que é bom. Além disso, o comprimento médio da cadeia é 1, o que também é bom. Nenhuma alteração necessária.  
  
 Para obter mais informações sobre como solucionar problemas nos índices de hash com otimização de memória, consulte [Troubleshooting Common Performance Problems with Memory-Optimized Hash Indexes](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md).  
  
## <a name="detailed-considerations-for-further-optimization"></a>Considerações detalhadas para a otimização adicional  
 Esta seção descreve considerações adicionais para otimizar o número de buckets.  
  
 Para obter o melhor desempenho de índices de hash, equilibre a quantidade de memória alocada para a tabela de hash e o número de valores distintos na chave de índice. Também há um equilíbrio entre o desempenho de pesquisas de ponto e as verificações de tabela:  
  
-   Quanto mais alto o valor do número de buckets, mais buckets vazios existirão no índice. Isso tem um impacto no uso da memória (8 bytes por bucket) e no desempenho de verificações de tabela, pois cada bucket é verificado como parte de uma verificação de tabela.  
  
-   Quanto menor o número de buckets, mais valores serão atribuídos a um único bucket. Isso reduz o desempenho para pesquisas e inserções de ponto, pois o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode precisar atravessar vários valores em um único bucket para localizar o valor especificado pelo predicado de pesquisa.  
  
 Se o número de buckets é significativamente menor que o número de chaves de índice exclusivo, muitos valores serão mapeadas para cada bucket. Isso afeta o desempenho da maioria das operações de DML, especialmente pesquisas de ponto (pesquisas de chaves de índice individuais) e de operações de inserção. Por exemplo, você pode ver o desempenho baixo de consultas SELECT, e das operações UPDATE e DELETE com predicados de igualdade, que correspondem às colunas de chave do índice na cláusula WHERE. Um baixo número de buckets também afeta o tempo de recuperação do banco de dados, pois os índices são recriados na inicialização do banco de dados.  
  
### <a name="duplicate-index-key-values"></a>Valores de chave de índice duplicados  
 Os valores duplicados podem aumentar o impacto do desempenho de colisões de hash. Em geral, não há problema se cada chave de índice tem um número baixo de duplicatas. Mas, isso poderá ser um problema se a discrepância entre o número de chaves de índice exclusivo e o número de linhas nas tabelas for muito grande.  
  
 Todas as linhas com a mesma chave de índice constarão na mesma cadeia duplicada. Se várias chaves de índice estiverem no mesmo bucket devido a uma colisão de hash, o verificador de índice sempre precisará verificar a cadeia duplicada completa para ver o primeiro valor antes de localizar a primeira linha que corresponde ao segundo valor. As chaves duplicadas também dificultam a localização da linha por parte da coleta de lixo. Por exemplo, se houver 1.000 duplicatas para qualquer chave e uma das linhas for excluída, o coletor de lixo precisará examinar a cadeia de 1.000 duplicatas para desvincular a linha do índice. Isso será verdadeiro mesmo se a consulta que localizou a exclusão tiver usado um índice mais eficaz (um índice de chave primária) para localizar a linha, porque o coletor de lixo precisa desvincular de cada índice  
  
 Para índices de hash, há duas maneiras de reduzir o trabalho causado por valores de chave de índice duplicados:  
  
-   Usar um índice não clusterizado. Você pode diminuir as duplicadas adicionando colunas à chave de índice sem exigir nenhuma alteração ao aplicativo.  
  
-   Especificar uma número de buckets alto demais para o índice. Por exemplo, 20 a 100 vezes o número de chaves de índice exclusivo. Isso reduzirá as colisões de hash.  
  
### <a name="small-tables"></a>Tabelas pequenas  
 Para tabelas menores, a utilização da memória não costuma ser uma preocupação, pois o tamanho do índice será pequeno comparado ao tamanho geral do banco de dados.  
  
 Você deve fazer uma escolha com base no tipo de desempenho desejado:  
  
-   Se as operações essenciais para o desempenho no índice forem predominantemente pesquisas de ponto e/ou operações de inserção, um número de buckets mais alto será apropriado para reduzir a probabilidade de colisões de hash. A melhor opção é ter três vezes o número de linhas ou até mesmo mais.  
  
-   Se as verificações de índice completo forem as operações essenciais para o desempenho predominantes, use um número de buckets próximo ao número real de valores de chave de índice.  
  
### <a name="big-tables"></a>Tabelas grandes  
 Para tabelas grandes, a utilização de memória pode se tornar um problema. Por exemplo, com uma tabela de 250 milhões de linhas que tem 4 índices de hash, cada um com uma contagem de bucket de um bilhão, a sobrecarga das tabelas de hash é de 4 índices * 1 bilhão de buckets \* 8 bytes = 32 gigabytes de utilização de memória. Ao escolher um número de buckets equivalente a 250 milhões para cada um dos índices, a sobrecarga total das tabelas de hash será de 8 gigabytes. Observe que isso está além do uso de memória de 8 bytes cada índice adiciona a cada linha individual, que é 8 gigabytes neste cenário (4 índices \* 8 bytes \* 250 milhões de linhas).  
  
 As verificações completas de tabelas em geral não estão no caminho essencial para o desempenho para cargas de trabalho do OLTP. Consequentemente, a escolha é entre a utilização de memória versus o desempenho da pesquisa de ponto e as operações de inserção:  
  
-   Caso a utilização de memória seja uma preocupação, escolha um número de buckets próximo ao número de valores de chave de índice. O número de buckets não deve ser significativamente menor do que o número de valores de chave de índice, pois isso afeta a maioria das operações de DML, bem como o tempo necessário para recuperar o banco de dados após a reinicialização do servidor.  
  
-   Ao otimizar o desempenho para pesquisas de ponto, um número de buckets duas ou três vezes maior do que o número de valores de índice exclusivo seria apropriado. Um número maior de buckets significaria uma maior utilização de memória e a necessidade de mais tempo para realizar uma verificação de índice completo.  
  
## <a name="see-also"></a>Consulte também  
 [Índices em tabelas com otimização de memória](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
