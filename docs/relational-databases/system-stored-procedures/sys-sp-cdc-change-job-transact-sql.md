---
title: sp_cdc_change_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cfbf93fc858f52cd35401bd80fe5ede7dee86a3d
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591740"
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica a configuração de um trabalho de captura ou limpeza do Change Data Capture no banco de dados atual. Para exibir a configuração atual de um trabalho, consulte o [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) de tabela, ou use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md).  
  
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
 [  **@job_type=** ] **'**_job_type_**'**  
 Tipo de trabalho a ser modificado. *job_type* está **nvarchar (20)** com um padrão de 'capture'. As entradas válidas são 'capture' e 'cleanup'.  
  
 [ **@maxtrans** ] **=** _max_trans_  
 O número máximo de transações a processar em cada ciclo de exame. *max_trans* está **int** com um padrão NULL, que indica nenhuma alteração para esse parâmetro. Se especificado, o valor deve ser um inteiro positivo.  
  
 *max_trans* é válido somente para trabalhos de captura.  
  
 [ **@maxscans** ] **=** _max_scans_  
 O número máximo de ciclos de exame a executar para extrair todas as linhas do log. *max_scans* está **int** com um padrão NULL, que indica nenhuma alteração para esse parâmetro.  
  
 *max_scan* é válido somente para trabalhos de captura.  
  
 [ **@continuous** ] **=** _contínua_  
 Indica se o trabalho de captura deve ser executado continuamente (1) ou apenas uma vez (0). *contínua* está **bit** com um padrão NULL, que indica nenhuma alteração para esse parâmetro.  
  
 Quando *contínua* = 1, o [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) trabalho examina o log e processa até (*max_trans* \* *max_scans*) transações. Ele, em seguida, aguardará o número de segundos especificado no *polling_interval* antes de iniciar a próxima verificação de log.  
  
 Quando *contínua* = 0, o **sp_cdc_scan** trabalho é executado até *max_scans* verificações do log, processando até *max_trans* transações durante cada verificação e, em seguida, sai.  
  
 Se **@continuous** é alterado de 1 para 0, **@pollinginterval** é definida automaticamente como 0. Um valor especificado para **@pollinginterval** diferente de 0 é ignorado.  
  
 Se **@continuous** for omitido ou explicitamente definido como NULL e **@pollinginterval** é explicitamente definido como um valor maior que 0, **@continuous** é automaticamente definido como 1.  
  
 *contínua* é válido somente para trabalhos de captura.  
  
 [ **@pollinginterval** ] **=** _polling_interval_  
 Número de segundos entre ciclos de exame de log. *polling_interval* está **bigint** com um padrão NULL, que indica nenhuma alteração para esse parâmetro.  
  
 *polling_interval* é válido somente para captura de trabalhos quando *contínua* é definido como 1.  
  
 [ **@retention** ] **=** _retenção_  
 O número de minutos que as linhas de alteração devem ser retidas em tabelas de alteração. *retenção* está **bigint** com um padrão NULL, que indica nenhuma alteração para esse parâmetro. O valor máximo é 52494800 (100 anos). Se especificado, o valor deve ser um inteiro positivo.  
  
 *retenção* é válido somente para trabalhos de limpeza.  
  
 [  **@threshold=** ] **'**_excluir limite_**'**  
 O número máximo de entradas de exclusão que podem ser excluídas por meio de uma única instrução na limpeza. *excluir o limite* está **bigint** com um padrão NULL, que indica nenhuma alteração para esse parâmetro. *Excluir limite* é válido somente para trabalhos de limpeza.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 Se um parâmetro for omitido, o valor associado na [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) tabela não é atualizada. Um conjunto de parâmetros definido explicitamente como NULL é tratado como se o parâmetro tivesse sido omitido.  
  
 Especificar um parâmetro que é inválido para o tipo de trabalho fará a instrução falhar.  
  
 As alterações a um trabalho não terão efeito até que o trabalho seja interrompido por meio [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) e reiniciado usando [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **db_owner** função fixa de banco de dados.  
  
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
  
### <a name="b-changing-a-cleanup-job"></a>b. Alterando um trabalho de limpeza  
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
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
