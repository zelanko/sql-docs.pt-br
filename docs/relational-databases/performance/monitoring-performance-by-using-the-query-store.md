---
title: "Monitorando o desempenho usando o Repositório de Consultas | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: aad94f116c1a8b668c9a218b32372424897a8b4a
ms.openlocfilehash: 53e0f5d479d7fc3cdeae2c6ce121734b6fc16f21
ms.contentlocale: pt-br
ms.lasthandoff: 06/28/2017

---
<a id="monitoring-performance-by-using-the-query-store" class="xliff"></a>

# Monitorar o desempenho usando o Repositório de Consultas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  O recurso Repositório de Consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece informações sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, ajudando você a identificar rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O Repositório de Consultas captura automaticamente um histórico das consultas, dos planos e das estatísticas de tempo de execução e os mantém para sua análise. Ele separa os dados por janelas por hora, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor. O repositório de consultas pode ser configurado usando a opção [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) . 
  
 Para obter informações sobre operar o Repositório de consultas no Banco de dados SQL do Azure, consulte [Operando o Repositório de Consultas no Banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/).  
  
##  <a name="Enabling"></a> Habilitando o Repositório de Consultas  
 O repositório de consultas não está ativo para novos bancos de dados por padrão.  
  
<a id="use-the-query-store-page-in-management-studio" class="xliff"></a>

#### Usar a página Repositório de Consultas no Management Studio  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um banco de dados e clique em **Propriedades**.  
  
    > [!NOTE]  
    >  Exige, no mínimo, a versão [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Na caixa de diálogo **Propriedades do Banco de Dados** , selecione a página **Repositório de Consultas** .  
  
3.  Na caixa **Modo de operação (Solicitado)** , selecione **Ativado**.  
  
<a id="use-transact-sql-statements" class="xliff"></a>

#### Usar Instruções Transact-SQL  
  
1.  Use a instrução **ALTER DATABASE** para habilitar o repositório de consultas. Por exemplo:  
  
    ```tsql  
    ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
    ```  
  
     Para obter mais opções de sintaxe relacionadas ao repositório de consultas, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
> [!NOTE]  
>  Não é possível habilitar o repositório de consultas no banco de dados **mestre** ou **tempdb** .  
 
##  <a name="About"></a> Informações no Repositório de Consultas  
 Planos de execução para qualquer consulta específica no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente envolvem horas extras por vários motivos diferentes, como alterações de estatísticas, alterações de esquema, criação/exclusão de índices, etc. O cache de procedimento (no qual os planos de consulta em cache são armazenados) armazena apenas o plano de execução mais recente. Os planos também são removidos do cache do plano devido à pressão da memória. Como resultado, as regressões do desempenho de consulta causadas por alterações no plano de execução podem não ser triviais e podem ter resolução lenta.  
  
 Como o repositório de consultas mantém vários planos de execução por consulta, ele pode impor políticas para direcionar o processador de consultas para usar um plano de execução específico para uma consulta. Isso é conhecido como imposição de plano. A imposição de plano no repositório de consultas é fornecida usando um mecanismo semelhante à dica de consulta [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) , mas não requer nenhuma alteração nos aplicativos do usuário. A imposição de plano pode resolver uma regressão de desempenho de consulta causada por uma alteração do plano em um período muito curto.  

 As **estatísticas de espera** são outra fonte de informações que ajudam a solucionar problemas de desempenho no SQL Server. Por muito tempo, as estatísticas de espera estavam disponíveis somente no nível da instância, o que tornava difícil refazer o caminho para a consulta real. No SQL Server 2017 e no Banco de Dados SQL do Azure adicionamos outra dimensão no Repositório de Consultas que controla as estatísticas de espera. 

 Cenários comuns para o uso do recurso Repositório de Consultas são:  
  
-   Localizar e corrigir rapidamente uma regressão de desempenho do plano, forçando o plano de consulta anterior. Corrigir consultas com regressão recente no desempenho devido a alterações no plano de execução.  
  
-   Determinar o número de vezes que uma consulta foi executada em determinada janela de tempo, auxiliando um DBA na solução de problemas de recurso de desempenho.  
  
-   Identificar as principais consultas *n* (por tempo de execução, consumo de memória, etc.) nas últimas *x* horas.  
  
-   Fazer auditoria de histórico dos planos de consulta para determinada consulta.  
  
-   Analisar os padrões de uso dos recursos (CPU, E/S e memória) para determinado banco de dados.  
-   Identifique as principais n consultas que estão esperando em recursos. 
-   Entenda a natureza de espera de um plano ou de uma consulta específica.
  
O Repositório de Consultas contém três repositórios:
- um **repositório de plano** para manter as informações de plano de execução
- um **repositório de estatísticas de tempo de execução** para manter as informações de estatísticas de execução. 
- um **repositório de estatísticas de espera** para manter as informações de estatísticas de espera.
 
 O número de planos exclusivos que pode ser armazenado para uma consulta no repositório de planos é limitado pela opção de configuração **max_plans_per_query** . Para melhorar o desempenho, as informações são gravadas nos dois repositórios de forma assíncrona. Para otimizar o uso do espaço, as estatísticas de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixa. As informações nesses repositórios são visíveis consultando as exibições de catálogo do repositório de consultas.  
  
 A consulta a seguir retorna informações sobre consultas e planos no repositório de consultas.  
  
```tsql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
##  <a name="Regressed"></a> Usar o recurso Consultas Regredidas  
 Depois de habilitar o repositório de consultas, atualize a parte do banco de dados do painel Pesquisador de Objetos para adicionar a seção **Repositório de Consultas** .  
  
 ![Árvore do repositório de consulta no Pesquisador de Objetos](../../relational-databases/performance/media/objectexplorerquerystore.PNG "Árvore do repositório de consulta no Pesquisador de Objetos")  
  
 Selecione **Consultas Regredidas** para abrir o painel **Consultas Regredidas** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. O painel Consultas Regredidas mostra consultas e planos no repositório de consultas. Use as caixas de listas suspensas na parte superior para selecionar consultas com base em vários critérios. Selecione um plano para ver o plano de consulta gráfico. Botões estão disponíveis para exibir a consulta de origem, impor e cancelar a imposição de um plano de consulta e atualizar a exibição.  
  
 ![Consultas regressadas no Pesquisador de Objetos](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "Consultas regressadas no Pesquisador de Objetos")  
  
 Para impor um plano, selecione uma consulta e um plano e, em seguida, clique em **Impor Plano.** Você pode impor apenas planos que foram salvos pelo recurso de plano de consulta e ainda são mantidos no cache do plano de consulta.  
##  <a name="Waiting"></a> Localizando consultas de espera

A partir do SQL Server 2017 CTP 2.0 e do Banco de Dados SQL do Azure, as estatísticas de espera por consulta estão disponíveis para clientes do Repositório de Consultas. No Repositório de Consultas os tipos de espera são combinados em **categorias de espera**. O mapeamento completo está disponível aqui [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)

As **categorias de espera** combinam tipos diferentes de espera em buckets semelhantes por natureza. Categorias de espera diferentes exigem um acompanhamento de análise diferente para resolver o problema, mas os tipos de espera da mesma categoria levam a experiências de solução de problemas muito semelhantes e fornecer a consulta afetada com base nas esperas seria a peça que faltava para concluir a maioria dessas investigações de com êxito.

Aqui estão alguns exemplos de como você pode obter mais informações sobre sua carga de trabalho antes e depois de introduzir as categorias de espera no Repositório de Consultas:

|||| 
|-|-|-|  
|Experiência anterior|Nova experiência|Ação|
|RESOURCE_SEMAPHORE alto de esperas por banco de dados|Esperas de memória alta no Repositório de Consultas para consultas específicas|Localize as consultas com maior consumo de memória no Repositório de Consultas. Essas consultas estão provavelmente atrasando o andamento das consultas afetadas. Considere usar a dica de consulta MAX_GRANT_PERCENT para essas consultas ou para as consultas afetadas.|
|Espera de LCK_M_X alta por banco de dados|Esperas de bloqueio altas no Repositório de Consultas para consultas específicas|Verifique os textos de consulta das consultas afetadas e identifique as entidades de destino. Pesquise outras consultas no Repositório de Consultas que modificam a mesma entidade, que são executadas com frequência e/ou têm alta duração. Depois de identificar essas consultas, considere alterar a lógica do aplicativo para melhorar a simultaneidade ou use um nível de isolamento menos restritivo.|
|Esperas de PAGEIOLATCH_SH altas por banco de dados|Esperas de buffer de E/S altas no Repositório de Consultas para consultas específicas|Localize as consultas com um grande número de leituras físicas no Repositório de Consultas. Se elas corresponderem às consultas com esperas de E/S, considere introduzir um índice na entidade subjacente, para fazer buscas em vez de verificações e, portanto, minimizar a sobrecarga de E/S das consultas.|
|Esperas de SOS_SCHEDULER_YIELD altas por banco de dados|Esperas de CPU altas no Repositório de Consultas para consultas específicas|Localize as consultas com maior consumo de CPU no Repositório de Consultas. Entre elas, identifique as consultas para as quais a tendência de CPU alta se correlaciona às esperas de CPU altas para as consultas afetadas. Concentre-se em otimizar essas consultas – poderia haver uma regressão de plano ou talvez um índice ausente.| 
##  <a name="Options"></a> Opções de configuração 

As seguintes opções estão disponíveis para configurar parâmetros de repositório de consulta.

 `OPERATION_MODE`  
 Pode ser READ_WRITE (padrão) ou READ_ONLY.  
  
 `CLEANUP_POLICY (STALE_QUERY_THRESHOLD_DAYS)`  
 Configure o argumento STALE_QUERY_THRESHOLD_DAYS para especificar o número de dias que os dados devem ser mantidos no repositório de consultas. O valor padrão é 30. Para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition, o padrão é 7 dias.
  
 `DATA_FLUSH_INTERVAL_SECONDS`  
 Determina a frequência na qual os dados gravados no repositório de consultas é persistida no disco. Para otimizar o desempenho, os dados coletados pelo repositório de consultas são gravados de maneira assíncrona no disco. A frequência em que essa transferência assíncrona ocorre é configurada via DATA_FLUSH_INTERVAL_SECONDS. O valor padrão é 900 (15 min).  
  
 `MAX_STORAGE_SIZE_MB`  
 Configura o tamanho máximo do repositório de consultas. Se os dados no repositório de consultas atingir o limite MAX_STORAGE_SIZE_MB, o repositório de consultas alterará automaticamente o status de somente gravação para somente leitura e interromperá a coleta de novos dados.  O valor padrão é 100 Mb. Para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition, o padrão é 1 Gb e, para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition, o padrão é 10 Mb.
  
 `INTERVAL_LENGTH_MINUTES`  
 Determina o intervalo de tempo em que os dados de estatísticas de execução do tempo de execução são agregados no repositório de consultas. Para otimizar o uso de espaço, as estatísticas de execução de tempo de execução no repositório de estatísticas de tempo de execução são agregadas em uma janela de tempo fixa. Essa janela de tempo fixa é configurada usando INTERVAL_LENGTH_MINUTES. O valor padrão é 60. 
  
 `SIZE_BASED_CLEANUP_MODE`  
 Controla se o processo de limpeza será ativado automaticamente quando o volume total de dados se aproximar do tamanho máximo. Pode ser AUTO (padrão) ou OFF.  
  
 `QUERY_CAPTURE_MODE`  
 Indica se o Repositório de Consultas captura todas as consultas ou consultas relevantes com base no consumo de recursos e na contagem de execuções, ou se ele para de adicionar novas consultas e rastreia apenas as consultas atuais. Pode ser ALL (capturar todas as consultas), AUTO (ignorar incomum e consultas com duração de compilação e execução insignificante) ou NONE (parar de capturar novas consultas). O valor padrão no SQL Server 2016 é ALL, enquanto no Banco de dados SQL do Azure é AUTO.
  
 `MAX_PLANS_PER_QUERY`  
 Um número inteiro que representa a quantidade máxima de planos de manutenção para cada consulta. O valor padrão é 200.  
 
 `WAIT_STATS_CAPTURE_MODE`  
 Controla se o repositório de consultas captura informações de estatísticas de espera. Pode ser OFF = 0 ou em = 1 (padrão)  
 
 Consulte a exibição **sys.database_query_store_options** para determinar as opções atuais do repositório de consultas. Para obter mais informações sobre os valores, consulte [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
 Para obter mais informações sobre como definir opções usando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , consulte [Gerenciamento de opção](#OptionMgmt).  
  
##  <a name="Related"></a> Exibições, Funções e Procedimentos Relacionados  
 Exiba e gerencie o Repositório de Consultas por meio do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou usando as exibições e os procedimentos a seguir.  

||| 
|-|-|  
|[sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)|| 
  
<a id="query-store-catalog-views" class="xliff"></a>

### Exibições do catálogo de repositório de consulta  
 As exibições do catálogo apresentam informações sobre o Repositório de Consultas.  

||| 
|-|-|  
|[sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)|[sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)|  
|[sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)|[sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)|  
|[sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|[sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)|  
|[sys.query_store_wait_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)|[sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)|  
  
<a id="query-store-stored-procedures" class="xliff"></a>

### Procedimentos armazenados do repositório de consulta  
 Os procedimentos armazenados configuram o Repositório de Consultas.  

||| 
|-|-|  
|[sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)|[sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)|  
|[sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)|[sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)|  
|[sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)|[sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)|  
 
##  <a name="Scenarios"></a> Principais cenários de uso  
  
###  <a name="OptionMgmt"></a> Gerenciamento de opção  
 Esta seção fornece algumas diretrizes sobre como gerenciar recursos do próprio repositório de consultas.  
  
 **O Repositório de Consultas está ativo no momento?**  
  
 O Repositório de Consultas armazena seus dados dentro do banco de dados do usuário e é por isso que ele tem limite de tamanho (configurado com `MAX_STORAGE_SIZE_MB`). Se os dados no repositório de consultas atingirem esse limite, o repositório de consultas alterará automaticamente o status de somente gravação para somente leitura e interromperá a coleta de novos dados.  
  
 Consulte [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para determinar se o Repositório de Consultas está ativo no momento e se está coletando estatísticas de tempo de execução ou não.  
  
```tsql  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 O status do Repositório de Consultas é determinado pela coluna actual_state. Caso não seja o status desejado, a coluna `readonly_reason` pode fornecer mais informações.   
Quando o tamanho do Repositório de Consultas exceder a cota, o recurso passará para o modo de readon_only.  
  
 **Opções Obter Repositório de Consultas**  
  
 Para obter informações detalhadas sobre o status do repositório de consultas, execute o seguinte em um banco de dados do usuário.  
  
```tsql  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **Configurar o intervalo do Repositório de Consultas**  
  
 Você pode substituir o intervalo para agregar estatísticas de tempo de execução de consulta (o padrão é 60 minutos).  
  
```tsql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 > [!NOTE]
 > Não são permitidos valores arbitrários para `INTERVAL_LENGTH_MINUTES`. Use um dos seguintes: 1, 5, 10, 15, 30, 60 ou 1440 minutos.  
  
 O novo valor do intervalo é exposto por meio da exibição **sys.database_query_store_options** .  
  
 **Uso de espaço do Repositório de Consultas**  
  
 Para verificar o tamanho atual e o limite do Repositório de Consultas, execute a instrução a seguir no banco de dados do usuário.  
  
```tsql  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 Se o armazenamento do repositório de consultas estiver completo, use a seguinte instrução para ampliar o armazenamento.  
  
```tsql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **Opções Obter Todos os Repositórios de Consultas**  
  
 Você pode definir várias opções de repositório de consultas de uma só vez com uma única instrução ALTER DATABASE.  
  
```tsql  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000,
    WAIT_STATS_CAPTURE_MODE = ON 
);  
```  
  
 **Limpar o espaço**  
  
 Tabelas internas do repositório de consultas são criadas no grupo de arquivos PRIMARY durante a criação do banco de dados e essa configuração não pode ser alterada posteriormente. Se você estiver executando sem espaço, limpe os dados antigos do repositório de consultas usando a instrução a seguir.  
  
```tsql  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 Você pode também limpar apenas dados de consulta ad hoc, pois são menos relevantes para otimizações de consulta e análise do plano, mas eles ocupam a mesma quantidade de espaço.  
  
 **Excluir consultas ad hoc** Isso exclui as consultas que só foram executadas uma vez e que têm mais de 24 horas.  
  
```tsql  
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
  
 Você pode definir seu próprio procedimento com uma lógica diferente para limpar os dados que não são mais necessários.  
  
 O exemplo acima usa o procedimento armazenado estendido **sp_query_store_remove_query** para remover dados desnecessários. Você também pode usar:  
  
-   **sp_query_store_reset_exec_stats** – para limpar as estatísticas de tempo de execução para um plano específico.  
  
-   **sp_query_store_remove_plan** – para remover um único plano.  
 
  
###  <a name="Peformance"></a> Auditoria e solução de problemas de desempenho  
 O Repositório de Consultas mantém um histórico das métricas de compilação e de tempo de execução durante as execuções de consulta, permitindo que você faça perguntas sobre sua carga de trabalho.  
  
 **Últimas *n* consultas executadas no banco de dados?**  
  
```tsql  
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
  
 **Número de execuções de cada consulta?**  
  
```tsql  
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
  
 **O número de consultas com o tempo médio de execução mais longo na última hora?**  
  
```tsql  
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
  
 **O número de consultas que tiveram a maior média de leituras físicas de E/S nas últimas 24 horas, com a média de contagem de linha e execução correspondente?**  
  
```tsql  
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
  
 **Consultas com vários planos?** Essas consultas são especialmente interessantes porque são candidatas a regressões em razão de alteração na escolha do plano. A consulta a seguir identifica essas consultas junto com todos os planos:  
  
```tsql  
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
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
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
  
 **Consultas com regressão recente de desempenho (comparando diferentes pontos no tempo)?** O exemplo de consulta a seguir retorna todas as consultas para as quais o tempo de execução dobrou nas últimas 48 horas em razão de alteração na escolha do plano. A consulta compara todos os intervalos de estatísticas de tempo de execução lado a lado.  
  
```tsql  
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

 **Consultas que estão aguardando mais?**
 Essa consulta retornará as dez principais consultas que mais esperam. 
 
 ```tsql 
  SELECT TOP 10
    qt.query_text_id,
    q.query_id,
    p.plan_id,
    sum(total_query_wait_time_ms) AS sum_total_wait_ms
FROM sys.query_store_wait_stats ws
JOIN sys.query_store_plan p ON ws.plan_id = p.plan_id
JOIN sys.query_store_query q ON p.query_id = q.query_id
JOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_id
GROUP BY qt.query_text_id, q.query_id, p.plan_id
ORDER BY sum_total_wait_ms DESC
 ```
 
 **Consultas com regressão recente de desempenho (comparando execuções recentes e históricas)?** A próxima consulta compara os períodos de execução baseados na execução da consulta. Nesse exemplo específico, a consulta compara a execução no período recente (uma hora) com o período do histórico (último dia) e identifica as que introduziram o `additional_duration_workload`. Essa métrica é calculada como uma diferença entre a média de execução recente e a média de execução do histórico, multiplicado pelo número de execuções recentes. Representa, na verdade, quanto de duração adicional as execuções recentes introduziram em comparação com histórico:  
  
```tsql  
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
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time \<= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time \<= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
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
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time \<= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time \<= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
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
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
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
 Para consultas executadas várias vezes, você pode perceber que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa diferentes planos, resultando em diferentes utilizações de recurso e duração. Com o Repositório de Consultas, você pode detectar quando o desempenho da consulta regrediu e determinar o plano ideal dentro de um período de interesse. Em seguida, você pode impor esse plano ideal para execução futura da consulta.  
  
 Você também pode identificar desempenho inconsistente de consulta para uma consulta com parâmetros ( autoparametrizada ou parametrizada manualmente). Entre diferentes planos, você pode identificar o plano que é rápido e ideal o suficiente para todos ou a maioria dos valores de parâmetro e impor esse plano, mantendo desempenho previsível para o conjunto mais amplo de cenários de usuário.  
  
 **Impor um plano para uma consulta (aplicar política de imposição).** Quando um plano é forçado para determinada consulta, sempre que uma consulta é executada com o plano imposto.  
  
```tsql  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 Ao usar **sp_query_store_force_plan** você só pode impor planos registrados pelo repositório de consultas como um plano para essa consulta. Em outras palavras, os únicos planos disponíveis para uma consulta são aqueles que já foram usados para executar essa consulta enquanto o Repositório de Consultas estava ativo.  
  
 **Remover a imposição de plano de uma consulta.** Para depender novamente no otimizador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para calcular o plano de consulta ideal, use **sp_query_store_unforce_plan** para cancelar a imposição do plano selecionado para a consulta.  
  
```tsql  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
  
<a id="see-also" class="xliff"></a>

## Consulte também  
 [Prática recomendada com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Usar o Repositório de Consultas com OLTP na memória](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Cenários de uso do Repositório de Consultas](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [Como o Repositório de Consultas coleta dados](../../relational-databases/performance/how-query-store-collects-data.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Exibições de Catálogo do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)   
 [Monitor de atividade](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [Operar o Repositório de Consultas no banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  

