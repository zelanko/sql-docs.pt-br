---
title: UPDATE STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: "74"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b619b3cf7ea50fb87e18fd96e8a85a2a231d21f5
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Atualiza estatísticas de otimização de consulta de uma tabela ou exibição indexada. Por padrão, o otimizador de consulta já atualiza estatísticas conforme necessário para melhorar o plano de consulta; em alguns casos você pode melhorar o desempenho da consulta usando UPDATE STATISTICS ou o procedimento armazenado [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) para atualizar estatísticas com mais frequência do que as atualizações padrão.  
  
 A atualização de estatísticas assegura que as consultas sejam compiladas com estatísticas atualizadas. Porém, a atualização de estatísticas faz com que as consultas sejam recompiladas. É recomendável não atualizar estatísticas com muita frequência porque existe uma compensação de desempenho entre o aprimoramento dos planos de consulta e o tempo necessário para recompilar consultas. As compensações específicas dependem do seu aplicativo. UPDATE STATISTICS pode usar tempdb para classificar o exemplo de linhas para compilação de estatísticas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
              [ ON PARTITIONS ( { <partition_number> | <range> } [, …n] ) ]  
            | <update_stats_stream_option> [ ,...n ]  
        ]   
        [ [ , ] [ ALL | COLUMNS | INDEX ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ]  
    ] ;  
  
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
UPDATE STATISTICS schema_name . ] table_name   
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
  
## <a name="arguments"></a>Argumentos  
 *table_or_indexed_view_name*  
 É o nome da tabela ou exibição indexada que contém o objeto de estatísticas.  
  
 *index_or_statistics_name*  
 É o nome do índice no qual atualizar estatísticas ou o nome das estatísticas a serem atualizadas. Se *index_or_statistics_name* não for especificado, o otimizador de consulta atualiza todas as estatísticas para a tabela ou exibição indexada. Isso inclui as estatísticas criadas com a instrução CREATE STATISTICS, as estatísticas de coluna única criadas quando a instrução AUTO_CREATE_STATISTICS está ativa e as estatísticas criadas para índices.  
  
 Para obter mais informações sobre AUTO_CREATE_STATISTICS, consulte [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para exibir todos os índices de uma tabela ou exibição, você pode usar [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 FULLSCAN  
 Calcule as estatísticas verificando todas as linhas da tabela ou da exibição indexada. FULLSCAN e SAMPLE 100 PERCENT têm os mesmos resultados. FULLSCAN não pode ser usado com a opção SAMPLE.  
  
 EXEMPLO *número* {% | LINHAS}  
 Especifica a porcentagem aproximada ou o número de linhas da tabela ou da exibição indexada para uso do otimizador de consulta ao atualizar as estatísticas. Para PERCENT, *número* pode ser de 0 a 100 e para linhas, *número* pode estar entre 0 e o número total de linhas. A porcentagem real ou o número de linhas que o otimizador de consulta usa como exemplo talvez não corresponda à porcentagem ou ao número especificado. Por exemplo, o otimizador de consulta verifica todas as linhas de uma página de dados.  
  
 EXEMPLO é útil para casos especiais em que o plano de consulta, baseado na amostragem padrão, não é ideal. Na maioria das situações, não é necessário especificar SAMPLE porque o otimizador de consulta usa amostragem e, por padrão, determina o tamanho da amostra estatisticamente significativa, conforme necessário, para criar planos de consulta de alta qualidade. 
 
Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], amostragem de dados para a criação de estatísticas é executada em paralelo, ao usar o nível de compatibilidade 130, para melhorar o desempenho da coleta de estatísticas. O otimizador de consulta usará estatísticas de exemplo paralelo, sempre que um tamanho de tabela excede um certo limite. 
   
 SAMPLE não pode ser usado com a opção FULLSCAN. Quando nem SAMPLE nem FULLSCAN estão especificados, o otimizador de consulta usa dados de exemplo e computa o tamanho do exemplo por padrão.  
  
 Recomendamos especificar 0 PERCENT ou 0 ROWS. Quando 0 PERCENT ou ROWS é especificado, o objeto de estatísticas é atualizado, mas não contém dados estatísticos.  
  
 Para a maioria das cargas de trabalho, uma verificação completa não é necessária e amostragem padrão é adequada.  
No entanto, determinadas cargas de trabalho que são sensíveis a diferentes amplamente distribuições de dados podem exigir um tamanho maior de exemplo, ou até mesmo uma verificação completa.  
Para obter mais informações, consulte o [blog CSS SQL escalonamento Services](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx).  
  
 RESAMPLE  
 Atualiza cada estatística usando sua taxa de amostragem mais recente.  
  
 O uso de RESAMPLE pode resultar em um exame de tabela completa. Por exemplo, estatísticas de índices usam um exame de tabela completa para sua taxa de amostragem. Quando nenhuma das opções de exemplo (SAMPLE, FULLSCAN, RESAMPLE) é especificada, o otimizador de consulta usa os dados de exemplo e computa o tamanho de exemplo por padrão.  

PERSIST_SAMPLE_PERCENT = {ON | OFF}  
Quando **ON**, as estatísticas reterá o percentual de amostragem do conjunto de atualizações subsequentes que não especificam explicitamente um percentual de amostragem. Quando **OFF**, percentual de amostragem de estatísticas será redefinida para amostragem padrão em atualizações subsequentes que não especificam explicitamente um percentual de amostragem. O padrão é **OFF**. 
 
 > [!NOTE]
 > Se AUTO_UPDATE_STATISTICS é executado, ele usa o percentual de amostragem persistente, se disponível, ou use percentual de amostragem padrão se não.
 > Criar nova amostra comportamento não é afetado por essa opção.
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) e [sys.DM db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) expor o valor de porcentagem de amostra persistente para a estatística selecionada.
 
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4) por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1).  
 
 PARTIÇÕES ({ \<número_da_partição > | \<intervalo >} [,... n]) ] Força as estatísticas de nível folha que abrangem as partições especificadas na cláusula ON PARTITIONS a serem recomputadas e, em seguida, mescladas para criar estatísticas globais. WITH RESAMPLE é necessário porque as estatísticas de partições criadas com taxas de amostragem diferentes não podem ser mescladas em conjunto.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ALL | COLUMNS | INDEX  
 Atualize todas as estatísticas existentes, as estatísticas criadas em uma ou mais colunas ou as estatísticas criadas para índices. Se nenhuma das opções for especificada, a instrução UPDATE STATISTICS atualizará todas as estatísticas na tabela ou na exibição indexada.  
  
 NORECOMPUTE  
 Desabilite a opção de atualização das estatísticas automáticas, AUTO_UPDATE_STATISTICS, das estatísticas especificadas. Se essa opção for especificada, o otimizador de consulta concluirá essa atualização de estatísticas e desabilitará atualizações futuras.  
  
 Para reabilitar o comportamento da opção AUTO_UPDATE_STATISTICS, execute UPDATE STATISTICS novamente sem a opção NORECOMPUTE ou execute **sp_autostats**.  
  
> [!WARNING]  
>  O uso dessa opção pode produzir planos de consulta de qualidade inferior. É recomendável usar essa opção moderadamente e somente por um administrador de sistema qualificado.  
  
 Para obter mais informações sobre a opção AUTO_STATISTICS_UPDATE, consulte [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = { ON | OFF }  
 Quando **ON**, as estatísticas serão recriadas por estatísticas de partição. Quando **OFF**, a árvore de estatísticas é descartada e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recomputará as estatísticas. O padrão é **OFF**.  
  
 Se as estatísticas por partição não tiverem suporte, um erro será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
  
-   Estatísticas criadas em bancos de dados somente leitura.  
  
-   Estatísticas criadas em índices filtrados.  
  
-   Estatísticas criadas em exibições.  
  
-   Estatísticas criadas em tabelas internas.  
  
-   Estatísticas criadas com índices espaciais ou índices XML.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 \<update_stats_stream_option >[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="remarks"></a>Remarks  
  
## <a name="when-to-use-update-statistics"></a>Quando usar UPDATE STATISTICS  
 Para obter mais informações sobre quando usar UPDATE STATISTICS, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
## <a name="updating-all-statistics-with-spupdatestats"></a>Atualizando todas as estatísticas com sp_updatestats  
 Para obter informações sobre como atualizar estatísticas de todas as tabelas definidas pelo usuário e internas no banco de dados, veja o procedimento armazenado [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md). Por exemplo, o comando a seguir chama sp_updatestats para atualizar todas as estatísticas do banco de dados.  
  
```sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>Determinando a última atualização das estatísticas  
 Para determinar quando as estatísticas foram atualizadas pela última vez, use a função [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) .  
  
## <a name="pdw--sql-data-warehouse"></a>PDW / SQL Data Warehouse  
 Não há suporte para a seguinte sintaxe por PDW / SQL Data Warehouse  
  
```sql  
update statistics t1 (a,b);   
```  
  
```sql  
update statistics t1 (a) with sample 10 rows;  
```  
  
```sql  
update statistics t1 (a) with NORECOMPUTE;  
```  
  
```sql  
update statistics t1 (a) with INCREMENTAL=ON;  
```  
  
```sql  
update statistics t1 (a) with stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER na tabela ou exibição.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-update-all-statistics-on-a-table"></a>A. Atualizar todas as estatísticas de uma tabela  
 O exemplo a seguir atualiza as estatísticas para todos os índices no `SalesOrderDetail` tabela.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>E. Atualizar estatísticas em uma tabela  
 A exemplo a seguir atualiza o `CustomerStats1` estatísticas sobre o `Customer` tabela.  
  
```sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>F. Atualizar estatísticas usando uma verificação completa  
 A exemplo a seguir atualiza o `CustomerStats1` estatísticas, com base na verificação de todas as linhas de `Customer` tabela.  
  
```sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>G. Atualizar todas as estatísticas de uma tabela  
 O exemplo a seguir atualiza todas as estatísticas sobre o `Customer` tabela.  
  
```sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Estatísticas](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40; Transact-SQL &#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  



