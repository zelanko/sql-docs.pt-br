---
title: Monitorando o desempenho usando o Repositório de Consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5a57623bc05b443de086835374b5f409f630b9de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37184273"
---
# <a name="monitoring-performance-by-using-the-query-store"></a>Monitoring Performance By Using the Query Store
  O recurso repositório de consultas fornece aos DBAs insights sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, permitindo que você localize rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O recurso captura automaticamente um histórico de consultas, planos e estatísticas de tempo de execução e os mantém para sua análise. Ele separa os dados por janelas de tempo, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor. O repositório de consultas pode ser configurado usando o [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) opção.  
  
||  
|-|  
|**Aplica-se ao**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([obtê-la](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
> [!IMPORTANT]  
>  Este é um recurso de visualização. Para usar o repositório de consultas, você deve reconhecer e concordar que a implementação do repositório está sujeita aos termos de visualização anteriores do contrato de licença (por exemplo, Contrato Enterprise, Contrato do Microsoft Azure ou Contrato de Assinatura do Microsoft Online), bem como quaisquer [Termos suplementares de uso da Visualização do Microsoft Azure](http://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)aplicáveis.  
  
##  <a name="Enabling"></a> Habilitando o Repositório de Consultas  
 O repositório de consultas não está ativo para novos bancos de dados por padrão.  
  
#### <a name="by-using-the-query-store-page-in-management-studio"></a>Usando a página Repositório de Consultas no Management Studio  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um banco de dados e clique em **Propriedades**. (Requer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versão de 2016 do [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].)  
  
2.  Na caixa de diálogo **Propriedades do Banco de Dados** , selecione a página **Repositório de Consultas** .  
  
3.  Na caixa **Habilitar** selecione **Verdadeiro**.  
  
#### <a name="by-using-transact-sql-statements"></a>Usando as instruções Transact-SQL  
  
1.  Use o `ALTER DATABASE` statement para habilitar o repositório de consultas. Por exemplo:  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
    ```  
  
     Para obter mais opções de sintaxe relacionadas ao repositório de consultas, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
> [!NOTE]  
>  Não é possível habilitar o repositório de consultas no banco de dados mestre.  
  

  
##  <a name="About"></a> Informações no Repositório de Consultas  
 Planos de execução para qualquer consulta específica no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] normalmente envolvem horas extras por vários motivos diferentes, como alterações de estatísticas, alterações de esquema, criação/exclusão de índices, etc. O cache de procedimento (no qual os planos de consulta em cache são armazenados) armazena apenas o plano de execução mais recente. Os planos também são removidos do cache do plano devido à pressão da memória. Como resultado, as regressões do desempenho de consulta causadas por alterações no plano de execução podem não ser triviais e podem ter resolução lenta.  
  
 Como o repositório de consultas mantém vários planos de execução por consulta, ele pode impor políticas para direcionar o processador de consultas para usar um plano de execução específico para uma consulta. Isso é conhecido como imposição de plano. A imposição de plano no repositório de consultas é fornecida usando um mecanismo semelhante à dica de consulta [USE PLAN](/sql/t-sql/queries/hints-transact-sql-query) , mas não requer nenhuma alteração nos aplicativos do usuário. A imposição de plano pode resolver uma regressão de desempenho de consulta causada por uma alteração do plano em um período muito curto.  
  
 Cenários comuns para o uso do recurso Repositório de Consultas são:  
  
-   Localizar e corrigir rapidamente uma regressão de desempenho do plano, forçando o plano de consulta anterior. Corrigir consultas com regressão recente no desempenho devido a alterações no plano de execução.  
  
-   Determinar o número de vezes que uma consulta foi executada em determinada janela de tempo, auxiliando um DBA na solução de problemas de recurso de desempenho.  
  
-   Identificar as principais consultas *n* (por tempo de execução, consumo de memória, etc.) nas últimas *x* horas.  
  
-   Fazer auditoria de histórico dos planos de consulta para determinada consulta.  
  
-   Analisar os padrões de uso dos recursos (CPU, E/S e memória) para determinado banco de dados.  
  
 O armazenamento de consultas contém dois repositórios; um **repositório de planos** para manter as informações do plano de execução e um **repositório de estatísticas de tempo de execução** para manter as informações de estatísticas de execução. O número de planos exclusivos que podem ser armazenadas para uma consulta no repositório de planos é limitada pela `max_plans_per_query` opção de configuração. Para melhorar o desempenho, as informações são gravadas nos dois repositórios de forma assíncrona. Para otimizar o uso do espaço, as estatísticas de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixa. As informações nesses repositórios são visíveis consultando as exibições de catálogo do repositório de consultas.  
  
 A consulta a seguir retorna informações sobre consultas e planos no repositório de consultas.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  

  
## <a name="using-the-regressed-queries-feature"></a>Usando o recurso de consultas regredidas  
 Depois de habilitar o repositório de consultas, atualize a parte do banco de dados do painel Pesquisador de Objetos para adicionar a seção **Repositório de Consultas** .  
  
 ![A QueryStore](../../database-engine/media/querystore.PNG "a QueryStore")  
  
 Selecionando **consultas Regredidas**, abre o **consultas Regredidas** painel no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]. O painel Consultas Regredidas mostra consultas e planos no repositório de consultas. Caixas de listas suspensas na parte superior permitem que você selecione consultas com base em vários critérios. Selecione um plano para ver o plano de consulta gráfico. Botões estão disponíveis para exibir a consulta de origem, impor e cancelar a imposição de um plano de consulta e atualizar a exibição.  
  
 ![RegressedQueries](../../database-engine/media/regressedqueries.PNG "RegressedQueries")  
  
 Para impor um plano, selecione uma consulta e um plano e, em seguida, clique em **Impor Plano.** Você pode impor apenas planos que foram salvos pelo recurso de plano de consulta e ainda são mantidos no cache do plano de consulta.  
  

  
##  <a name="Options"></a> Opções de configuração  
 OPERATION_MODE  
 Pode ser READ_WRITE ou READ_ONLY.  
  
 CLEANUP_POLICY  
 Configure o argumento STALE_QUERY_THRESHOLD_DAYS para especificar o número de dias que os dados devem ser mantidos no repositório de consultas.  
  
 DATA_FLUSH_INTERVAL_SECONDS  
 Determina a frequência na qual os dados gravados no repositório de consultas é persistida no disco. Para otimizar o desempenho, os dados coletados pelo repositório de consultas são gravados de maneira assíncrona no disco. A frequência em que essa transferência assíncrona ocorre é configurada via DATA_FLUSH_INTERVAL_SECONDS.  
  
 MAX_SIZE_MB  
 Configura o tamanho máximo do repositório de consultas. Se os dados no repositório de consultas atingir o limite MAX_SIZE_MB, o repositório de consultas alterará automaticamente o status de somente gravação para somente leitura e interromperá a coleta de novos dados.  
  
 INTERVAL_LENGTH_MINUTES  
 Determina o intervalo de tempo em que os dados de estatísticas de execução do tempo de execução são agregados no repositório de consultas. Para otimizar o uso de espaço, as estatísticas de execução de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixa. Essa janela de tempo fixa é configurada usando INTERVAL_LENGTH_MINUTES.  
  
 Consulta o `sys.database_query_store_options` modo de exibição para determinar as opções atuais do repositório de consultas.  
  
 Para obter mais informações sobre como definir opções usando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , consulte [Gerenciamento de opção](#OptionMgmt).  
  
 
  
##  <a name="Related"></a> Exibições, Funções e Procedimentos Relacionados  
 A Store consulta podem ser exibido e gerenciado por meio de [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] ou usando as exibições e os procedimentos a seguir.  
  
-   [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql)  
  
### <a name="query-store-catalog-views"></a>Exibições do catálogo de repositório de consulta  
 Sete exibições do catálogo apresentam informações sobre o repositório de consultas.  
  
-   [sys.database_query_store_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql)  
  
-   [sys.query_context_settings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-query-context-settings-transact-sql)  
  
-   [sys.query_store_plan &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-query-store-plan-transact-sql)  
  
-   [sys.query_store_query &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-query-store-query-transact-sql)  
  
-   [sys.query_store_query_text &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql)  
  
-   [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql)  
  
-   [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql)  
  
### <a name="query-store-stored-procedures"></a>Procedimentos armazenados do repositório de consulta  
 Seis procedimentos armazenados configuram o repositório de consultas.  
  
-   [sp_query_store_flush_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql)  
  
-   [sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql)  
  
-   [sp_query_store_force_plan &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql)  
  
-   [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql)  
  
-   [sp_query_store_remove_plan &#40;Transct-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql)  
  
-   [sp_query_store_remove_query &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql)  
  

  
##  <a name="Scenarios"></a> Principais cenários de uso  
  
###  <a name="OptionMgmt"></a> Gerenciamento de opção  
 Esta seção fornece algumas diretrizes sobre como gerenciar recursos do próprio repositório de consultas.  
  
 **O Repositório de Consultas está ativo no momento?**  
  
 O Repositório de Consultas armazena seus dados dentro do banco de dados do usuário e é por isso que ele tem limite de tamanho (configurado com `MAX_STORAGE_SIZE_MB`). Se os dados no repositório de consultas atingirem esse limite, o repositório de consultas alterará automaticamente o status de somente gravação para somente leitura e interromperá a coleta de novos dados.  
  
 Execute o script a seguir para determinar se o repositório de consultas está ativo no momento e se está coletando estatísticas de tempo de execução ou não.  
  
```  
DECLARE @x nvarchar(100) = CAST(newid() AS nvarchar(100));  
DECLARE @query nvarchar(max) =   
N'IF EXISTS  
(  
    SELECT *   
    FROM sys.query_store_query_text   
    WHERE query_sql_text LIKE ''%' + @x + N'%''  
)  
SELECT ''Query Store is active'' ;  
ELSE SELECT ''Query Store is NOT active''' ;  
EXEC sp_executesql @query;  
```  
  
 **Opções Obter Repositório de Consultas**  
  
 Para obter informações detalhadas sobre o status do repositório de consultas, execute o seguinte em um banco de dados do usuário.  
  
```  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **Configurar o intervalo do Repositório de Consultas**  
  
 Você pode substituir o intervalo para agregar estatísticas de tempo de execução de consulta (o padrão é 60 minutos).  
  
```  
  
      USE master;  
GO  
  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 Observe que não são permitidos valores arbitrários – você deve usar um dos seguintes: 1, 5, 10, 15, 30 e 60.  
  
 Novo valor do intervalo é exposto por meio de `sys.database_query_store_options` modo de exibição.  
  
 Se o armazenamento do repositório de consultas estiver completo, use a seguinte instrução para ampliar o armazenamento.  
  
```  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **Opções Obter Todos os Repositórios de Consultas**  
  
 Você pode definir várias opções de repositório de consultas de uma só vez com uma única instrução ALTER DATABASE.  
  
```  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY =   
    (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15  
);  
```  
  
 **Limpar o espaço**  
  
 Tabelas internas do repositório de consultas são criadas no grupo de arquivos PRIMARY durante a criação do banco de dados e essa configuração não pode ser alterada posteriormente. Se você estiver executando sem espaço, limpe os dados antigos do repositório de consultas usando a instrução a seguir.  
  
```  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 Você pode também limpar apenas dados de consulta ad hoc, pois são menos relevantes para otimizações de consulta e análise do plano, mas eles ocupam a mesma quantidade de espaço.  
  
 **Excluir consultas ad hoc** Isso exclui as consultas que só foram executadas uma vez e que têm mais de 24 horas.  
  
```  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 Você pode definir seu próprio procedimento com uma lógica diferente, para limpar os dados que não são mais importantes para você.  
  
 O exemplo acima usa o `sp_query_store_remove_query` procedimento armazenado para remover dados desnecessários. Você também pode usar dois outros procedimentos.  
  
-   `sp_query_store_reset_exec_stats` – Limpa as estatísticas de tempo de execução para um plano específico.  
  
-   `sp_query_store_remove_plan` – Remove um único plano.  
  

  
###  <a name="Peformance"></a> Auditoria e solução de problemas de desempenho  
 Como o repositório de consultas mantém o histórico de compilação e métricas do tempo de execução durante as execuções da consulta, há muitas questões diferentes que podem ser respondidas facilmente com relação à carga de trabalho.  
  
 **Última *n* consultas executadas no banco de dados.**  
  
```  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **Número de execuções de cada consulta.**  
  
```  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **O número de consultas com o tempo médio de execução mais longo na última hora.**  
  
```  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **Lê o número de consultas que tiveram a maior média física e/s nas últimas 24 horas, com a contagem de médio da linha correspondente e execução.**  
  
```  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **Consultas com vários planos.** Essas consultas são especialmente interessantes porque são candidatas a regressões em razão de alteração na escolha do plano. A consulta a seguir identifica essas consultas junto com todos os planos:  
  
```  
WITH Query_MultPlans  
AS  
(  
    SELECT COUNT(*) AS cnt, q.query_id   
    FROM sys.query_store_query_text AS qt  
    JOIN sys.query_store_query AS q  
        ON qt.query_text_id = q.query_text_id  
    JOIN sys.query_store_plan AS p  
        ON p.query_id = q.query_id  
    GROUP BY q.query_id  
    HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject, query_sql_text,  
plan_id, p.query_plan AS plan_xml,  
p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **Consultas com regressão recente de desempenho (comparando diferentes pontos no tempo).** O exemplo de consulta a seguir retorna todas as consultas para as quais o tempo de execução dobrou nas últimas 48 horas em razão de alteração na escolha do plano. A consulta compara todos os intervalos de estatísticas de tempo de execução lado a lado.  
  
```  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 Para ver todas as regressões de desempenho (não apenas as relacionadas a alteração na escolha do plano), basta remover a condição `AND p1.plan_id <> p2.plan_id` da consulta anterior.  
  
 **Consultas com regressão recente de desempenho (comparando execuções recentes e históricas).** A próxima consulta compara os períodos de execução baseados na execução da consulta. Nesse exemplo específico, a consulta compara a execução no período recente (1 hora) versus o período do histórico (último dia) e identifica as que introduziram additional_duration_workload. Essa métrica é calculada como uma diferença entre a média de execução recente e a média de execução do histórico, multiplicado pelo número de execuções recentes. Representa, na verdade, quanto de duração adicional as execuções recentes introduziram em comparação com histórico:  
  
```  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time <= @history_start_time AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time <= @history_end_time AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time <= @recent_start_time AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time <= @recent_end_time AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/recent.count_executions-hist.total_duration/hist.count_executions)*(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
  

  
###  <a name="Stability"></a> Manter a estabilidade do desempenho da consulta  
 Para consultas que são executadas várias vezes você pode perceber que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usou diferentes planos que resultaram em diferentes utilizações de recurso e duração. Com o repositório de consultas, você pode facilmente detectar quando o desempenho da consulta regrediu e determinar o plano ideal dentro de um período de interesse. Em seguida, você pode forçar o plano ideal para execução futura da consulta.  
  
 Você também pode identificar desempenho inconsistente de consulta para uma consulta com parâmetros ( autoparametrizada ou parametrizada manualmente). Entre diferentes planos, você pode identificar o plano que é rápido e ideal o suficiente para todos ou a maioria dos valores de parâmetro e forçar esse plano, mantendo desempenho previsível para o conjunto mais amplo de cenários de usuário.  
  
 **Impor um plano para uma consulta (aplicar política de imposição).** Quando um plano é forçado para determinada consulta, sempre que uma consulta é executada com o plano imposto.  
  
```  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 Ao usar `sp_query_store_force_plan` só pode impor planos registrados pelo Store consulta como um plano para a consulta. Em outras palavras, os únicos planos disponíveis para uma consulta são aqueles que já foram usados para executar Q1 enquanto o repositório de consultas estava ativo.  
  
 **Remover a imposição de plano de uma consulta.** Para depender novamente na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consultar otimizador para calcular o plano de consulta ideal, use `sp_query_store_unforce_plan` para impor o plano que foi selecionado para a consulta.  
  
```  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
  

  
## <a name="see-also"></a>Consulte também  
 [Monitorar e ajustar o desempenho](../performance/monitor-and-tune-for-performance.md)   
 [Ferramentas para monitoramento e ajuste de desempenho](../performance/performance-monitoring-and-tuning-tools.md)   
 [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [Monitor de Atividade](../performance-monitor/activity-monitor.md)  
  
  
