---
title: sp_cdc_change_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48ea42d122c0b7431279ec53b384d400ea5f9de8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica a configuração de um trabalho de captura ou limpeza do Change Data Capture no banco de dados atual. Para exibir a configuração atual de um trabalho, consulte o [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) tabela ou use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_type=** ] **'***job_type***'**  
 Tipo de trabalho a ser modificado. *job_type* é **nvarchar (20)** com um padrão de 'capture'. As entradas válidas são 'capture' e 'cleanup'.  
  
 [ **@maxtrans** ] **= * max_trans*  
 O número máximo de transações a processar em cada ciclo de exame. *max_trans* é **int** com um padrão NULL, que indica nenhuma alteração para esse parâmetro. Se especificado, o valor deve ser um inteiro positivo.  
  
 *max_trans* é válido somente para trabalhos de captura.  
  
 [ **@maxscans** ] **= * max_scans*  
 O número máximo de ciclos de exame a executar para extrair todas as linhas do log. *max_scans* é **int** com um padrão NULL, que indica nenhuma alteração para esse parâmetro.  
  
 *max_scan* é válido somente para trabalhos de captura.  
  
 [ **@continuous** ] **= * contínua*  
 Indica se o trabalho de captura deve ser executado continuamente (1) ou apenas uma vez (0). *contínua* é **bit** com um padrão NULL, que indica nenhuma alteração para esse parâmetro.  
  
 Quando *contínua* = 1, o [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) trabalho examina o log e processa até (*max_trans* \* *max_scans*) transações. Ele espera, em seguida, o número de segundos especificado em *intervalo_de_sondagem* antes de começar a próxima verificação de log.  
  
 Quando *contínua* = 0, o **sp_cdc_scan** executa trabalho até *max_scans* verificações do log, processando até *max_trans* transações durante cada verificação e, em seguida, sai.  
  
 Se **@continuous** é alterado de 1 para 0, **@pollinginterval** é definida automaticamente como 0. Um valor especificado para **@pollinginterval** diferente de 0 é ignorado.  
  
 Se **@continuous** for omitido ou explicitamente definido como NULL e **@pollinginterval** é definida explicitamente como um valor maior que 0, **@continuous** automaticamente definido como 1.  
  
 *contínua* é válido somente para trabalhos de captura.  
  
 [ **@pollinginterval** ] **= * intervalo_de_sondagem*  
 Número de segundos entre ciclos de exame de log. *intervalo_de_sondagem* é **bigint** com um padrão NULL, que indica nenhuma alteração para esse parâmetro.  
  
 *intervalo_de_sondagem* é válido somente para captura trabalhos quando *contínua* é definido como 1.  
  
 [ **@retention** ] **= * retenção*  
 O número de minutos que as linhas de alteração devem ser retidas em tabelas de alteração. *retenção* é **bigint** com um padrão NULL, que indica nenhuma alteração para esse parâmetro. O valor máximo é 52494800 (100 anos). Se especificado, o valor deve ser um inteiro positivo.  
  
 *retenção* é válido somente para trabalhos de limpeza.  
  
 [  **@threshold=** ] **'***excluir limite***'**  
 O número máximo de entradas de exclusão que podem ser excluídas por meio de uma única instrução na limpeza. *Excluir limite* é **bigint** com um padrão NULL, que indica nenhuma alteração para esse parâmetro. *Excluir limite* é válido somente para trabalhos de limpeza.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Se um parâmetro for omitido, o valor associado no [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) tabela não é atualizada. Um conjunto de parâmetros definido explicitamente como NULL é tratado como se o parâmetro tivesse sido omitido.  
  
 Especificar um parâmetro que é inválido para o tipo de trabalho fará a instrução falhar.  
  
 As alterações a um trabalho não entram em vigor até que o trabalho é interrompido usando [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) e reiniciado usando [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **db_owner** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-a-capture-job"></a>A. Alterando um trabalho de captura  
 A exemplo a seguir atualiza o `@job_type`, `@maxscans`, e `@maxtrans` parâmetros de um trabalho de captura no `AdventureWorks2012` banco de dados. Os outros parâmetros válidos para um trabalho de captura, `@continuous` e `@pollinginterval`, são omitidos; seus valores não são modificados.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>B. Alterando um trabalho de limpeza  
 O exemplo a seguir atualiza um trabalho de limpeza no banco de dados `AdventureWorks2012`. Todos os parâmetros válidos para esse tipo de trabalho, exceto **@threshold**, são especificados. O valor de **@threshold** não é modificado.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys. sp_cdc_add_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
