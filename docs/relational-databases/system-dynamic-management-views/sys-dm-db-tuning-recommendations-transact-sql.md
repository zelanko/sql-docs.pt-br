---
title: sys. dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: e8c18ce07ba5e36dcbdb5750db77edf17495c7b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285436"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>recomendações\_de\_ajuste\_do sys.dm dB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Retorna informações detalhadas sobre as recomendações de ajuste.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.

| **Nome da coluna** | **Tipo de dados** | **Descrição** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome exclusivo da recomendação. |
| **type** | **nvarchar(4000)** | O nome da opção de ajuste automático que produziu a recomendação, por exemplo,`FORCE_LAST_GOOD_PLAN` |
| **motivo** | **nvarchar(4000)** | Motivo pelo qual essa recomendação foi fornecida. |
| **válido\_desde** | **datetime2** | Na primeira vez em que essa recomendação foi gerada. |
| **última\_atualização** | **datetime2** | A última vez em que essa recomendação foi gerada. |
| **state** | **nvarchar(4000)** | Documento JSON que descreve o estado da recomendação. Os campos a seguir estão disponíveis:<br />-   `currentValue`-estado atual da recomendação.<br />-   `reason`– constante que descreve por que a recomendação está no estado atual.|
| **é\_ação\_executável** | **bit** | 1 = a recomendação pode ser executada no banco de dados [!INCLUDE[tsql_md](../../includes/tsql-md.md)] via script.<br />0 = a recomendação não pode ser executada no banco de dados (por exemplo: somente informações ou recomendação revertida) |
| **é\_\_ação revertida** | **bit** | 1 = a recomendação pode ser monitorada e revertida automaticamente pelo mecanismo de banco de dados.<br />0 = a recomendação não pode ser monitorada e revertida automaticamente. A &quot;maioria&quot; das ações executáveis será &quot;revertida&quot;. |
| **executar\_a\_hora\_de início da ação** | **datetime2** | Data em que a recomendação é aplicada. |
| **duração\_da\_ação de execução** | **time** | Duração da ação de execução. |
| **executar\_ação\_iniciada\_por** | **nvarchar(4000)** | `User`= O usuário forçou manualmente o plano na recomendação. <br /> `System`= O sistema aplicou automaticamente a recomendação. |
| **tempo\_iniciado\_\_da ação de execução** | **datetime2** | Data em que a recomendação foi aplicada. |
| **reverter\_hora\_de\_início da ação** | **datetime2** | Data em que a recomendação foi revertida. |
| **reverter\_duração\_da ação** | **time** | Duração da ação de reversão. |
| **reverter\_ação\_iniciada\_por** | **nvarchar(4000)** | `User`= O plano recomendado pelo usuário não foi forçado manualmente. <br /> `System`= O sistema reverteu a recomendação automaticamente. |
| **reverter\_hora\_iniciada\_da ação** | **datetime2** | Data em que a recomendação foi revertida. |
| **placar** | **int** | Valor/impacto estimado para essa recomendação na escala de 0-100 (maior é o melhor) |
| **Ver** | **nvarchar(max)** | Documento JSON que contém mais detalhes sobre a recomendação. Os campos a seguir estão disponíveis:<br /><br />`planForceDetails`<br />-    `queryId`-ID\_de consulta da consulta regressiva.<br />-    `regressedPlanId`-plan_id do plano regressivo.<br />-   `regressedPlanExecutionCount`-Número de execuções da consulta com o plano regressivo antes de a regressão ser detectada.<br />-    `regressedPlanAbortedCount`-Número de erros detectados durante a execução do plano regressivo.<br />-    `regressedPlanCpuTimeAverage`-Tempo médio de CPU (em micro segundos) consumido pela consulta regressiva antes de a regressão ser detectada.<br />-    `regressedPlanCpuTimeStddev`-Desvio padrão do tempo de CPU consumido pela consulta regressiva antes de a regressão ser detectada.<br />-    `recommendedPlanId`-plan_id do plano que deve ser forçado.<br />-   `recommendedPlanExecutionCount`-Número de execuções da consulta com o plano que deve ser forçado antes que a regressão seja detectada.<br />-    `recommendedPlanAbortedCount`-Número de erros detectados durante a execução do plano que deve ser forçado.<br />-    `recommendedPlanCpuTimeAverage`-Tempo médio de CPU (em micro segundos) consumido pela consulta executada com o plano que deve ser forçado (calculado antes da detecção da regressão).<br />-    `recommendedPlanCpuTimeStddev`Desvio padrão do tempo de CPU consumido pela consulta regressiva antes de a regressão ser detectada.<br /><br />`implementationDetails`<br />-  `method`-O método que deve ser usado para corrigir a regressão. O valor é `TSql`sempre.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]script que deve ser executado para forçar o plano recomendado. |
  
## <a name="remarks"></a>Comentários  
 As informações retornadas pelo `sys.dm_db_tuning_recommendations` são atualizadas quando o mecanismo de banco de dados identifica a possível regressão de desempenho de consulta e não é persistente. As recomendações são mantidas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente até que o seja reiniciado. Os administradores de banco de dados devem fazer cópias de backup da recomendação de ajuste periodicamente se desejarem mantê-lo após a reciclagem do servidor. 

 `currentValue`o campo na `state` coluna pode ter os seguintes valores:
 
 | Status | Descrição |
 |--------|-------------|
 | `Active` | A recomendação está ativa e ainda não foi aplicada. O usuário pode usar o script de recomendação e executá-lo manualmente. |
 | `Verifying` | A recomendação é aplicada [!INCLUDE[ssde_md](../../includes/ssde_md.md)] pelo e o processo de verificação interno compara o desempenho do plano forçado com o plano regressivo. |
 | `Success` | A recomendação foi aplicada com êxito. |
 | `Reverted` | A recomendação é revertida porque não há ganhos de desempenho significativos. |
 | `Expired` | A recomendação expirou e não pode mais ser aplicada. |

O documento JSON `state` na coluna contém o motivo que descreve por que é a recomendação no estado atual. Os valores no campo de motivo podem ser: 

| Motivo | Descrição |
|--------|-------------|
| `SchemaChanged` | A recomendação expirou porque o esquema de uma tabela referenciada foi alterado. A nova recomendação será criada se uma nova regressão do plano de consulta for detectada no novo esquema. |
| `StatisticsChanged`| A recomendação expirou devido à alteração de estatística em uma tabela referenciada. A nova recomendação será criada se uma nova regressão do plano de consulta for detectada com base em novas estatísticas. |
| `ForcingFailed` | O plano recomendado não pode ser forçado em uma consulta. Localize o `last_force_failure_reason` na exibição [Sys. query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) para encontrar o motivo da falha. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`a opção é desabilitada pelo usuário durante o processo de verificação. Habilite `FORCE_LAST_GOOD_PLAN` a opção usando [ALTER DATABASE SET AUTOMATIC_TUNING &#40;instrução Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) ou force o plano manualmente usando o `[details]` script na coluna. |
| `UnsupportedStatementType` | O plano não pode ser forçado na consulta. Exemplos de consultas sem suporte são cursores e `INSERT BULK` instruções. |
| `LastGoodPlanForced` | A recomendação foi aplicada com êxito. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]regressão de desempenho potencial identificada, `FORCE_LAST_GOOD_PLAN` mas a opção não está habilitada-consulte [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplique a recomendação manualmente ou `FORCE_LAST_GOOD_PLAN` habilite a opção. |
| `VerificationAborted`| O processo de verificação foi anulado devido à reinicialização ou Repositório de Consultas limpeza. |
| `VerificationForcedQueryRecompile`| A consulta é recompilada porque não há uma melhoria significativa no desempenho. |
| `PlanForcedByUser`| O usuário forçou manualmente o plano usando [sp_query_store_force_plan &#40;procedimento de&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) . O mecanismo de banco de dados não aplicará a recomendação se o usuário decidir explicitamente forçar algum plano. |
| `PlanUnforcedByUser` | O usuário não impô manualmente o plano usando [sp_query_store_unforce_plan &#40;procedimento de&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) . Como o usuário reverteu explicitamente o plano recomendado, o mecanismo de banco de dados continuará usando o plano atual e gerará uma nova recomendação se ocorrer alguma regressão do plano no futuro. |

 A estatística na coluna de detalhes não mostra as estatísticas do plano de tempo de execução (por exemplo, o tempo de CPU atual). Os detalhes de recomendação são obtidos no momento da detecção de regressão e descrevem [!INCLUDE[ssde_md](../../includes/ssde_md.md)] por que a regressão de desempenho identificada. Use `regressedPlanId` e `recommendedPlanId` para consultar [repositório de consultas exibições de catálogo](../../relational-databases/performance/how-query-store-collects-data.md) para localizar as estatísticas exatas do plano de tempo de execução.

## <a name="examples-of-using-tuning-recommendations-information"></a>Exemplos de como usar informações de recomendações de ajuste  

### <a name="example-1"></a>Exemplo 1
O seguinte Obtém o script [!INCLUDE[tsql](../../includes/tsql-md.md)] gerado que força um bom plano para qualquer consulta específica:  
 
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
O seguinte Obtém o script [!INCLUDE[tsql](../../includes/tsql-md.md)] gerado que força um bom plano para qualquer consulta específica e informações adicionais sobre o lucro estimado:

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
Veja a seguir o script [!INCLUDE[tsql](../../includes/tsql-md.md)] gerado que força um bom plano para qualquer consulta específica e informações adicionais que incluam o texto da consulta e os planos de consulta armazenados no repositório de consultas:

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

Para obter mais informações sobre as funções JSON que podem ser usadas para consultar valores no modo de exibição de recomendação, [!INCLUDE[ssde_md](../../includes/ssde_md.md)]consulte suporte a [JSON](../../relational-databases/json/index.md) no.
  
## <a name="permissions"></a>Permissões  

Requer `VIEW SERVER STATE` permissão no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
Requer a `VIEW DATABASE STATE` permissão para o banco de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]dados no.   

## <a name="see-also"></a>Consulte Também  
 [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys. database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys. database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Suporte a JSON](../../relational-databases/json/index.md)
 
