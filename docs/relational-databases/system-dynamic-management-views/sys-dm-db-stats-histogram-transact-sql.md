---
title: sys.dm_db_stats_histogram (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sys.dm_db_stats_histogram
- sys.dm_db_stats_histogram_TSQL
- dm_db_stats_histogram
- dm_db_stats_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_histogram dynamic management function
ms.assetid: 1897fd4a-8d51-461e-8ef2-c60be9e563f2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0e6fc1d921c5941492d99fd9eb733f910ac24b4c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbstatshistogram-transact-sql"></a>sys.dm_db_stats_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Retorna o histograma de estatísticas para o objeto de banco de dados especificado (tabela ou exibição indexada) no atual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Semelhante ao `DBCC SHOW_STATISTICS WITH HISTOGRAM`.

> [!NOTE] 
> Essa DMF está disponível desde [!INCLUDE[ssSQL15](../../includes/ssSQL15-md.md)] SP1 CU2

## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_db_stats_histogram (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É a ID do objeto no banco de dados atual para o qual as propriedades de uma de suas estatísticas é solicitada. *object_id* é **int**.  
  
 *stats_id*  
 É a ID de estatísticas do *object_id*especificado. A ID de estatísticas pode ser obtida na exibição de gerenciamento dinâmico [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) . *stats_id* é **int**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id |**Int**|ID do objeto (tabela ou exibição indexada) para o qual as propriedades do objeto de estatísticas serão retornadas.|  
|stats_id |**Int**|ID do objeto de estatísticas. É exclusiva na tabela ou exibição indexada. Para obter mais informações, veja [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|  
|step_number |**Int** |O número da etapa do histograma. |
|range_high_key |**sql_variant** |Valor da coluna associada superior de uma etapa do histograma. O valor da coluna também será denominado um valor de chave.|
|range_rows |**real** |Número estimado de linhas cujo valor de coluna fica dentro de uma etapa do histograma, excluindo-se o limite superior. |
|equal_rows |**real** |Número estimado de linhas cujo valor de coluna é igual ao limite superior da etapa do histograma. |
|distinct_range_rows |**bigint** |Número estimado de linhas com um valor de coluna distinto dentro de uma etapa do histograma, excluindo-se o limite superior. |
|average_range_rows |**real** |Número médio de linhas com valores de colunas duplicados em uma etapa de histograma, exceto o limite superior (`RANGE_ROWS / DISTINCT_RANGE_ROWS` para `DISTINCT_RANGE_ROWS > 0`). |
  
 ## <a name="remarks"></a>Remarks  
 
 O conjunto de resultados para `sys.dm_db_stats_histogram` retorna informações semelhantes `DBCC SHOW_STATISTICS WITH HISTOGRAM` e também inclui `object_id`, `stats_id`, e `step_number`.

 Porque a coluna `range_high_key` é do tipo de dados sql_variant tipo, você precisará usar `CAST` ou `CONVERT` se um predicado de comparação com uma constante de cadeia de caracteres não.

### <a name="histogram"></a>Histograma
  
 Um histograma mede a frequência de ocorrência de cada valor distinto em um conjunto de dados. O otimizador de consulta calcula um histograma com base nos valores de coluna na primeira coluna de chave do objeto de estatísticas, selecionando os valores de coluna por amostragem estatística das linhas ou pela execução de uma verificação completa de todas as linhas na tabela ou na exibição. Se o histograma for criado com base em um conjunto amostrado de linhas, os totais armazenados para o número de linhas e o número de valores distintos são estimativas e não precisam ser números inteiros.  
  
 Para criar o histograma, o otimizador de consulta classifica os valores de colunas, calcula o número de valores que correspondem a cada valor de coluna distinta e agrega os valores de colunas em um máximo de 200 etapas de histograma contíguas. Cada etapa inclui uma gama de valores de colunas seguidos por um valor de coluna associada superior. O intervalo inclui todos os possíveis valores de coluna entre valores de limite, excluindo-se os próprios valores de limite em si. O mais baixo dos valores de coluna classificados é o valor do limite superior da primeira etapa do histograma.  
  
 O diagrama a seguir mostra um histograma com seis etapas: A área à esquerda do primeiro valor do limite superior corresponde à primeira etapa.  
  
 ![](../../relational-databases/system-dynamic-management-views/media/histogram_2.gif "Histograma")  
  
 Para cada etapa do histograma:  
  
-   A linha em negrito representa o valor do limite superior (*range_high_key*) e o número de vezes que ele ocorre (*equal_rows*)  
  
-   A área sólida à esquerda de *range_high_key* representa o intervalo de valores de coluna e o número médio de vezes que cada valor de coluna ocorre (*average_range_rows*). As *average_range_rows* da primeira etapa do histograma são sempre 0.  
  
-   As linhas pontilhadas representam os valores amostrados usados para estimar o número total de valores distintos no intervalo (*distinct_range_rows*) e o número total de valores no intervalo (*range_rows*). O otimizador de consulta usa *range_rows* e *distinct_range_rows* para calcular *average_range_rows* e não armazena os valores amostrados.  
  
 O otimizador de consulta define as etapas do histograma de acordo com o significado estatístico delas. Ele usa um algoritmo de diferença máxima para minimizar o número de etapas no histograma, enquanto maximiza a diferença entre os valores de limite. O número máximo de etapas é 200. O número de etapas do histograma pode ser menor do que o número de valores distintos, até mesmo para colunas com menos de 200 pontos de limite. Por exemplo, uma coluna com 100 valores distintos pode ter um histograma com menos de 100 pontos de limite.  
  
## <a name="permissions"></a>Permissões  

Requer que o usuário tenha permissões selecionadas em colunas de estatísticas, que ele possua a tabela ou que seja membro da função de servidor fixa `sysadmin`, da função de banco de dados fixa `db_owner` ou da função de banco de dados fixa `db_ddladmin`.

## <a name="examples"></a>Exemplos  

### <a name="a-simple-example"></a>A. Exemplo simples    
O exemplo a seguir cria e preenche uma tabela simples. Em seguida, cria estatísticas no `Country_Name` coluna.

```sql
CREATE TABLE Country
(Country_ID int IDENTITY PRIMARY KEY,
Country_Name varchar(120) NOT NULL);
INSERT Country (Country_Name) VALUES ('Canada'), ('Denmark'), ('Iceland'), ('Peru');

CREATE STATISTICS Country_Stats  
    ON Country (Country_Name) ;  
```   
A chave primária ocupa `stat_id` número 1, portanto, chame `sys.dm_db_stats_histogram` para `stat_id` número 2, para retornar o histograma de estatísticas para o `Country` tabela.    
```sql     
SELECT * FROM sys.dm_db_stats_histogram(OBJECT_ID('Country'), 2);
```

### <a name="b-useful-query"></a>B. Consulta úteis:   
```sql  
SELECT hist.step_number, hist.range_high_key, hist.range_rows, 
    hist.equal_rows, hist.distinct_range_rows, hist.average_range_rows
FROM sys.stats AS s
CROSS APPLY sys.dm_db_stats_histogram(s.[object_id], s.stats_id) AS hist
WHERE s.[name] = N'<statistic_name>';
```

### <a name="c-useful-query"></a>C. Consulta úteis:
O exemplo a seguir seleciona da tabela `Country` com um predicado na coluna `Country_Name`.

```sql  
SELECT * FROM Country 
WHERE Country_Name = 'Canada';
```

O exemplo a seguir examina a estatística criada anteriormente na tabela `Country` e coluna `Country_Name` para a etapa de histograma correspondência o predicado na consulta acima.

```sql  
SELECT ss.name, ss.stats_id, shr.steps, shr.rows, shr.rows_sampled, 
    shr.modification_counter, shr.last_updated, sh.range_rows, sh.equal_rows
FROM sys.stats ss
INNER JOIN sys.stats_columns sc 
    ON ss.stats_id = sc.stats_id AND ss.object_id = sc.object_id
INNER JOIN sys.all_columns ac 
    ON ac.column_id = sc.column_id AND ac.object_id = sc.object_id
CROSS APPLY sys.dm_db_stats_properties(ss.object_id, ss.stats_id) shr
CROSS APPLY sys.dm_db_stats_histogram(ss.object_id, ss.stats_id) sh
WHERE ss.[object_id] = OBJECT_ID('Country') 
    AND ac.name = 'Country_Name'
    AND sh.range_high_key = CAST('Canada' AS CHAR(8));
```
  
## <a name="see-also"></a>Consulte também  
[DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
[Objeto exibições de gerenciamento dinâmico relacionadas e funções (Transact-SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
