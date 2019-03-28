---
title: sys.sp_cdc_add_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_add_job_TSQL
- sys.sp_cdc_add_job
- sys.sp_cdc_add_job_TSQL
- sp_cdc_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_add_job
ms.assetid: c4458738-ed25-40a6-8294-a26ca5a05bd9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 533f37252fa16e2e139f29ac843d6d4a933f13de
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532130"
---
# <a name="sysspcdcaddjob-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma limpeza de captura de dados de alteração ou trabalho de captura no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_add_job [ @job_type = ] 'job_type'  
    [ , [ @start_job = ] start_job ]   
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ , [ @threshold ] = 'delete_threshold' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_type = ] 'job\_type'` Tipo de trabalho a ser adicionado. *job_type* está **nvarchar (20)** e não pode ser NULL. As entradas válidas são **'capture'** e **'cleanup'**.  
  
`[ @start_job = ] start_job` Sinalizador que indica se o trabalho deve ser iniciado imediatamente depois que ele é adicionado. *start_job* está **bit** com um padrão de 1.  
  
`[ @maxtrans ] = max_trans` Número máximo de transações a serem processadas em cada ciclo de verificação. *max_trans* está **int** com um padrão de 500. Se especificado, o valor deve ser um inteiro positivo.  
  
 *max_trans* é válido somente para trabalhos de captura.  
  
`[ @maxscans ] = max\_scans_` Número máximo de ciclos de exame a executar para extrair todas as linhas do log. *max_scans* está **int** com um padrão de 10.  
  
 *max_scan* é válido somente para trabalhos de captura.  
  
`[ @continuous ] = continuous_` Indica se o trabalho de captura deve ser executado continuamente (1), ou apenas uma vez (0). *contínua* está **bit** com um padrão de 1.  
  
 Quando *contínua* = 1, o [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) trabalho examina o log e processa até (*max_trans* \* *max_scans*) transações. Ele, em seguida, aguardará o número de segundos especificado no *polling_interval* antes de iniciar a próxima verificação de log.  
  
 Quando *contínua* = 0, o **sp_cdc_scan** trabalho é executado até *max_scans* verificações do log, processando até *max_trans* transação durante cada verificação e, em seguida, sai.  
  
 *contínua* é válido somente para trabalhos de captura.  
  
`[ @pollinginterval ] = polling\_interval_` Número de segundos entre ciclos de exame de log. *polling_interval* está **bigint** com um padrão de 5.  
  
 *polling_interval* é válido somente para captura de trabalhos quando *contínua* é definido como 1. Se especificado, o valor não pode ser negativo nem exceder 24 horas. Se um valor 0 estiver especificado, não haverá espera entre os exames de log.  
  
`[ @retention ] = retention_` Número de minutos que alteram os dados de linhas são retidas em tabelas de alteração. *retenção* está **bigint** com um padrão de 4320 (72 horas). O valor máximo é 52494800 (100 anos). Se especificado, o valor deve ser um inteiro positivo.  
  
 *retenção* é válido somente para trabalhos de limpeza.  
  
`[ @threshold = ] 'delete\_threshold'` Número máximo de entradas de exclusão que podem ser excluídas usando uma única instrução na limpeza. *delete_threshold* está **bigint** com um padrão de 5000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 Um trabalho de limpeza é criado usando os valores padrão quando a primeira tabela no banco de dados é habilitada para captura de dados de alteração. Um trabalho de captura é criado usando os valores padrão quando a primeira tabela no banco de dados é habilitada para captura de dados de alteração e não há publicações transacionais no banco de dados. Quando existir uma publicação transacional, o leitor do log transacional será usado para orientar o mecanismo de captura e um trabalho de captura separado não será nem necessário, nem permitido.  
  
 Como os trabalhos de limpeza e captura são criados por padrão, este procedimento armazenado será necessário somente quando um trabalho tiver sido explicitamente encerrado e tiver de ser recriado.  
  
 É o nome do trabalho **cdc.**  _\<banco de dados\_nome\>_**\_limpeza** ou **cdc.**  _\<banco de dados\_nome\>_**\_capturar**, onde *< database_name >* é o nome do banco de dados atual. Se um trabalho com o mesmo nome já existir, o nome é anexado com um ponto (**.**) seguido por um identificador exclusivo, por exemplo: **cdc. AdventureWorks_capture. A1ACBDED-13FC-428C-8302-10100EF74F52**.  
  
 Para exibir a configuração atual de um trabalho de limpeza ou captura, use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md). Para alterar a configuração de um trabalho, use [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **db_owner** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-capture-job"></a>A. Criando um trabalho de captura  
 O seguinte exemplo cria um trabalho de captura. Este exemplo parte do pressuposto de que o trabalho de limpeza existente foi explicitamente encerrado e deve ser recriado. O trabalho é criado usando os valores padrão.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>B. Criando um trabalho de limpeza  
 O exemplo a seguir cria um trabalho de limpeza no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O parâmetro `@start_job` é definido em 0 e `@retention` é definido em 5760 minutos (96 horas). Este exemplo parte do pressuposto de que o trabalho de limpeza existente foi explicitamente encerrado e deve ser recriado.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>Consulte também  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
