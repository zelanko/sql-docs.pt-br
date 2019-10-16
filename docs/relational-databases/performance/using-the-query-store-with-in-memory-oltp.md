---
title: Usar o Repositório de Consultas com OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db274ccde27abf92617e0eadf95b1971e740705a
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251299"
---
# <a name="using-the-query-store-with-in-memory-oltp"></a>Como usar o Repositório de Consultas com OLTP in-memory
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Repositório de Consultas permite que você monitore o desempenho do código compilado nativamente para cargas de trabalho executando o OLTP in-memory.  
Estatísticas de compilação e de tempo de execução são coletadas e expostas da mesma forma que as cargas de trabalho com base em disco.   
Ao migrar para o OLTP in-memory, você pode continuar usando os modos de exibição do Repositório de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , bem como scripts personalizados que você desenvolveu para cargas de trabalho com base em disco antes da migração. Isso economiza seu investimento no aprendizado da tecnologia de Repositório de Consultas e o torna amplamente utilizável para solucionar problemas com todos os tipos de cargas de trabalho.  
Para obter informações gerais sobre como usar o Repositório de Consultas, confira [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
 O uso do Repositório de Consultas com OLTP in-memory não exige qualquer configuração de recurso adicional. Quando você o ativa em seu banco de dados, ele funciona para todos os tipos de cargas de trabalho.   
No entanto, há alguns aspectos específicos dos quais os usuários devem estar cientes ao usar o Repositório de Consultas com OLTP in-memory:  
  
-   Quando o Repositório de Consultas é habilitado, as estatísticas de consultas, planos e tempo de compilação são coletadas por padrão. No entanto, a coleta de estatísticas de tempo de execução não é ativada, a menos que você a habilite com [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
-   Quando você define *\@new_collection_value* como 0, o Repositório de Consultas deixa de coletar estatísticas de tempo de execução do procedimento afetado ou para toda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O valor configurado com [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) não é persistente. Verifique e configure novamente a coleta de estatísticas após a reinicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Assim como ocorre com a coleta normal de estatísticas de consulta, o desempenho pode ser prejudicado quando você usa o Repositório de Consultas para monitorar a execução da carga de trabalho. Convém considerar a habilitação da coleta de estatísticas somente para um subconjunto importante de procedimentos armazenados compilados nativamente.  
  
-   Consultas e planos são capturados e armazenados na primeira compilação nativa, e atualizados após cada recompilação.  
  
-   Se você habilitou o Repositório de Consultas ou limpou seu conteúdo após a compilação de todos os procedimentos armazenados nativos, será necessário recompilá-los manualmente para que eles sejam capturados pelo Repositório de Consultas. O mesmo se aplica se você removeu consultas manualmente usando [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) ou [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md). Use [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) para forçar a recompilação do procedimento.  
  
-   O Repositório de Consultas aproveita os mecanismos de geração de plano do OLTP in-memory para capturar o plano de execução de consulta durante a compilação. O plano armazenado é semanticamente equivalente a um plano obtido com o uso de `SET SHOWPLAN_XML ON` com uma diferença; os planos no Repositório de Consultas são sempre divididos e armazenados por instrução individual.  
    
-   Ao executar o Repositório de Consultas em um banco de dados com uma carga de trabalho mista, é possível usar o campo **is_natively_compiled** do [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) para localizar rapidamente os planos de consulta gerados pela compilação de código nativo.  
  
-   O modo de captura do Repositório de Consultas (o parâmetro *QUERY_CAPTURE_MODE* na instrução **ALTER TABLE**) não afeta as consultas de módulos compilados de modo nativo, pois elas são sempre capturadas, independentemente do valor configurado. Isso inclui a configuração de `QUERY_CAPTURE_MODE = NONE`.  
  
-   A duração da compilação de consulta capturada pelo Repositório de Consultas inclui apenas o tempo gasto na otimização da consulta, antes da geração do código nativo. Mais precisamente, não inclui o tempo de compilação do código C e a geração de estruturas internas necessárias para geração de código C.  
  
-   As métricas de concessões de memória em [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) não são populadas em consultas compiladas de modo nativo – seus valores são sempre 0. As colunas de concessão de memória são: avg_query_max_used_memory, last_query_max_used_memory, min_query_max_used_memory, max_query_max_used_memory e stdev_query_max_used_memory.  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>Como habilitar e usar o Repositório de Consultas com OLTP in-memory  
 O exemplo simples a seguir demonstra o uso do Repositório de Consultas com OLTP in-memory em um cenário de usuário de ponta a ponta. Neste exemplo, vamos supor que um banco de dados (`MemoryOLTP`) esteja habilitado para OLTP in-memory.  
    Para obter mais detalhes sobre os pré-requisitos para tabelas com otimização de memória, veja [Criando uma tabela com otimização de memória e um procedimento armazenado compilado nativamente](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Criando uma tabela com otimização de memória e um procedimento armazenado compilado nativamente](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Procedimentos armazenados do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
