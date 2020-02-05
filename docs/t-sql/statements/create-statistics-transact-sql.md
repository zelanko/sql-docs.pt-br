---
title: CREATE STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STATISTICS
- STATISTICS_TSQL
- CREATE STATISTICS
- CREATE_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], creating
- indexed views [SQL Server], statistics
- FULLSCAN option
- CREATE STATISTICS statement
- filtered statistics [SQL Server]
- creating statistics [SQL Server]
- NORECOMPUTE clause
ms.assetid: b23e2f6b-076c-4e6d-9281-764bdb616ad2
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7efc30e37b1242c66df856f79944de687650b99d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982573"
---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria estatísticas de otimização de consulta em uma ou mais colunas de uma tabela, uma exibição indexada ou uma tabela externa. Para a maioria das consultas, o otimizador de consulta já gera as estatísticas necessárias para um plano de consulta de alta qualidade; em alguns casos, você precisa criar estatísticas adicionais com CREATE STATISTICS ou modificar o design de consulta para melhorar o desempenho da consulta.  
  
 Para obter mais informações, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create statistics on an external table  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WITH FULLSCAN ] ;  
  
-- Create statistics on a regular table or indexed view  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH   
        [ [ FULLSCAN   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | SAMPLE number { PERCENT | ROWS }   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | <update_stats_stream_option> [ ,...n ]    
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ]
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
    
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ] 
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( column_name  [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH {  
           FULLSCAN   
           | SAMPLE number PERCENT   
      }  
    ]  
[;]  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>Argumentos  
 *statistics_name*  
 É o nome das estatísticas que devem ser criadas.  
  
 *table_or_indexed_view_name*  
 É o nome da tabela, da exibição indexada ou da tabela externa na qual criar as estatísticas. Para criar estatísticas em outro banco de dados, especifique um nome de tabela qualificado.  
  
 *column [ ,...n]*  
 Uma ou mais colunas a serem incluídas nas estatísticas. As colunas devem estar em ordem de prioridade da esquerda para a direita. Apenas a primeira coluna é usada para criar o histograma. Todas as colunas são usadas para estatísticas de correlação entre colunas chamadas de densidades.  
  
 É possível especificar qualquer coluna que possa ser especificada como uma coluna de chave de índice, com as seguintes exceções:  
  
-   Colunas **Xml**, texto completo e FILESTREAM não podem ser especificadas.  
  
-   As colunas computadas poderão ser especificadas somente se as configurações de banco de dados ARITHABORT e QUOTED_IDENTIFIER forem ON.  
  
-   As colunas do tipo CLR definidas pelo usuário poderão ser especificadas se o tipo der suporte à ordenação binária. As colunas computadas definidas como invocações de método de uma coluna de tipo definida pelo usuário poderão ser especificadas se os métodos forem marcados como determinísticos.  
  
 WHERE \<filter_predicate> Especifica uma expressão para selecionar um subconjunto de linhas a serem incluídas durante a criação do objeto de estatísticas. As estatísticas criadas com um predicado de filtro são chamadas de estatísticas filtradas. O predicado de filtro usa a lógica de comparação simples e não pode fazer referência a uma coluna computada, a uma coluna UDT, a uma coluna de tipo de dados espacial ou a uma coluna de tipo de dados **hierarchyID**. Comparações que usam literais NULL não são permitidas com os operadores de comparação. Use os operadores IS NULL e IS NOT NULL em seu lugar.  
  
 Estes são alguns exemplos de predicados de filtro para a tabela Production.BillOfMaterials:  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Para obter mais informações sobre predicados filtrados, veja [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 FULLSCAN  
 Calcule as estatísticas verificando todas as linhas. FULLSCAN e SAMPLE 100 PERCENT têm os mesmos resultados. FULLSCAN não pode ser usado com a opção SAMPLE.  
  
 Quando omitido, o SQL Server usa amostragem para criar as estatísticas e determina o tamanho da amostra necessário para criar um plano de consulta de alta qualidade  
  
 SAMPLE *number* { PERCENT | ROWS }  
 Especifica a porcentagem aproximada ou o número de linhas da tabela ou da exibição indexada para uso do otimizador de consulta ao criar as estatísticas. Para PERCENT, *number* pode ser de 0 a 100 e, para ROWS, *number* pode ser de 0 ao número total de linhas. A porcentagem real ou o número de linhas que o otimizador de consulta usa como exemplo talvez não corresponda à porcentagem ou ao número especificado. Por exemplo, o otimizador de consulta verifica todas as linhas de uma página de dados.  
  
 SAMPLE é útil para casos especiais em que o plano de consulta, baseado na amostragem padrão, não é ideal. Na maioria das situações, não é necessário especificar SAMPLE porque o otimizador de consulta já usa amostragem e, por padrão, determina o tamanho da amostra estatisticamente significativa, conforme necessário para criar planos de consulta de alta qualidade.  
  
 SAMPLE não pode ser usado com a opção FULLSCAN. Quando nem SAMPLE nem FULLSCAN estão especificados, o otimizador de consulta usa dados de exemplo e computa o tamanho do exemplo por padrão.  
  
 Recomendamos especificar 0 PERCENT ou 0 ROWS. Quando 0 PERCENT ou ROWS está especificado, o objeto de estatísticas é criado, mas não contém dados estatísticos.  
 
 PERSIST_SAMPLE_PERCENT = { ON | OFF }  
 Quando for **ON**, as estatísticas reterão o percentual de amostragem de criação para as atualizações seguintes que não especificam explicitamente um percentual de amostragem. Quando for **OFF**, o percentual de amostragem de estatísticas será redefinido com a amostragem padrão nas atualizações seguintes que não especificam explicitamente um percentual de amostragem. O padrão é **OFF**. 
 
 > [!NOTE]
 > Se a tabela estiver truncada, todas as estatísticas criadas no HoBT truncado serão revertidas para usar a porcentagem de amostragem padrão.

 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4 em diante) e posterior (no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1 em diante).    
  
 STATS_STREAM **=** _stats_stream_  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 Desabilite a opção de atualização das estatísticas automáticas, AUTO_STATISTICS_UPDATE, para *statistics_name*. Se essa opção for especificada, o otimizador de consulta concluirá todas as atualizações de estatísticas em andamento para *statistics_name* e desabilitará atualizações futuras.  
  
 Para reabilitar atualizações de estatísticas, remova as estatísticas com [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) e execute CREATE STATISTICS sem a opção NORECOMPUTE.  
  
> [!WARNING]  
> O uso dessa opção pode produzir planos de consulta de qualidade inferior. É recomendável usar essa opção moderadamente e somente por um administrador de sistema qualificado.  
  
 Para obter mais informações sobre a opção AUTO_STATISTICS_UPDATE, veja [Opções de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para obter mais informações sobre como desabilitar e reabilitar atualizações de estatísticas, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
 INCREMENTAL = { ON | OFF }  
 Quando estiver **ON**, as estatísticas serão criadas conforme as estatísticas de partição. Quando **OFF**, as estatísticas serão combinadas para todas as partições. O padrão é **OFF**.  
  
 Se as estatísticas por partição não tiverem suporte, um erro será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
-   Estatísticas criadas em bancos de dados somente leitura.  
-   Estatísticas criadas em índices filtrados.  
-   Estatísticas criadas em exibições.  
-   Estatísticas criadas em tabelas internas.  
-   Estatísticas criadas com índices espaciais ou índices XML.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.  
  
MAXDOP = *max_degree_of_parallelism*  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 até [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3).  
  
 Substitui a opção de configuração **max degree of parallelism** enquanto durar a operação estatística. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação estatística paralela ao número especificado ou menos, com base na carga de trabalho atual do sistema.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 \<update_stats_stream_option> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="permissions"></a>Permissões  
 Requer uma destas permissões:  
  
-   ALTER TABLE  
-   Usuário é o proprietário da tabela  
-   Associação na função de banco de dados fixa **db_ddladmin**  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar tempdb para classificar as linhas de amostra antes de compilar estatísticas.  
  
### <a name="statistics-for-external-tables"></a>Estatísticas para tabelas externas  
 Ao criar estatísticas de tabela externa, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importa a tabela externa para uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] temporária e, em seguida, cria as estatísticas. Para estatísticas de amostra, apenas as linhas de amostra são importadas. Se você tiver uma tabela externa grande, será muito mais rápido usar a amostragem padrão, em vez da opção de verificação completa.  
  
### <a name="statistics-with-a-filtered-condition"></a>Estatísticas com uma condição filtrada  
 As estatísticas filtradas podem melhorar o desempenho de consultas selecionadas em subconjuntos bem definidos de dados. Estatísticas filtradas usam um predicado de filtro na cláusula WHERE para selecionar o subconjunto de dados incluído nas estatísticas.  
  
### <a name="when-to-use-create-statistics"></a>Quando usar CREATE STATISTICS  
 Para obter mais informações sobre quando usar CREATE STATISTICS, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>Referenciando dependências de estatísticas filtradas  
 A exibição do catálogo [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) controla cada coluna no predicado de estatísticas filtradas como uma dependência de referência. Avalie as operações realizadas nas colunas da tabela antes de criar estatísticas filtradas, pois não será possível remover, renomear ou alterar a definição de uma coluna da tabela que esteja definida em um predicado de estatísticas filtradas.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
* Não há compatibilidade com a atualização de estatística em tabelas externas. Para atualizar as estatísticas em uma tabela externa, remova e recrie as estatísticas.  
* Você pode listar até 64 colunas por objeto de estatísticas.
* A opção MAXDOP não é compatível com as opções STATS_STREAM, ROWCOUNT e PAGECOUNT.
* A opção MAXDOP é limitada pela configuração MAX_DOP de grupo de carga de trabalho de Resource Governor, se usada.
  
## <a name="examples"></a>Exemplos  

### <a name="examples-use-the-adventureworks-database"></a>Os exemplos usam o banco de dados AdventureWorks.  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>a. Usando CREATE STATISTICS com SAMPLE número PERCENT  
 O exemplo a seguir cria a estatística `ContactMail1` utilizando uma amostra aleatória de 5% das colunas `BusinessEntityID` e `EmailPromotion` da tabela `Person` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. Usando CREATE STATISTICS com FULLSCAN e NORECOMPUTE  
 O exemplo a seguir cria a estatística `NamePurchase` de todas as linhas das colunas `BusinessEntityID` e `EmailPromotion` da tabela `Person` e desabilita o recálculo de estatísticas.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. Usando CREATE STATISTICS para criar estatísticas filtradas  
 O exemplo a seguir cria as estatísticas filtradas `ContactPromotion1`. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz a amostragem de 50% dos dados e então seleciona as linhas com `EmailPromotion` igual a 2.  
  
```sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. Criar estatísticas em uma tabela externa  
 A única decisão que você precisa tomar ao criar estatísticas em uma tabela externa, além de fornecer a lista de colunas, é criar as estatísticas por amostragem de linhas ou verificando todas as linhas.  
  
 Uma vez que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importa dados da tabela externa para uma tabela temporária para criar estatísticas, a opção de verificação completa demorará muito mais. Para uma tabela grande, o método de amostragem padrão normalmente é suficiente.  
  
```sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persist_sample_percent"></a>E. Usando CREATE STATISTICS com FULLSCAN e PERSIST_SAMPLE_PERCENT  
 O exemplo a seguir cria estatísticas `NamePurchase` para todas as linhas nas colunas `BusinessEntityID` e `EmailPromotion` da tabela `Person` e define um percentual de amostragem de 100 por cento de todas as atualizações subsequentes que não especificam explicitamente um percentual de amostragem.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>Exemplos do uso de banco de dados AdventureWorksDW. 
  
### <a name="f-create-statistics-on-two-columns"></a>F. Criar estatísticas em duas colunas  
 O exemplo a seguir cria as estatísticas `CustomerStats1` com base nas colunas `CustomerKey` e `EmailAddress` da tabela `DimCustomer`. As estatísticas são criadas com base em uma amostragem estatisticamente significativa das linhas na tabela `Customer`.  
  
```sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. Criar estatísticas usando uma verificação completa  
 O exemplo a seguir cria as estatísticas de `CustomerStatsFullScan` com base na verificação de todas as linhas da tabela `DimCustomer`.  
  
```sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. Criar estatísticas especificando o percentual de amostra  
 O exemplo a seguir cria as estatísticas de `CustomerStatsSampleScan` com base na verificação de 50 por cento de todas as linhas da tabela `DimCustomer`.  
  
```sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Estatística](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

