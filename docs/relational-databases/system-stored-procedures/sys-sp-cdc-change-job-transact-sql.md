---
title: sys.sp_cdc_change_job (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 4bd906f9a359a73a15d89a4cb60b6646a2abe53a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305069"
---
# <a name="syssp_cdc_change_job-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica a configuração de um trabalho de captura ou limpeza do Change Data Capture no banco de dados atual. Para exibir a configuração atual de um trabalho, consulte a tabela [dbo. CDC _jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) ou use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md).  
  
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
`[ @job_type = ] 'job_type'` tipo de trabalho a ser modificado. *job_type* é **nvarchar (20)** com um padrão de ' Capture '. As entradas válidas são 'capture' e 'cleanup'.  
  
`[ @maxtrans ] = max_trans_` número máximo de transações a serem processadas em cada ciclo de verificação. *max_trans* é **int** com um padrão de NULL, que não indica nenhuma alteração para esse parâmetro. Se especificado, o valor deve ser um inteiro positivo.  
  
 *max_trans* é válido somente para trabalhos de captura.  
  
`[ @maxscans ] = max_scans_` número máximo de ciclos de verificação a serem executados para extrair todas as linhas do log. *max_scans* é **int** com um padrão de NULL, que não indica nenhuma alteração para esse parâmetro.  
  
 *max_scan* é válido somente para trabalhos de captura.  
  
`[ @continuous ] = continuous_` indica se o trabalho de captura deve ser executado continuamente (1) ou ser executado apenas uma vez (0). *continuou* é **bit** com um padrão de NULL, que não indica nenhuma alteração para esse parâmetro.  
  
 Quando *Continuous* = 1, o trabalho [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) examina o log e processa até (*max_trans* \* *max_scans*) transações. Em seguida, ele aguarda o número de segundos especificado em *polling_interval* antes de iniciar a próxima verificação de log.  
  
 Quando *Continuous* = 0, o trabalho **sp_cdc_scan** é executado até *max_scans* verificações do log, processando até *max_trans* transações durante cada verificação e, em seguida, sai.  
  
 Se **\@continuous** for alterado de 1 para 0, **\@pollinginterval** será definido automaticamente como 0. Um valor especificado para **\@pollinginterval** diferente de 0 é ignorado.  
  
 Se **\@continuous** for omitido ou definido explicitamente como nulo e **\@pollinginterval** for definido explicitamente como um valor maior que 0, **\@continuous** será definido automaticamente como 1.  
  
 *contínuo* é válido somente para trabalhos de captura.  
  
`[ @pollinginterval ] = polling_interval_` número de segundos entre os ciclos de verificação de log. *polling_interval* é **bigint** com um padrão de NULL, que não indica nenhuma alteração para esse parâmetro.  
  
 *polling_interval* é válido somente para trabalhos de captura quando *Continuous* é definido como 1.  
  
`[ @retention ] = retention_` número de minutos que as linhas de alteração devem ser retidas em tabelas de alterações. a *retenção* é **bigint** com um padrão de NULL, que não indica nenhuma alteração para esse parâmetro. O valor máximo é 52494800 (100 anos). Se especificado, o valor deve ser um inteiro positivo.  
  
 a *retenção* é válida somente para trabalhos de limpeza.  
  
`[ @threshold = ] 'delete threshold'` número máximo de entradas de exclusão que podem ser excluídas usando uma única instrução na limpeza. o *limite de exclusão* é **bigint** com um padrão de NULL, que não indica nenhuma alteração para esse parâmetro. o *limite de exclusão* é válido somente para trabalhos de limpeza.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Se um parâmetro for omitido, o valor associado na tabela [dbo. CDC _jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) não será atualizado. Um conjunto de parâmetros definido explicitamente como NULL é tratado como se o parâmetro tivesse sido omitido.  
  
 Especificar um parâmetro que é inválido para o tipo de trabalho fará a instrução falhar.  
  
 As alterações em um trabalho não entram em vigor até que o trabalho seja interrompido usando [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) e reiniciado usando [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-a-capture-job"></a>A. Alterando um trabalho de captura  
 O exemplo a seguir atualiza os parâmetros `@job_type`, `@maxscans` e `@maxtrans` de um trabalho de captura no banco de dados `AdventureWorks2012`. Os outros parâmetros válidos para um trabalho de captura, `@continuous` e `@pollinginterval`, são omitidos; seus valores não são modificados.  
  
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
 O exemplo a seguir atualiza um trabalho de limpeza no banco de dados `AdventureWorks2012`. Todos os parâmetros válidos para esse tipo de trabalho, exceto **@threshold** , são especificados. O valor de **@threshold** não é modificado.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
