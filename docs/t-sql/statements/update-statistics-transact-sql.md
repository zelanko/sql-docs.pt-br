---
description: UPDATE STATISTICS (Transact-SQL)
title: UPDATE STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c338ebb3f64dc1752c4e68e33f6954e554d6d4e6
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91227420"
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Atualiza estatísticas de otimização de consulta de uma tabela ou exibição indexada. Por padrão, o otimizador de consulta já atualiza estatísticas conforme necessário para melhorar o plano de consulta, em alguns casos, é possível melhorar o desempenho de consulta usando `UPDATE STATISTICS` ou o procedimento armazenado [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) para atualizar estatísticas com mais frequência do que as atualizações padrão.  
  
A atualização de estatísticas assegura que as consultas sejam compiladas com estatísticas atualizadas. Porém, a atualização de estatísticas faz com que as consultas sejam recompiladas. É recomendável não atualizar estatísticas com muita frequência porque existe uma compensação de desempenho entre o aprimoramento dos planos de consulta e o tempo necessário para recompilar consultas. As compensações específicas dependem do seu aplicativo. `UPDATE STATISTICS` pode usar tempdb para classificar o exemplo de linhas para compilação de estatísticas.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
UPDATE STATISTICS table_or_indexed_view_name   
    [   
        {   
            { index_or_statistics__name }  
          | ( { index_or_statistics_name } [ ,...n ] )   
                }  
    ]   
    [    WITH   
        [  
            FULLSCAN   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | SAMPLE number { PERCENT | ROWS }   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | RESAMPLE   
              [ ON PARTITIONS ( { <partition_number> | <range> } [, ...n] ) ]  
            | <update_stats_stream_option> [ ,...n ]  
        ]   
        [ [ , ] [ ALL | COLUMNS | INDEX ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ] 
    ] ;  
  
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ]  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
UPDATE STATISTICS [ schema_name . ] table_name   
    [ ( { statistics_name | index_name } ) ]  
    [ WITH   
       {  
              FULLSCAN   
            | SAMPLE number PERCENT   
            | RESAMPLE   
        }  
    ]  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *table_or_indexed_view_name*  
 É o nome da tabela ou da exibição indexada que contém o objeto de estatísticas.  
  
 *index_or_statistics_name*  
 É o nome do índice no qual atualizar estatísticas ou o nome das estatísticas a serem atualizadas. Se *index_or_statistics_name* não for especificado, o otimizador de consulta atualizará todas as estatísticas da tabela ou da exibição indexada. Isso inclui as estatísticas criadas com a instrução CREATE STATISTICS, as estatísticas de coluna única criadas quando a instrução AUTO_CREATE_STATISTICS está ativa e as estatísticas criadas para índices.  
  
 Para obter mais informações sobre AUTO_CREATE_STATISTICS, consulte [Opções de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para exibir todos os índices de uma tabela ou exibição, use [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 FULLSCAN  
 Calcule as estatísticas verificando todas as linhas da tabela ou da exibição indexada. FULLSCAN e SAMPLE 100 PERCENT têm os mesmos resultados. FULLSCAN não pode ser usado com a opção SAMPLE.  
  
 SAMPLE *number* { PERCENT | ROWS }  
 Especifica a porcentagem aproximada ou o número de linhas da tabela ou da exibição indexada para uso do otimizador de consulta ao atualizar as estatísticas. Para PERCENT, *number* pode ser de 0 a 100 e, para ROWS, *number* pode ser de 0 ao número total de linhas. A porcentagem real ou o número de linhas que o otimizador de consulta usa como exemplo talvez não corresponda à porcentagem ou ao número especificado. Por exemplo, o otimizador de consulta verifica todas as linhas de uma página de dados.  
  
 SAMPLE é útil para casos especiais em que o plano de consulta, baseado na amostragem padrão, não é ideal. Na maioria das situações, não é necessário especificar SAMPLE porque o otimizador de consulta usa amostragem e, por padrão, determina o tamanho da amostra estatisticamente significativa, conforme necessário, para criar planos de consulta de alta qualidade. 
 
Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a amostragem de dados para criar estatísticas é feita em paralelo, ao usar o nível de compatibilidade 130, para melhorar o desempenho da coleta de estatísticas. O otimizador de consulta usará estatísticas de amostra paralelas sempre que um tamanho de tabela exceder determinado limite. 
   
 SAMPLE não pode ser usado com a opção FULLSCAN. Quando nem SAMPLE nem FULLSCAN estão especificados, o otimizador de consulta usa dados de exemplo e computa o tamanho do exemplo por padrão.  
  
 Recomendamos especificar 0 PERCENT ou 0 ROWS. Quando 0 PERCENT ou ROWS é especificado, o objeto de estatísticas é atualizado, mas não contém dados estatísticos.  
  
 Para a maioria das cargas de trabalho, uma verificação completa não é necessária e a amostragem padrão é adequada.  
No entanto, algumas cargas de trabalho que são sensíveis a distribuições de dados com ampla variação podem exigir um tamanho maior de amostra ou até mesmo uma verificação completa.  
Para obter mais informações, confira o [blog CSS SQL Escalation Services](https://docs.microsoft.com/archive/blogs/psssql/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed) (Serviços de escalonamento do CSS SQL).  
  
 RESAMPLE  
 Atualiza cada estatística usando sua taxa de amostragem mais recente.  
  
 O uso de RESAMPLE pode resultar em um exame de tabela completa. Por exemplo, estatísticas de índices usam um exame de tabela completa para sua taxa de amostragem. Quando nenhuma das opções de exemplo (SAMPLE, FULLSCAN, RESAMPLE) é especificada, o otimizador de consulta usa os dados de exemplo e computa o tamanho de exemplo por padrão.  

PERSIST_SAMPLE_PERCENT = { ON | OFF }  
Quando for **ON**, as estatísticas reterão o percentual de amostragem definido para as atualizações seguintes que não especificam explicitamente um percentual de amostragem. Quando for **OFF**, o percentual de amostragem de estatísticas será redefinido com a amostragem padrão nas atualizações seguintes que não especificam explicitamente um percentual de amostragem. O padrão é **OFF**. 
 
 > [!NOTE]
 > Se AUTO_UPDATE_STATISTICS for executado, ele usará o percentual de amostragem persistente, se disponível; caso contrário, ele usará o percentual de amostragem padrão.
 > O comportamento de RESAMPLE não é afetado por essa opção.
 
 > [!NOTE]
 > Se a tabela estiver truncada, todas as estatísticas criadas no HoBT truncado serão revertidas para usar a porcentagem de amostragem padrão.
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) e [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) expõem o valor de percentual de amostra persistente para a estatística selecionada.
 
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4 em diante) e posterior (no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1 em diante).  
 
 ON PARTITIONS ( { \<partition_number> | \<range> } [, ...n] ) ] força as estatísticas de nível folha que abrangem as partições especificadas na cláusula ON PARTITIONS a serem recalculadas e mescladas para criar as estatísticas globais. WITH RESAMPLE é necessário porque as estatísticas de partições criadas com taxas de amostragem diferentes não podem ser mescladas em conjunto.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior
  
 ALL | COLUMNS | INDEX  
 Atualize todas as estatísticas existentes, as estatísticas criadas em uma ou mais colunas ou as estatísticas criadas para índices. Se nenhuma das opções for especificada, a instrução UPDATE STATISTICS atualizará todas as estatísticas na tabela ou na exibição indexada.  
  
 NORECOMPUTE  
 Desabilite a opção de atualização das estatísticas automáticas, AUTO_UPDATE_STATISTICS, das estatísticas especificadas. Se essa opção for especificada, o otimizador de consulta concluirá essa atualização de estatísticas e desabilitará atualizações futuras.  
  
 Para reabilitar o comportamento da opção AUTO_UPDATE_STATISTICS, execute UPDATE STATISTICS novamente sem a opção NORECOMPUTE ou execute **sp_autostats**.  
  
> [!WARNING]  
> O uso dessa opção pode produzir planos de consulta de qualidade inferior. É recomendável usar essa opção moderadamente e somente por um administrador de sistema qualificado.  
  
 Para obter mais informações sobre a opção AUTO_STATISTICS_UPDATE, veja [Opções de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = { ON | OFF }  
 Quando for **ON**, as estatísticas serão recriadas por estatísticas de partição. Quando estiver **OFF**, a árvore de estatísticas será removida e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] calculará as estatísticas novamente. O padrão é **OFF**.  
  
 Se as estatísticas por partição não tiverem suporte, um erro será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
-   Estatísticas criadas em bancos de dados somente leitura.  
-   Estatísticas criadas em índices filtrados.  
-   Estatísticas criadas em exibições.  
-   Estatísticas criadas em tabelas internas.  
-   Estatísticas criadas com índices espaciais ou índices XML.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior

MAXDOP = *max_degree_of_parallelism*  
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3).  
  
 Substitui a opção de configuração **max degree of parallelism** enquanto durar a operação estatística. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação estatística paralela ao número especificado ou menos, com base na carga de trabalho atual do sistema.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 \<update_stats_stream_option> 
 
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="remarks"></a>Comentários  
  
### <a name="when-to-use-update-statistics"></a>Quando usar UPDATE STATISTICS  
 Para obter mais informações sobre quando usar `UPDATE STATISTICS`, confira [Estatísticas](../../relational-databases/statistics/statistics.md).  

### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
* Não há compatibilidade com a atualização de estatística em tabelas externas. Para atualizar as estatísticas em uma tabela externa, remova e recrie as estatísticas.  
* A opção `MAXDOP` não é compatível com as opções `STATS_STREAM`, `ROWCOUNT` e `PAGECOUNT`.
* A opção `MAXDOP` é limitada pela configuração `MAX_DOP` de grupo de carga de trabalho de Resource Governor, se usada.

### <a name="updating-all-statistics-with-sp_updatestats"></a>Atualizando todas as estatísticas com sp_updatestats  
Para obter informações sobre como atualizar estatísticas de todas as tabelas definidas pelo usuário e internas no banco de dados, veja o procedimento armazenado [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md). Por exemplo, o comando a seguir chama sp_updatestats para atualizar todas as estatísticas do banco de dados.  
  
```sql  
EXEC sp_updatestats;  
```  

### <a name="automatic-index-and-statistics-management"></a>Índice automático e gerenciamento de estatísticas
Aproveite soluções como a [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para gerenciar automaticamente a desfragmentação de índice e as atualizações de estatísticas em um ou mais bancos de dados. Este procedimento escolhe automaticamente se deve recompilar ou reorganizar um índice de acordo com seu nível de fragmentação, entre outros parâmetros, e atualizar as estatísticas com um limite linear.
  
### <a name="determining-the-last-statistics-update"></a>Determinando a última atualização das estatísticas  
 Para determinar quando as estatísticas foram atualizadas pela última vez, use a função [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) .  
  
### <a name="pdw--azure-synapse-analytics"></a>PDW/Azure Synapse Analytics  
 A sintaxe a seguir não têm suporte no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] / [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]  
  
```syntaxsql
UPDATE STATISTICS t1 (a,b);   
```  
  
```sql  
UPDATE STATISTICS t1 (a) WITH SAMPLE 10 ROWS;  
```  
  
```sql  
UPDATE STATISTICS t1 (a) WITH NORECOMPUTE;  
```  
  
```sql  
UPDATE STATISTICS t1 (a) WITH INCREMENTAL = ON;  
```  
  
```sql  
UPDATE STATISTICS t1 (a) WITH stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER` na tabela ou exibição.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-update-all-statistics-on-a-table"></a>a. Atualizar todas as estatísticas de uma tabela  
 O exemplo a seguir atualiza as estatísticas de todos os índices na tabela `SalesOrderDetail`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail;  
GO  
```  
  
### <a name="b-update-the-statistics-for-an-index"></a>B. Atualizar as estatísticas de um índice  
 O exemplo a seguir atualiza as estatísticas do índice `AK_SalesOrderDetail_rowguid` da tabela `SalesOrderDetail`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;  
GO  
```  
  
### <a name="c-update-statistics-by-using-50-percent-sampling"></a>C. Atualizar estatísticas com o uso de amostragem de 50 por cento  
 O exemplo a seguir cria e atualiza as estatísticas das colunas `Name` e `ProductNumber` na tabela `Product`.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS Products  
    ON Production.Product ([Name], ProductNumber)  
    WITH SAMPLE 50 PERCENT  
-- Time passes. The UPDATE STATISTICS statement is then executed.  
UPDATE STATISTICS Production.Product(Products)   
    WITH SAMPLE 50 PERCENT;  
```  
  
### <a name="d-update-statistics-by-using-fullscan-and-norecompute"></a>D. Atualizar estatísticas com o uso de FULLSCAN e NORECOMPUTE  
 O exemplo a seguir atualiza as estatísticas `Products` na tabela `Product` força um exame completo de todas as linhas na tabela `Product` e desativa a atualização automática das estatísticas de `Products`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Production.Product(Products)  
    WITH FULLSCAN, NORECOMPUTE;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>E. Atualizar as estatísticas em uma tabela  
 O exemplo a seguir atualiza as estatísticas de `CustomerStats1` na tabela `Customer`.  
  
```sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>F. Atualizar estatísticas usando uma verificação completa  
 O exemplo a seguir atualiza as estatísticas de `CustomerStats1`, com base na verificação de todas as linhas da tabela `Customer`.  
  
```sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>G. Atualizar todas as estatísticas de uma tabela  
 O exemplo a seguir atualiza todas as estatísticas na tabela `Customer`.  
  
```sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Estatística](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)    
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
