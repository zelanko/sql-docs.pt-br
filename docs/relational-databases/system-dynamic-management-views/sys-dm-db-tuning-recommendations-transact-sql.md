---
title: sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: Saiba como encontrar possíveis problemas de desempenho e correções recomendadas no SQL Server e no Azure SQL Database
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285436"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm\_\_recomendações\_de ajuste db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Retorna informações detalhadas sobre recomendações de ajuste.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar expor essas informações, todas as linhas que contenham dados que não pertencem ao inquilino conectado são filtradas.

| **Nome da coluna** | **Tipo de dados** | **Descrição** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome único de recomendação. |
| **type** | **nvarchar(4000)** | O nome da opção de ajuste automático que produziu a recomendação, por exemplo,`FORCE_LAST_GOOD_PLAN` |
| **motivo** | **nvarchar(4000)** | Razão pela qual esta recomendação foi fornecida. |
| **válido\_desde** | **datetime2** | A primeira vez que essa recomendação foi gerada. |
| **última\_atualização** | **datetime2** | A última vez que essa recomendação foi gerada. |
| **Estado** | **nvarchar(4000)** | Documento JSON que descreve o estado da recomendação. Os seguintes campos estão disponíveis:<br />-   `currentValue`- estado atual da recomendação.<br />-   `reason`- constante que descreve por que a recomendação está no estado atual.|
| **é\_ação\_executável** | **bit** | 1 = A recomendação pode ser [!INCLUDE[tsql_md](../../includes/tsql-md.md)] executada no banco de dados via script.<br />0 = A recomendação não pode ser executada no banco de dados (por exemplo: apenas informações ou recomendação revertida) |
| **é\_ação\_revertível** | **bit** | 1 = A recomendação pode ser automaticamente monitorada e revertida pelo mecanismo do Banco de Dados.<br />0 = A recomendação não pode ser automaticamente monitorada e revertida. A &quot;maioria&quot; das &quot;ações&quot;executáveis será revertida. |
| **executar\_\_tempo\_de início de ação** | **datetime2** | Data em que a recomendação for aplicada. |
| **executar\_\_duração de ação** | **time** | Duração da ação de execução. |
| **executar\_\_ação\_iniciada por** | **nvarchar(4000)** | `User`= Plano forçado manualmente pelo usuário na recomendação. <br /> `System`= Recomendação aplicada automaticamente pelo sistema. |
| **executar\_\_ação\_iniciada tempo** | **datetime2** | Data em que a recomendação foi aplicada. |
| **reverter\_\_tempo\_de início ação ação** | **datetime2** | Data em que a recomendação foi revertida. |
| **reverter\_\_duração de ação** | **time** | Duração da ação de reverter. |
| **reverter\_\_ação\_iniciada por** | **nvarchar(4000)** | `User`= Plano recomendado manualmente não forçado pelo usuário. <br /> `System`= Recomendação do sistema automaticamente revertida. |
| **reverter\_\_ação\_iniciada tempo** | **datetime2** | Data em que a recomendação foi revertida. |
| **Pontuação** | **int** | Valor/impacto estimado para esta recomendação na escala 0-100 (quanto maior, melhor) |
| **Detalhes** | **nvarchar(max)** | Documento JSON que contém mais detalhes sobre a recomendação. Os seguintes campos estão disponíveis:<br /><br />`planForceDetails`<br />-    `queryId`- consulta\_id da consulta regredida.<br />-    `regressedPlanId`- plan_id do plano regredido.<br />-   `regressedPlanExecutionCount`- Número de execuções da consulta com plano regredido antes da regressão ser detectada.<br />-    `regressedPlanAbortedCount`- Número de erros detectados durante a execução do plano regredido.<br />-    `regressedPlanCpuTimeAverage`- Tempo médio da CPU (em micro segundos) consumido pela consulta regredida antes da regressão ser detectada.<br />-    `regressedPlanCpuTimeStddev`- Desvio padrão do tempo da CPU consumido pela consulta regredida antes que a regressão seja detectada.<br />-    `recommendedPlanId`- plan_id do plano que deve ser forçado.<br />-   `recommendedPlanExecutionCount`- Número de execuções da consulta com o plano que deve ser forçado antes que a regressão seja detectada.<br />-    `recommendedPlanAbortedCount`- Número de erros detectados durante a execução do plano que deve ser forçado.<br />-    `recommendedPlanCpuTimeAverage`- Tempo médio da CPU (em micro segundos) consumido pela consulta executada com o plano que deve ser forçado (calculado antes da regressão ser detectada).<br />-    `recommendedPlanCpuTimeStddev`Desvio padrão do tempo da CPU consumido pela consulta regredida antes que a regressão seja detectada.<br /><br />`implementationDetails`<br />-  `method`- O método que deve ser usado para corrigir a regressão. Valor é `TSql`sempre .<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]script que deve ser executado para forçar o plano recomendado. |
  
## <a name="remarks"></a>Comentários  
 As informações `sys.dm_db_tuning_recommendations` retornadas são atualizadas quando o mecanismo do banco de dados identifica a regressão potencial do desempenho da consulta e não é persistido. As recomendações são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantidas apenas até que seja reiniciada. Os administradores de banco de dados devem fazer periodicamente cópias de backup da recomendação de ajuste se quiserem mantê-la após a reciclagem do servidor. 

 `currentValue`campo na `state` coluna pode ter os seguintes valores:
 
 | Status | Descrição |
 |--------|-------------|
 | `Active` | A recomendação é ativa e ainda não foi aplicada. O usuário pode pegar o script de recomendação e executá-lo manualmente. |
 | `Verifying` | A recomendação [!INCLUDE[ssde_md](../../includes/ssde_md.md)] é aplicada pelo processo de verificação interna que compara o desempenho do plano forçado com o plano regredido. |
 | `Success` | A recomendação é aplicada com sucesso. |
 | `Reverted` | A recomendação é revertida porque não há ganhos significativos de desempenho. |
 | `Expired` | A recomendação expirou e não pode mais ser aplicada. |

O documento JSON na `state` coluna contém o motivo que descreve por que a recomendação está no estado atual. Valores no campo da razão podem ser: 

| Motivo | Descrição |
|--------|-------------|
| `SchemaChanged` | A recomendação expirou porque o esquema de uma tabela referenciada foi alterado. Nova recomendação será criada se um novo plano de consulta for detectado no novo esquema. |
| `StatisticsChanged`| A recomendação expirou devido à mudança estatística em uma tabela referenciada. Uma nova recomendação será criada se um novo plano de consulta for detectado com base em novas estatísticas. |
| `ForcingFailed` | O plano recomendado não pode ser forçado em uma consulta. Encontre `last_force_failure_reason` o no [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) vista para encontrar a razão do fracasso. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`opção é desativada pelo usuário durante o processo de verificação. Habilitar `FORCE_LAST_GOOD_PLAN` a opção usando [ALTER DATABASE SET AUTOMATIC_TUNING &#40;declaração de&#41;Transact-SQL](../../t-sql/statements/alter-database-transact-sql-set-options.md) ou forçar o plano manualmente usando o script na `[details]` coluna. |
| `UnsupportedStatementType` | O plano não pode ser forçado na consulta. Exemplos de consultas não suportadas são `INSERT BULK` cursores e declaração. |
| `LastGoodPlanForced` | A recomendação é aplicada com sucesso. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]identificou regressão de desempenho `FORCE_LAST_GOOD_PLAN` potencial identificada, mas a opção não está habilitada - consulte [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplique recomendação manualmente ou habilite a `FORCE_LAST_GOOD_PLAN` opção. |
| `VerificationAborted`| O processo de verificação é abortado devido à limpeza da reinicialização ou da Loja de Consulta. |
| `VerificationForcedQueryRecompile`| A consulta é recompilada porque não há melhora significativa no desempenho. |
| `PlanForcedByUser`| O usuário forçou manualmente o plano usando [sp_query_store_force_plan procedimento de&#41;transact-SQL &#40;.](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) O mecanismo do banco de dados não aplicará a recomendação se o usuário decidir explicitamente forçar algum plano. |
| `PlanUnforcedByUser` | O usuário não forçou manualmente o plano usando [sp_query_store_unforce_plan procedimento de&#41;transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) &#40;. Uma vez que o usuário reverteu explicitamente o plano recomendado, o mecanismo de banco de dados continuará usando o plano atual e gerará uma nova recomendação se alguma regressão do plano ocorrer no futuro. |

 A estatística na coluna de detalhes não mostra estatísticas do plano de tempo de execução (por exemplo, o tempo atual da CPU). Os detalhes da recomendação são tomados no [!INCLUDE[ssde_md](../../includes/ssde_md.md)] momento da detecção da regressão e descrevem por que a regressão de desempenho identificada. Use `regressedPlanId` `recommendedPlanId` e consulte as visualizações do [catálogo da Query Store](../../relational-databases/performance/how-query-store-collects-data.md) para encontrar estatísticas exatas do plano de tempo de execução.

## <a name="examples-of-using-tuning-recommendations-information"></a>Exemplos de uso de informações sobre recomendações de ajuste  

### <a name="example-1"></a>Exemplo 1
A seguir, [!INCLUDE[tsql](../../includes/tsql-md.md)] obtém o script gerado que força um bom plano para qualquer consulta dada:  
 
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
A seguir, [!INCLUDE[tsql](../../includes/tsql-md.md)] obtém o script gerado que força um bom plano para qualquer consulta dada e informações adicionais sobre o ganho estimado:

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
A seguir, [!INCLUDE[tsql](../../includes/tsql-md.md)] obtém o script gerado que força um bom plano para qualquer consulta dada e informações adicionais que incluam o texto de consulta e os planos de consulta armazenados na Query Store:

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

Para obter mais informações sobre funções JSON que podem ser usadas para consultar [!INCLUDE[ssde_md](../../includes/ssde_md.md)]valores na exibição de recomendação, consulte O suporte ao [JSON](../../relational-databases/json/index.md) em .
  
## <a name="permissions"></a>Permissões  

Requer `VIEW SERVER STATE` permissão em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
Requer `VIEW DATABASE STATE` a permissão [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]para o banco de dados em .   

## <a name="see-also"></a>Consulte Também  
 [Sintonia automática](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options&#41;&#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options database_query_store_options&#41;&#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Suporte JSON](../../relational-databases/json/index.md)
 
