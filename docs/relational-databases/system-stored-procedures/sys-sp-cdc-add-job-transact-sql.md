---
title: sys. sp_cdc_add_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7c42d2150a148f1a288c1fa447f4bb1d9020fe09
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261955"
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
 [  **@job_type=** ] **'***job_type***'**  
 Tipo de trabalho a adicionar. *job_type* é **nvarchar (20)** e não pode ser NULL. As entradas válidas são **'capture'** e **'cleanup'**.  
  
 [  **@start_job=** ] *start_job*  
 Sinalizador que indica se o trabalho deve ser iniciado imediatamente depois de adicionado. *start_job* é **bit** com um padrão de 1.  
  
 [ **@maxtrans** ] = *max_trans*  
 O número máximo de transações a processar em cada ciclo de exame. *max_trans* é **int** com um padrão de 500. Se especificado, o valor deve ser um inteiro positivo.  
  
 *max_trans* é válido somente para trabalhos de captura.  
  
 [ **@maxscans** ] **= * max_scans*  
 O número máximo de ciclos de exame a executar para extrair todas as linhas do log. *max_scans* é **int** com um padrão de 10.  
  
 *max_scan* é válido somente para trabalhos de captura.  
  
 [ **@continuous** ] **= * contínua*  
 Indica se o trabalho de captura deve ser executado continuamente (1) ou apenas uma vez (0). *contínua* é **bit** com um padrão de 1.  
  
 Quando *contínua* = 1, o [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) trabalho examina o log e processa até (*max_trans* \* *max_scans*) transações. Ele espera, em seguida, o número de segundos especificado em *intervalo_de_sondagem* antes de começar a próxima verificação de log.  
  
 Quando *contínua* = 0, o **sp_cdc_scan** executa trabalho até *max_scans* verificações do log, processando até *max_trans* transação durante cada verificação e, em seguida, sai.  
  
 *contínua* é válido somente para trabalhos de captura.  
  
 [ **@pollinginterval** ] **= * intervalo_de_sondagem*  
 Número de segundos entre ciclos de exame de log. *intervalo_de_sondagem* é **bigint** com um padrão de 5.  
  
 *intervalo_de_sondagem* é válido somente para captura trabalhos quando *contínua* é definido como 1. Se especificado, o valor não pode ser negativo nem exceder 24 horas. Se um valor 0 estiver especificado, não haverá espera entre os exames de log.  
  
 [ **@retention** ] **= * retenção*  
 O número de minutos que as linhas de alteração de dados serão retidas em tabelas de alteração. *retenção* é **bigint** com um padrão de 4320 (72 horas). O valor máximo é 52494800 (100 anos). Se especificado, o valor deve ser um inteiro positivo.  
  
 *retenção* é válido somente para trabalhos de limpeza.  
  
 [  **@threshold =** ] **'***delete_threshold***'**  
 O número máximo de entradas de exclusão que podem ser excluídas com o uso de uma única instrução na limpeza. *delete_threshold* é **bigint** com um padrão de 5000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Um trabalho de limpeza é criado usando os valores padrão quando a primeira tabela no banco de dados é habilitada para captura de dados de alteração. Um trabalho de captura é criado usando os valores padrão quando a primeira tabela no banco de dados é habilitada para captura de dados de alteração e não há publicações transacionais no banco de dados. Quando existir uma publicação transacional, o leitor do log transacional será usado para orientar o mecanismo de captura e um trabalho de captura separado não será nem necessário, nem permitido.  
  
 Como os trabalhos de limpeza e captura são criados por padrão, este procedimento armazenado será necessário somente quando um trabalho tiver sido explicitamente encerrado e tiver de ser recriado.  
  
 O nome do trabalho é **cdc. ***< nome_do_banco_de_dados >*** CleanUp** ou **cdc. ***< nome_do_banco_de_dados >*** Capture**, onde *< nome_do_banco_de_dados >* é o nome do banco de dados atual. Se um trabalho com o mesmo nome já existir, o nome é anexado com um período (**.**) seguido por um identificador exclusivo, por exemplo: **cdc. AdventureWorks_capture. A1ACBDED-13FC-428C-8302-10100EF74F52**.  
  
 Para exibir a configuração atual de um trabalho de limpeza ou captura, use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md). Para alterar a configuração de um trabalho, use [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **db_owner** função fixa de banco de dados.  
  
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
 [cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
