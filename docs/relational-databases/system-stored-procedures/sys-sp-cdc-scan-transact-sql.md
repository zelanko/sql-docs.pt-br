---
title: sys. sp_cdc_scan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 84e404ffb9459abc3f0ab2a7a1604d3f4c5609a8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827410"
---
# <a name="syssp_cdc_scan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Executa a operação de verificação no log Change Data Capture.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @maxtrans = ] max_trans`Número máximo de transações a serem processadas em cada ciclo de verificação. *max_trans* é **int** com um padrão de 500.  
  
`[ @maxscans = ] max_scans`Número máximo de ciclos de verificação a serem executados para extrair todas as linhas do log. *max_scans* é **int** com um padrão de 10.  
  
`[ @continuous = ] continuous`Indica se o procedimento armazenado deve terminar após a execução de um ciclo de verificação único (0) ou ser executado continuamente, pausando o tempo especificado pelo *polling_interval* antes de executar novamente o ciclo de verificação (1). *continuou* é **tinyint** com um padrão de 0.  
  
`[ @pollinginterval = ] polling_interval`Número de segundos entre os ciclos de verificação de log. *polling_interval* é **bigint** com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 sys.sp_cdc_scan será chamado internamente pelo sys.sp_MScdc_capture_job, se o trabalho de captura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estiver sendo usado pelo Change Data Capture. O procedimento não pode ser executado explicitamente quando uma operação de verificação de log do Change Data Capture já estiver ativa ou quando o banco de dados estiver habilitado para replicação transacional. Este procedimento armazenado deve ser usado por administradores que desejam personalizar o comportamento do trabalho de captura que é configurado automaticamente.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte Também  
 [o dbo. cdc_jobs &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
