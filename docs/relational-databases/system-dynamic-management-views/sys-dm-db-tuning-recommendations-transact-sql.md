---
title: sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: Saiba como encontrar possíveis problemas de desempenho e correções recomendadas no SQL Server e no banco de dados SQL do Azure
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: adf2a1eb88397acbbc8e092eb320e15f239ae8f2
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834527"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>\_ \_ \_ recomendações de ajuste do sys.dm dB (Transact-SQL)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  Retorna informações detalhadas sobre as recomendações de ajuste.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.

| **Nome da coluna** | **Data type** | **Descrição** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome exclusivo da recomendação. |
| **type** | **nvarchar(4000)** | O nome da opção de ajuste automático que produziu a recomendação, por exemplo, `FORCE_LAST_GOOD_PLAN` |
| **motivo** | **nvarchar(4000)** | Motivo pelo qual essa recomendação foi fornecida. |
| **válido \_ desde** | **datetime2** | Na primeira vez em que essa recomendação foi gerada. |
| **última \_ atualização** | **datetime2** | A última vez em que essa recomendação foi gerada. |
| **state** | **nvarchar(4000)** | Documento JSON que descreve o estado da recomendação. Os campos a seguir estão disponíveis:<br />-   `currentValue` -estado atual da recomendação.<br />-   `reason` – constante que descreve por que a recomendação está no estado atual.|
| **é \_ \_ ação executável** | **bit** | 1 = a recomendação pode ser executada no banco de dados via [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script.<br />0 = a recomendação não pode ser executada no banco de dados (por exemplo: somente informações ou recomendação revertida) |
| **é \_ ação revertida \_** | **bit** | 1 = a recomendação pode ser monitorada e revertida automaticamente pelo mecanismo de banco de dados.<br />0 = a recomendação não pode ser monitorada e revertida automaticamente. A maioria das &quot; ações executáveis &quot; será &quot; revertida &quot; . |
| **executar \_ a \_ hora de início da ação \_** | **datetime2** | Data em que a recomendação é aplicada. |
| **\_duração da ação de execução \_** | **time** | Duração da ação de execução. |
| **executar \_ ação \_ iniciada \_ por** | **nvarchar(4000)** | `User` = O usuário forçou manualmente o plano na recomendação. <br /> `System` = O sistema aplicou automaticamente a recomendação. |
| **\_ \_ tempo iniciado da ação de execução \_** | **datetime2** | Data em que a recomendação foi aplicada. |
| **reverter \_ \_ hora de início da ação \_** | **datetime2** | Data em que a recomendação foi revertida. |
| **reverter \_ duração da ação \_** | **time** | Duração da ação de reversão. |
| **reverter \_ ação \_ iniciada \_ por** | **nvarchar(4000)** | `User` = O plano recomendado pelo usuário não foi forçado manualmente. <br /> `System` = O sistema reverteu a recomendação automaticamente. |
| **reverter \_ \_ hora iniciada da ação \_** | **datetime2** | Data em que a recomendação foi revertida. |
| **placar** | **int** | Valor/impacto estimado para essa recomendação na escala de 0-100 (maior é o melhor) |
| **Ver** | **nvarchar(max)** | Documento JSON que contém mais detalhes sobre a recomendação. Os campos a seguir estão disponíveis:<br /><br />`planForceDetails`<br />-    `queryId` - \_ ID de consulta da consulta regressiva.<br />-    `regressedPlanId` -plan_id do plano regressivo.<br />-   `regressedPlanExecutionCount` -Número de execuções da consulta com o plano regressivo antes de a regressão ser detectada.<br />-    `regressedPlanAbortedCount` -Número de erros detectados durante a execução do plano regressivo.<br />-    `regressedPlanCpuTimeAverage` -Tempo médio de CPU (em micro segundos) consumido pela consulta regressiva antes de a regressão ser detectada.<br />-    `regressedPlanCpuTimeStddev` -Desvio padrão do tempo de CPU consumido pela consulta regressiva antes de a regressão ser detectada.<br />-    `recommendedPlanId` -plan_id do plano que deve ser forçado.<br />-   `recommendedPlanExecutionCount`-Número de execuções da consulta com o plano que deve ser forçado antes que a regressão seja detectada.<br />-    `recommendedPlanAbortedCount` -Número de erros detectados durante a execução do plano que deve ser forçado.<br />-    `recommendedPlanCpuTimeAverage` -Tempo médio de CPU (em micro segundos) consumido pela consulta executada com o plano que deve ser forçado (calculado antes da detecção da regressão).<br />-    `recommendedPlanCpuTimeStddev` Desvio padrão do tempo de CPU consumido pela consulta regressiva antes de a regressão ser detectada.<br /><br />`implementationDetails`<br />-  `method` -O método que deve ser usado para corrigir a regressão. O valor é sempre `TSql` .<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script que deve ser executado para forçar o plano recomendado. |
  
## <a name="remarks"></a>Comentários  
 As informações retornadas pelo `sys.dm_db_tuning_recommendations` são atualizadas quando o mecanismo de banco de dados identifica a possível regressão de desempenho de consulta e não é persistente. As recomendações são mantidas somente até que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja reiniciado. Os administradores de banco de dados devem fazer cópias de backup da recomendação de ajuste periodicamente se desejarem mantê-lo após a reciclagem do servidor. 

 `currentValue` o campo na `state` coluna pode ter os seguintes valores:
 
 | Status | Descrição |
 |--------|-------------|
 | `Active` | A recomendação está ativa e ainda não foi aplicada. O usuário pode usar o script de recomendação e executá-lo manualmente. |
 | `Verifying` | A recomendação é aplicada pelo [!INCLUDE[ssde_md](../../includes/ssde_md.md)] e o processo de verificação interno compara o desempenho do plano forçado com o plano regressivo. |
 | `Success` | A recomendação foi aplicada com êxito. |
 | `Reverted` | A recomendação é revertida porque não há ganhos de desempenho significativos. |
 | `Expired` | A recomendação expirou e não pode mais ser aplicada. |

O documento JSON na `state` coluna contém o motivo que descreve por que é a recomendação no estado atual. Os valores no campo de motivo podem ser: 

| Motivo | Descrição |
|--------|-------------|
| `SchemaChanged` | A recomendação expirou porque o esquema de uma tabela referenciada foi alterado. A nova recomendação será criada se uma nova regressão do plano de consulta for detectada no novo esquema. |
| `StatisticsChanged`| A recomendação expirou devido à alteração de estatística em uma tabela referenciada. A nova recomendação será criada se uma nova regressão do plano de consulta for detectada com base em novas estatísticas. |
| `ForcingFailed` | O plano recomendado não pode ser forçado em uma consulta. Localize o `last_force_failure_reason` na exibição [Sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) para localizar o motivo da falha. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` a opção é desabilitada pelo usuário durante o processo de verificação. Habilite `FORCE_LAST_GOOD_PLAN` a opção usando [ALTER DATABASE SET AUTOMATIC_TUNING &#40;instrução TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) ou force o plano manualmente usando o script na `[details]` coluna. |
| `UnsupportedStatementType` | O plano não pode ser forçado na consulta. Exemplos de consultas sem suporte são cursores e `INSERT BULK` instruções. |
| `LastGoodPlanForced` | A recomendação foi aplicada com êxito. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] regressão de desempenho potencial identificada, mas a `FORCE_LAST_GOOD_PLAN` opção não está habilitada-consulte [ALTER DATABASE SET AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplique a recomendação manualmente ou habilite a `FORCE_LAST_GOOD_PLAN` opção. |
| `VerificationAborted`| O processo de verificação foi anulado devido à reinicialização ou Repositório de Consultas limpeza. |
| `VerificationForcedQueryRecompile`| A consulta é recompilada porque não há uma melhoria significativa no desempenho. |
| `PlanForcedByUser`| O usuário forçou manualmente o plano usando [sp_query_store_force_plan &#40;procedimento de&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) . O mecanismo de banco de dados não aplicará a recomendação se o usuário decidir explicitamente forçar algum plano. |
| `PlanUnforcedByUser` | O usuário não impô manualmente o plano usando [sp_query_store_unforce_plan &#40;procedimento de&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) . Como o usuário reverteu explicitamente o plano recomendado, o mecanismo de banco de dados continuará usando o plano atual e gerará uma nova recomendação se ocorrer alguma regressão do plano no futuro. |

 A estatística na coluna de detalhes não mostra as estatísticas do plano de tempo de execução (por exemplo, o tempo de CPU atual). Os detalhes de recomendação são obtidos no momento da detecção de regressão e descrevem por que a [!INCLUDE[ssde_md](../../includes/ssde_md.md)] regressão de desempenho identificada. Use `regressedPlanId` e `recommendedPlanId` para consultar [repositório de consultas exibições de catálogo](../../relational-databases/performance/how-query-store-collects-data.md) para localizar as estatísticas exatas do plano de tempo de execução.

## <a name="examples-of-using-tuning-recommendations-information"></a>Exemplos de como usar informações de recomendações de ajuste  

### <a name="example-1"></a>Exemplo 1
O seguinte Obtém o [!INCLUDE[tsql](../../includes/tsql-md.md)] script gerado que força um bom plano para qualquer consulta específica:  
 
```sql
SELECT name, reason, score,
    JSON_VALUE(details, '$.implementationDetails.script') AS script,
    details.* 
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON(details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressed_plan_id int '$.regressedPlanId',
            last_good_plan_id int '$.recommendedPlanId') AS details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active';
```
### <a name="example-2"></a>Exemplo 2
O seguinte Obtém o [!INCLUDE[tsql](../../includes/tsql-md.md)] script gerado que força um bom plano para qualquer consulta específica e informações adicionais sobre o lucro estimado:

```sql
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

### <a name="example-3"></a>Exemplo 3
Veja a seguir o [!INCLUDE[tsql](../../includes/tsql-md.md)] script gerado que força um bom plano para qualquer consulta específica e informações adicionais que incluam o texto da consulta e os planos de consulta armazenados no repositório de consultas:

```sql
WITH cte_db_tuning_recommendations
AS (SELECT reason,
        score,
        query_id,
        regressedPlanId,
        recommendedPlanId,
        current_state = JSON_VALUE(state, '$.currentValue'),
        current_state_reason = JSON_VALUE(state, '$.reason'),
        script = JSON_VALUE(details, '$.implementationDetails.script'),
        estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
        error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
    FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(Details, '$.planForceDetails')
    WITH ([query_id] int '$.queryId',
        regressedPlanId int '$.regressedPlanId',
        recommendedPlanId int '$.recommendedPlanId',
        regressedPlanErrorCount int,    
        recommendedPlanErrorCount int,
        regressedPlanExecutionCount int,
        regressedPlanCpuTimeAverage float,
        recommendedPlanExecutionCount int,
        recommendedPlanCpuTimeAverage float
        )
    )
SELECT qsq.query_id,
    qsqt.query_sql_text,
    dtr.*,
    CAST(rp.query_plan AS XML) AS RegressedPlan,
    CAST(sp.query_plan AS XML) AS SuggestedPlan
FROM cte_db_tuning_recommendations AS dtr
INNER JOIN sys.query_store_plan AS rp ON rp.query_id = dtr.query_id
    AND rp.plan_id = dtr.regressedPlanId
INNER JOIN sys.query_store_plan AS sp ON sp.query_id = dtr.query_id
    AND sp.plan_id = dtr.recommendedPlanId
INNER JOIN sys.query_store_query AS qsq ON qsq.query_id = rp.query_id
INNER JOIN sys.query_store_query_text AS qsqt ON qsqt.query_text_id = qsq.query_text_id;
```

Para obter mais informações sobre as funções JSON que podem ser usadas para consultar valores no modo de exibição de recomendação, consulte [suporte a JSON](../json/json-data-sql-server.md) no [!INCLUDE[ssde_md](../../includes/ssde_md.md)] .
  
## <a name="permissions"></a>Permissões  

Requer `VIEW SERVER STATE` permissão no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] .   
Requer a `VIEW DATABASE STATE` permissão para o banco de dados no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .   

## <a name="see-also"></a>Consulte Também  
 [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [&#41;&#40;Transact-SQL de sys.database_automatic_tuning_options ](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.database_query_store_options ](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Suporte a JSON](../json/json-data-sql-server.md)
