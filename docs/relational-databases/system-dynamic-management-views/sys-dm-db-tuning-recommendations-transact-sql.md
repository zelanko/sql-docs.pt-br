---
title: sys.dm_db_tuning_recommendations (Transact-SQL) | Microsoft Docs
description: "Saiba como localizar problemas de desempenho e recomendações de correção no SQL Server e banco de dados do SQL Azure"
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43acc4c2bfbcb9458f93f2ad89414e3781a7836d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.dm\_db\_tuning\_recommendations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Retorna informações detalhadas sobre recomendações de ajuste.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém os dados que não pertencem ao locatário conectado será filtrada.

| **Nome da coluna** | **Tipo de dados** | **Descrição** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | Nome exclusivo da recomendação. |
| **type** | **nvarchar(4000)** | O nome da opção de ajuste automático que gerou a recomendação, por exemplo,`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | Motivo por que essa recomendação foi fornecida. |
| **valid\_since** | **datetime2** | Na primeira vez em que essa recomendação foi gerada. |
| **última\_atualizar** | **datetime2** | A última vez em que essa recomendação foi gerada. |
| **state** | **nvarchar(4000)** | Documento JSON que descreve o estado da recomendação. Campos a seguir estão disponíveis:<br />-   `currentValue`-estado atual da recomendação.<br />-   `reason`– constante que descreve o motivo pelo qual a recomendação está no estado atual.|
| **is\_executable\_action** | **bit** | 1 = a recomendação pode ser executada no banco de dados por meio de [!INCLUDE[tsql_md](../../includes/tsql_md.md)] script.<br />0 = a recomendação não pode ser executada no banco de dados (por exemplo: recomendação apenas ou revertido de informações) |
| **is\_revertable\_action** | **bit** | 1 = a recomendação pode ser monitorada e revertida pelo mecanismo de banco de dados automaticamente.<br />0 = a recomendação não pode ser monitorada e revertida automaticamente. A maioria dos &quot;executável&quot; ações serão &quot;revertable&quot;. |
| **execute\_action\_start\_time** | **datetime2** | Data em que a recomendação é aplicada. |
| **execute\_action\_duration** | **time** | Duração da ação executar. |
| **executar\_ação\_iniciada\_por** | **nvarchar(4000)** | `User`= Usuário forçado manualmente o plano na recomendação. <br /> `System`= Sistema aplicada automaticamente a recomendação. |
| **executar\_ação\_iniciada\_tempo** | **datetime2** | Data em que a recomendação foi aplicada. |
| **revert\_action\_start\_time** | **datetime2** | Data em que a recomendação foi revertida. |
| **revert\_action\_duration** | **time** | Duração da ação de reversão. |
| **Reverter\_ação\_iniciada\_por** | **nvarchar(4000)** | `User`= Plano de recomendado manualmente unforced usuário. <br /> `System`= Sistema revertido automaticamente a recomendação. |
| **Reverter\_ação\_iniciada\_tempo** | **datetime2** | Data em que a recomendação foi revertida. |
| **score** | **Int** | Estimado valor/impacto para esta recomendação para o valor de 0 a 100 escala (quanto maior o melhor) |
| **details** | **nvarchar(max)** | Documento JSON que contém mais detalhes sobre a recomendação. Campos a seguir estão disponíveis:<br /><br />`planForceDetails`<br />-    `queryId`-consulta\_id da consulta retornada.<br />-    `regressedPlanId`-plan_id do plano retornado.<br />-   `regressedPlanExecutionCount`-Número de execuções de consulta com retornadas plano antes da regressão é detectado.<br />-    `regressedPlanAbortedCount`-Número de erros detectados durante a execução do plano retornada.<br />-    `regressedPlanCpuTimeAverage`-Tempo de CPU médio consumido pela consulta retornada para a regressão é detectada.<br />-    `regressedPlanCpuTimeStddev`-Desvio padrão de tempo de CPU consumido pela consulta retornada antes da regressão é detectado.<br />-    `recommendedPlanId`-plan_id do plano que deve ser forçado.<br />-   `recommendedPlanExecutionCount`-Número de execuções de consulta com o plano deve ser forçado para a regressão é detectada.<br />-    `recommendedPlanAbortedCount`-Número de erros detectados durante a execução do plano que deve ser forçado.<br />-    `recommendedPlanCpuTimeAverage`-Tempo de CPU médio consumido pela consulta executada com o plano deve ser forçado (calculado antes da regressão é detectada).<br />-    `recommendedPlanCpuTimeStddev`Desvio padrão de tempo de CPU consumido pela consulta retornada antes da regressão é detectado.<br /><br />`implementationDetails`<br />-  `method`-O método que deve ser usado para corrigir a regressão. Valor é sempre `TSql`.<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql_md.md)]script que deve ser executado para forçar o plano recomendado. |
  
## <a name="remarks"></a>Remarks  
 Informações retornadas por `sys.dm_db_tuning_recommendations` é atualizada quando o mecanismo de banco de dados identifica possíveis regressão de desempenho de consulta e não persistirão. As recomendações são mantidas apenas até [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de recomendação de ajuste de se quiserem mantê-lo após a reciclagem do servidor. 

 `currentValue`campo de `state` coluna pode ter os seguintes valores:
 | Status | Description |
 |--------|-------------|
 | `Active` | Recomendação está ativa e não ainda é aplicada. Usuário pode tirar o script de recomendação e executá-lo manualmente. |
 | `Verifying` | Recomendação é aplicada pelo [!INCLUDE[ssde_md](../../includes/ssde_md.md)] e o processo de verificação internos compara o desempenho do plano forçado com o plano retornado. |
 | `Success` | Recomendação é aplicada com êxito. |
 | `Reverted` | Recomendação é revertida, pois não há nenhum ganhos significativos de desempenho. |
 | `Expired` | Recomendação expirou e não pode ser aplicada mais. |

Documento JSON em `state` coluna contém o motivo que descreve o motivo pelo qual é a recomendação no estado atual. Os valores no campo motivo podem ser: 

| Reason | Description |
|--------|-------------|
| `SchemaChanged` | Recomendação expirado porque o esquema de uma tabela referenciada é alterado. |
| `StatisticsChanged`| Recomendação expirou devido à alteração de estatística em uma tabela referenciada. |
| `ForcingFailed` | Não é possível forçar o plano recomendado em uma consulta. Localizar o `last_force_failure_reason` no [query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) para localizar o motivo da falha. |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`opção está desabilitada pelo usuário durante o processo de verificação. Habilitar `FORCE_LAST_GOOD_PLAN` usando a opção [ALTER AUTOMATIC_TUNING definido do banco de dados &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) instrução ou forçar o plano manualmente usando o script `[details]` coluna. |
| `UnsupportedStatementType` | Não é possível forçar o plano na consulta. Exemplos de consultas sem suporte são cursores e `INSERT BULK` instrução. |
| `LastGoodPlanForced` | Recomendação é aplicada com êxito. |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificado regressão de desempenho potencial, mas o `FORCE_LAST_GOOD_PLAN` opção não está habilitada – consulte [ALTER AUTOMATIC_TUNING definido do banco de dados &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Aplicar a recomendação manualmente ou habilitar `FORCE_LAST_GOOD_PLAN` opção. |
| `VerificationAborted`| Processo de verificação foi anulado devido a reinicialização ou a limpeza do repositório de consultas. |
| `VerificationForcedQueryRecompile`| Consulta é recompilada porque não há nenhum aprimoramento de desempenho significativa. |
| `PlanForcedByUser`| Usuário forçado manualmente usando o plano [sp_query_store_force_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) procedimento. |
| `PlanUnforcedByUser` | Usuário não manualmente forçados plano usando [sp_query_store_unforce_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) procedimento. |

 Estatística da coluna de detalhes não mostrar estatísticas de plano de tempo de execução (por exemplo, tempo de CPU atual). Os detalhes de recomendação são realizados no momento da detecção de regressão e descrever porque [!INCLUDE[ssde_md](../../includes/ssde_md.md)] identificado regressão de desempenho. Use `regressedPlanId` e `recommendedPlanId` a consulta [exibições do catálogo de repositório de consultas](../../relational-databases/performance/how-query-store-collects-data.md) para localizar as estatísticas do plano exata do tempo de execução.

## <a name="using-tuning-recommendations-information"></a>Usando informações de recomendações de ajuste  
 Você pode usar a consulta a seguir para obter o script T-SQL que corrige o problema:  
 
```
SELECT name, reason, score,
        JSON_VALUE(details, '$.implementationDetails.script') as script,
        details.* 
FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(details, '$.planForceDetails')
                WITH (  query_id int '$.queryId',
                        regressed_plan_id int '$.regressedPlanId',
                        last_good_plan_id int '$.recommendedPlanId') as details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active'
```
  
 Para obter mais informações sobre as funções JSON que pode ser usado para valores de consulta no modo de exibição de recomendação, consulte [suporte JSON](../../relational-databases/json/index.md) em [!INCLUDE[ssde_md](../../includes/ssde_md.md)].
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o `Server admin` ou um `Azure Active Directory admin` conta.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Suporte a JSON](../../relational-databases/json/index.md)
 
