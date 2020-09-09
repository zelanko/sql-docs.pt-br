---
description: sys.sp_cdc_add_job (Transact-SQL)
title: sys. sp_cdc_add_job (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8a1285df9bf4d7e17e074e3c22f0ff37241c400
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545828"
---
# <a name="syssp_cdc_add_job-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria uma limpeza de captura de dados de alteração ou trabalho de captura no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_type = ] 'job\_type'` Tipo de trabalho a ser adicionado. *job_type* é **nvarchar (20)** e não pode ser NULL. As entradas válidas são **"Capture"** e **"Cleanup"**.  
  
`[ @start_job = ] start_job` Sinalizador que indica se o trabalho deve ser iniciado imediatamente após ser adicionado. *start_job* é **bit** com um padrão de 1.  
  
`[ @maxtrans ] = max_trans` Número máximo de transações a serem processadas em cada ciclo de verificação. *max_trans* é **int** com um padrão de 500. Se especificado, o valor deve ser um inteiro positivo.  
  
 *max_trans* é válido somente para trabalhos de captura.  
  
`[ @maxscans ] = max\_scans_` Número máximo de ciclos de verificação a serem executados para extrair todas as linhas do log. *max_scans* é **int** com um padrão de 10.  
  
 *max_scan* é válido somente para trabalhos de captura.  
  
`[ @continuous ] = continuous_` Indica se o trabalho de captura deve ser executado continuamente (1) ou ser executado apenas uma vez (0). *continuou* é **bit** com um padrão de 1.  
  
 Quando *Continuous* = 1, o trabalho de [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) examina o log e processa até (*max_trans* \* *max_scans*) transações. Em seguida, ele aguarda o número de segundos especificado em *polling_interval* antes de iniciar a próxima verificação de log.  
  
 Quando *Continuous* = 0, o trabalho de **sp_cdc_scan** é executado até *max_scans* verificações do log, processamento de até *max_trans* transação durante cada verificação e, em seguida, é encerrado.  
  
 *contínuo* é válido somente para trabalhos de captura.  
  
`[ @pollinginterval ] = polling\_interval_` Número de segundos entre os ciclos de verificação de log. *polling_interval* é **bigint** com um padrão de 5.  
  
 *polling_interval* é válido somente para trabalhos de captura quando a *contínua* é definida como 1. Se especificado, o valor deve ser maior ou igual a 0 e menor que 24 horas (máx: 86399 segundos). Se um valor 0 estiver especificado, não haverá espera entre os exames de log.  
  
`[ @retention ] = retention_` Número de minutos que as linhas de dados de alteração devem ser retidas em tabelas de alterações. a *retenção* é **bigint** com um padrão de 4320 (72 horas). O valor máximo é 52494800 (100 anos). Se especificado, o valor deve ser um inteiro positivo.  
  
 a *retenção* é válida somente para trabalhos de limpeza.  
  
`[ @threshold = ] 'delete\_threshold'` Número máximo de entradas de exclusão que podem ser excluídas usando uma única instrução na limpeza. *delete_threshold* é **bigint** com um padrão de 5000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Um trabalho de limpeza é criado usando os valores padrão quando a primeira tabela no banco de dados é habilitada para captura de dados de alteração. Um trabalho de captura é criado usando os valores padrão quando a primeira tabela no banco de dados é habilitada para captura de dados de alteração e não há publicações transacionais no banco de dados. Quando existir uma publicação transacional, o leitor do log transacional será usado para orientar o mecanismo de captura e um trabalho de captura separado não será nem necessário, nem permitido.  
  
 Como os trabalhos de limpeza e captura são criados por padrão, este procedimento armazenado será necessário somente quando um trabalho tiver sido explicitamente encerrado e tiver de ser recriado.  
  
 O nome do trabalho é **CDC.** _\<database\_name\>_ ** \_ limpeza** ou **CDC.** _\<database\_name\>_ ** \_ Capture**, em que *<database_name>* é o nome do banco de dados atual. Se já existir um trabalho com o mesmo nome, o nome será anexado com um ponto final (**.**) seguido por um identificador exclusivo, por exemplo: **CDC. AdventureWorks_capture. A1ACBDED-13FC-428C-8302-10100EF74F52**.  
  
 Para exibir a configuração atual de um trabalho de limpeza ou de captura, use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md). Para alterar a configuração de um trabalho, use [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-capture-job"></a>a. Criando um trabalho de captura  
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
  
## <a name="see-also"></a>Consulte Também  
 [o dbo. cdc_jobs &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys. sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
