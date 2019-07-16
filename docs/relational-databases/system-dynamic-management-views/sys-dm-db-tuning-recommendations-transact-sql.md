---
title: sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: Saiba como localizar possíveis problemas de desempenho e recomendações de correção no SQL Server e banco de dados SQL
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
ms.openlocfilehash: dbee7422bdf58d753c31c7aa57a81bc4b29d2568
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096231"
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.DM\_db\_ajuste\_recomendações (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Retorna informações detalhadas sobre recomendações de ajuste.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém dados que não pertencem ao locatário conectado será filtrada.

| **Nome da coluna** | **Data type** | **Descrição** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome exclusivo da recomendação. |
| **type** | **nvarchar(4000)** | O nome da opção de ajuste automático que produziu a recomendação, por exemplo, `FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Motivo por que essa recomendação foi fornecida. |
| **valid\_since** | **datetime2** | Na primeira vez em que essa recomendação foi gerada. |
| **última\_atualizar** | **datetime2** | A última vez em que essa recomendação foi gerada. |
| **state** | **nvarchar(4000)** | Documento JSON que descreve o estado da recomendação. Campos a seguir estão disponíveis:<br />-   `currentValue` -estado atual da recomendação.<br />-   `reason` -constante que descreve por que a recomendação está no estado atual.|
| **está\_executável\_ação** | **bit** | 1 = a recomendação pode ser executada no banco de dados por meio de [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script.<br />0 = a recomendação não pode ser executada no banco de dados (por exemplo: recomendação de apenas ou revertido de informações) |
| **está\_revertable\_ação** | **bit** | 1 = a recomendação pode ser monitorada e revertida pelo mecanismo de banco de dados automaticamente.<br />0 = a recomendação não pode ser monitorada e revertida automaticamente. A maioria dos &quot;executável&quot; ações serão &quot;revertable&quot;. |
| **Execute\_ação\_iniciar\_tempo** | **datetime2** | Data em que a recomendação é aplicada. |
| **Execute\_ação\_duração** | **time** | Duração da ação executar. |
| **Execute\_ação\_iniciado\_por** | **nvarchar(4000)** | `User` = Usuário forçados manualmente o plano na recomendação. <br /> `System` = Sistema aplicada automaticamente a recomendação. |
| **Execute\_ação\_iniciado\_tempo** | **datetime2** | Data em que a recomendação foi aplicada. |
| **Reverter\_ação\_iniciar\_tempo** | **datetime2** | Data em que a recomendação foi revertida. |
| **revert\_action\_duration** | **time** | Duração da ação de reversão. |
| **Reverter\_ação\_iniciado\_por** | **nvarchar(4000)** | `User` = Plano recomendado manualmente de usuário. <br /> `System` = O sistema automaticamente revertida recomendação. |
| **Reverter\_ação\_iniciado\_tempo** | **datetime2** | Data em que a recomendação foi revertida. |
| **score** | **int** | Estimado de valor/impacto dessa recomendação sobre o valor de 0 a 100 escala (quanto maior o melhor) |
| **Detalhes** | **nvarchar(max)** | Documento JSON que contém mais detalhes sobre a recomendação. Campos a seguir estão disponíveis:<br /><br />`planForceDetails`<br />-    `queryId` -consulta\_id da consulta regredida.<br />-    `regressedPlanId` -plan_id do plano regredido.<br />-   `regressedPlanExecutionCount` – O número de execuções da consulta com o plano regredido antes da regressão é detectado.<br />-    `regressedPlanAbortedCount` – O número de erros detectados durante a execução do plano retornado.<br />-    `regressedPlanCpuTimeAverage` -Tempo médio de CPU consumido pela consulta retornada antes que a regressão é detectada.<br />-    `regressedPlanCpuTimeStddev` -Desvio padrão de tempo de CPU consumido pela consulta retornada antes da regressão é detectado.<br />-    `recommendedPlanId` -plan_id do plano que deve ser forçado.<br />-   `recommendedPlanExecutionCount`– O número de execuções da consulta com o plano que deve ser forçado antes que a regressão é detectada.<br />-    `recommendedPlanAbortedCount` – O número de erros detectados durante a execução do plano que deve ser forçado.<br />-    `recommendedPlanCpuTimeAverage` -Tempo médio de CPU consumido pela consulta executada com o plano deve ser forçado (calculado antes que a regressão é detectada).<br />-    `recommendedPlanCpuTimeStddev` Desvio padrão de tempo de CPU consumido pela consulta retornada antes da regressão é detectado.<br /><br />`implementationDetails`<br />-  `method` -O método que deve ser usado para corrigir a regressão. Valor é sempre `TSql`.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] script que deve ser executado para forçar o plano recomendado. |
  
## <a name="remarks"></a>Comentários  
 Informações retornadas por `sys.dm_db_tuning_recommendations` é atualizada quando o mecanismo de banco de dados identifica potenciais regressão de desempenho de consulta e não é persistente. As recomendações são mantidas apenas até [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de recomendação de ajuste se quiserem mantê-lo após a reciclagem do servidor. 

 `currentValue` campo de `state` coluna pode ter os seguintes valores:
 
 | Status | Descrição |
 |--------|-------------|
 | `Active` | Recomendação estiver ativo e aplicada não ainda. Usuário pode tirar o script de recomendação e executá-lo manualmente. |
 | `Verifying` | A recomendação é aplicada por [!INCLUDE[ssde_md](../../includes/ssde_md.md)] e o processo de verificação interno compara o desempenho do plano forçado com o plano regredido. |
 | `Success` | A recomendação é aplicada com êxito. |
 | `Reverted` | A recomendação é revertida porque não há nenhum ganhos significativos de desempenho. |
 | `Expired` | Recomendação expirou e não pode ser aplicada mais. |

Documento JSON na `state` coluna contém o motivo que descreve por que é a recomendação no estado atual. Valores do campo motivo podem ser: 

| Reason | Descrição |
|--------|-------------|
| `SchemaChanged` | Recomendação expirou porque o esquema de uma tabela referenciado é alterado. |
| `StatisticsChanged`| Recomendação expirou devido à alteração de estatística em uma tabela referenciada. |
| `ForcingFailed` | Plano recomendado não pode ser forçado em uma consulta. Localizar o `last_force_failure_reason` no [query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) exibição para descobrir o motivo da falha. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` opção está desabilitada pelo usuário durante o processo de verificação. Habilitar `FORCE_LAST_GOOD_PLAN` usando a opção [ALTER AUTOMATIC_TUNING definido do banco de dados &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) instrução ou forçar o plano manualmente usando o script na `[details]` coluna. |
| `UnsupportedStatementType` | Não é possível forçar o plano na consulta. Exemplos de consultas sem suporte são cursores e `INSERT BULK` instrução. |
| `LastGoodPlanForced` | A recomendação é aplicada com êxito. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificado regressão de desempenho potencial, mas o `FORCE_LAST_GOOD_PLAN` opção não está habilitada – veja [ALTER AUTOMATIC_TUNING definido do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplicar recomendação manualmente ou habilitar `FORCE_LAST_GOOD_PLAN` opção. |
| `VerificationAborted`| Processo de verificação foi anulado devido à reinicialização ou do limpeza de Store de consulta. |
| `VerificationForcedQueryRecompile`| Consulta é recompilada porque não há nenhuma melhoria de desempenho significativa. |
| `PlanForcedByUser`| Usuário forçado manualmente usando o plano [sp_query_store_force_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) procedimento. |
| `PlanUnforcedByUser` | Usuário não manualmente forçados plano usando [sp_query_store_unforce_plan &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) procedimento. |

 Estatística da coluna de detalhes não mostram as estatísticas do plano de tempo de execução (por exemplo, tempo de CPU atual). Os detalhes de recomendação são obtidos no momento da detecção de regressão e descrever porque [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificado regressão de desempenho. Use `regressedPlanId` e `recommendedPlanId` para consultar [modos de exibição de catálogo de Store de consulta](../../relational-databases/performance/how-query-store-collects-data.md) para localizar as estatísticas de plano de execução exato.

## <a name="examples-of-using-tuning-recommendations-information"></a>Exemplos de como usar informações de recomendações de ajuste  

### <a name="example-1"></a>Exemplo 1
A seguir obtém o gerado [!INCLUDE[tsql](../../includes/tsql-md.md)] script que força um bom plano para qualquer consulta:  
 
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
A seguir obtém o gerado [!INCLUDE[tsql](../../includes/tsql-md.md)] script que força um bom plano para qualquer determinada consulta e informações adicionais sobre o ganho estimado:

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

### <a name="example-3"></a>Exemplo 3:
A seguir obtém o gerado [!INCLUDE[tsql](../../includes/tsql-md.md)] script que força um bom plano para qualquer determinada consulta e informações adicionais que incluem o texto da consulta e os planos de consulta armazenados no Query Store:

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

Para obter mais informações sobre as funções JSON que pode ser usado para valores de consulta no modo de exibição de recomendação, consulte [suporte a JSON](../../relational-databases/json/index.md) em [!INCLUDE[ssde_md](../../includes/ssde_md.md)].
  
## <a name="permissions"></a>Permissões  

Requer `VIEW SERVER STATE` permissão no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
Requer o `VIEW DATABASE STATE` permissão para o banco de dados [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   

## <a name="see-also"></a>Consulte também  
 [O ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Suporte a JSON](../../relational-databases/json/index.md)
 
