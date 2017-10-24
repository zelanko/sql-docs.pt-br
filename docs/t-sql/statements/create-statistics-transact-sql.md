---
title: "CRIAR estatísticas (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 105
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e09604deac2b823243515c10398dc27c75941bd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria estatísticas de otimização de consulta em uma ou mais colunas de uma tabela, uma exibição indexada ou uma tabela externa. Para a maioria das consultas, o otimizador de consulta já gera as estatísticas necessárias para um plano de consulta de alta qualidade; em alguns casos, você precisa criar estatísticas adicionais com CREATE STATISTICS ou modificar o design de consulta para melhorar o desempenho da consulta.  
  
 Para obter mais informações, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
          | STATS_STREAM = stats_stream ] ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ]  
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON [ database_name . [schema_name ] . | schema_name. ] table_name   
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
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>Argumentos  
 *statistics_name*  
 É o nome das estatísticas que devem ser criadas.  
  
 *table_or_indexed_view_name*  
 É o nome da tabela, exibição indexada ou tabela externa na qual deseja criar as estatísticas. Para criar estatísticas em outro banco de dados, especifique um nome de tabela qualificado.  
  
 *coluna [,... n]*  
 Uma ou mais colunas a serem incluídas nas estatísticas. As colunas devem ser em ordem de prioridade da esquerda para a direita. Apenas a primeira coluna é usada para criar o histograma. Todas as colunas são usadas para estatísticas de correlação entre colunas chamadas densidades.  
  
 É possível especificar qualquer coluna que possa ser especificada como uma coluna de chave de índice, com as seguintes exceções:  
  
-   **XML**, texto completo, e colunas FILESTREAM não podem ser especificadas.  
  
-   As colunas computadas poderão ser especificadas somente se as configurações de banco de dados ARITHABORT e QUOTED_IDENTIFIER forem ON.  
  
-   As colunas do tipo CLR definidas pelo usuário poderão ser especificadas se o tipo der suporte à ordenação binária. As colunas computadas definidas como invocações de método de uma coluna de tipo definida pelo usuário poderão ser especificadas se os métodos forem marcados como determinísticos.  
  
 ONDE \<filter_predicate > especifica uma expressão para selecionar um subconjunto de linhas a serem incluídas ao criar o objeto de estatísticas. As estatísticas criadas com um predicado de filtro são chamadas de estatísticas filtradas. O predicado de filtro usa a lógica de comparação simples e não pode fazer referência a uma coluna computada, uma coluna UDT, uma coluna de tipo de dados espaciais, ou um **hierarchyID** coluna de tipo de dados. Comparações que usam literais NULL não são permitidas com os operadores de comparação. Use os operadores IS NULL e IS NOT NULL em seu lugar.  
  
 Estes são alguns exemplos de predicados de filtro para a tabela Production.BillOfMaterials:  
  
 `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 `WHERE ComponentID IN (533, 324, 753)`  
  
 `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Para obter mais informações sobre predicados de filtro, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 FULLSCAN  
 Calcule as estatísticas verificando todas as linhas. FULLSCAN e SAMPLE 100 PERCENT têm os mesmos resultados. FULLSCAN não pode ser usado com a opção SAMPLE.  
  
 Quando omitido, o SQL Server usa amostragem para criar as estatísticas e determina o tamanho da amostra que é necessário para criar um plano de consulta de alta qualidade  
  
 EXEMPLO *número* {% | LINHAS}  
 Especifica a porcentagem aproximada ou o número de linhas da tabela ou da exibição indexada para uso do otimizador de consulta ao criar as estatísticas. Para PERCENT, *número* pode ser de 0 a 100 e para linhas, *número* pode estar entre 0 e o número total de linhas. A porcentagem real ou o número de linhas que o otimizador de consulta usa como exemplo talvez não corresponda à porcentagem ou ao número especificado. Por exemplo, o otimizador de consulta verifica todas as linhas de uma página de dados.  
  
 EXEMPLO é útil para casos especiais em que o plano de consulta, baseado na amostragem padrão, não é ideal. Na maioria das situações, não é necessário especificar SAMPLE porque o otimizador de consulta já usa amostragem e, por padrão, determina o tamanho da amostra estatisticamente significativa, conforme necessário para criar planos de consulta de alta qualidade.  
  
 SAMPLE não pode ser usado com a opção FULLSCAN. Quando nem SAMPLE nem FULLSCAN estão especificados, o otimizador de consulta usa dados de exemplo e computa o tamanho do exemplo por padrão.  
  
 Recomendamos especificar 0 PERCENT ou 0 ROWS. Quando 0 PERCENT ou ROWS é especificado, o objeto de estatísticas é criado, mas não contém dados de estatísticas.  
 
 PERSIST_SAMPLE_PERCENT = {ON | OFF}  
 Quando **ON**, as estatísticas reterá o percentual de amostragem de criação para as atualizações subsequentes que não especificam explicitamente um percentual de amostragem. Quando **OFF**, percentual de amostragem de estatísticas será redefinida para amostragem padrão em atualizações subsequentes que não especificam explicitamente um percentual de amostragem. O padrão é **OFF**. 
 
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 atualização cumulativa 4.  
  
 STATS_STREAM  **=**  *stats_stream*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 Desabilite AUTO_STATISTICS_UPDATE, opção de atualização automática de estatísticas para *statistics_name*. Se essa opção for especificada, o otimizador de consulta concluirá todas as atualizações de estatísticas em andamento para *statistics_name* e desabilitará atualizações futuras.  
  
 Para reabilitar atualizações de estatísticas, remova as estatísticas com [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) e, em seguida, execute CREATE STATISTICS sem a opção NORECOMPUTE.  
  
> [!WARNING]  
>  O uso dessa opção pode produzir planos de consulta de qualidade inferior. É recomendável usar essa opção moderadamente e somente por um administrador de sistema qualificado.  
  
 Para obter mais informações sobre a opção AUTO_STATISTICS_UPDATE, consulte [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para obter mais informações sobre como desabilitar e reabilitar atualizações de estatísticas, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
 INCREMENTAL = { ON | OFF }  
 Quando **ON**, as estatísticas serão criadas por estatísticas de partição. Quando **OFF**, estatísticas serão combinadas para todas as partições. O padrão é **OFF**.  
  
 Se as estatísticas por partição não tiverem suporte, um erro será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
  
-   Estatísticas criadas em bancos de dados somente leitura.  
  
-   Estatísticas criadas em índices filtrados.  
  
-   Estatísticas criadas em exibições.  
  
-   Estatísticas criadas em tabelas internas.  
  
-   Estatísticas criadas com índices espaciais ou índices XML.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer uma dessas permissões:  
  
-   ALTER TABLE  
  
-   Usuário é o proprietário da tabela  
  
-   Associação de **db_ddladmin** função de banco de dados fixa  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pode usar tempdb para classificar as linhas de amostra antes da criação de estatísticas.  
  
### <a name="statistics-for-external-tables"></a>Estatísticas para tabelas externas  
 Ao criar estatísticas de tabela externa, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importa a tabela externa para um temporário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da tabela e, em seguida, cria as estatísticas. Para estatísticas de exemplos, apenas as linhas de amostra são importadas. Se você tiver uma grande tabela externa, será muito mais rápido para usar a amostragem padrão em vez da opção de verificação completa.  
  
### <a name="statistics-with-a-filtered-condition"></a>Estatísticas com uma condição filtrada  
 As estatísticas filtradas podem melhorar o desempenho de consultas selecionadas em subconjuntos bem definidos de dados. Estatísticas filtradas usam um predicado de filtro na cláusula WHERE para selecionar o subconjunto de dados incluído nas estatísticas.  
  
### <a name="when-to-use-create-statistics"></a>Quando usar CREATE STATISTICS  
 Para obter mais informações sobre quando usar CREATE STATISTICS, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>Referenciando dependências de estatísticas filtradas  
 O [sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) exibição de catálogo controla cada coluna no predicado de estatísticas filtradas como uma dependência de referência. Avalie as operações realizadas nas colunas da tabela antes de criar estatísticas filtradas, pois não será possível remover, renomear ou alterar a definição de uma coluna da tabela que esteja definida em um predicado de estatísticas filtradas.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
*  Não há suporte para a atualização de estatísticas em tabelas externas. Para atualizar as estatísticas em uma tabela externa, descartar e recriar as estatísticas.  
*  Você pode listar até 64 colunas por objeto de estatísticas.
  
## <a name="examples"></a>Exemplos  

### <a name="examples-use-the-adventureworks-database"></a>Exemplos usam o banco de dados AdventureWorks.  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>A. Usando CREATE STATISTICS com SAMPLE número PERCENT  
 O exemplo a seguir cria a estatística `ContactMail1` utilizando uma amostra aleatória de 5% das colunas `BusinessEntityID` e `EmailPromotion` da tabela `Contact` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```t-sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. Usando CREATE STATISTICS com FULLSCAN e NORECOMPUTE  
 O exemplo a seguir cria a estatística `ContactMail2` de todas as linhas das colunas `BusinessEntityID` e `EmailPromotion` da tabela `Contact` e desabilita o recálculo de estatísticas.  
  
```t-sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. Usando CREATE STATISTICS para criar estatísticas filtradas  
 O exemplo a seguir cria as estatísticas filtradas `ContactPromotion1`. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz a amostragem de 50% dos dados e então seleciona as linhas com `EmailPromotion` igual a 2.  
  
```t-sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. Criar estatísticas em uma tabela externa  
 A decisão somente que você precisa tomar ao criar estatísticas em uma tabela externa, além de fornecer a lista de colunas, é criar as estatísticas por amostragem de linhas ou por meio do exame de todas as linhas.  
  
 Como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importa dados da tabela externa em uma tabela temporária para criar estatísticas, a opção de verificação completa irá demorar muito mais. Para uma tabela grande, o método de amostragem padrão normalmente é suficiente.  
  
```t-sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persistsamplepercent"></a>E. Usando CREATE STATISTICS com FULLSCAN e PERSIST_SAMPLE_PERCENT  
 O exemplo a seguir cria o `ContactMail2` estatísticas para todas as linhas de `BusinessEntityID` e `EmailPromotion` colunas do `Contact` de tabela e define uma porcentagem de amostragem de 100 por cento de todas as atualizações subsequentes que fazer explicitamente não especificar uma amostragem porcentagem.  
  
```t-sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>Exemplos do uso de banco de dados AdventureWorksDW. 
  
### <a name="f-create-statistics-on-two-columns"></a>F. Criar estatísticas em duas colunas  
 O exemplo a seguir cria o `CustomerStats1` estatísticas, com base no `CustomerKey` e `EmailAddress` colunas do `DimCustomer` tabela. As estatísticas são criadas com base em uma amostra estatisticamente significativa das linhas de `Customer` tabela.  
  
```t-sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. Criar estatísticas usando uma verificação completa  
 O exemplo a seguir cria o `CustomerStatsFullScan` estatísticas, com base na verificação de todas as linhas de `DimCustomer` tabela.  
  
```t-sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. Criar estatísticas, especificando a porcentagem de exemplo  
 O exemplo a seguir cria o `CustomerStatsSampleScan` estatísticas, com base na verificação de 50 por cento das linhas de `DimCustomer` tabela.  
  
```t-sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estatísticas](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  


