---
title: sp_cdc_scan (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbde9d47ae848ed52a9feeb81329f68456330c79
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysspcdcscan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Executa a operação de verificação no log Change Data Capture.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@maxtrans=** ] *max_trans*  
 O número máximo de transações a processar em cada ciclo de exame. *max_trans* é **int** com um padrão de 500.  
  
 [  **@maxscans=** ] *max_scans*  
 O número máximo de ciclos de exame a executar para extrair todas as linhas do log. *max_scans* é **int** com um padrão de 10.  
  
 [  **@continuous=** ] *contínua*  
 Indica se o procedimento armazenado deve terminar depois da execução de um único ciclo de verificação (0) ou executado continuamente, pausando na hora especificada pelo *intervalo_de_sondagem* antes de executar novamente o ciclo de verificação (1). *contínua* é **tinyint** com um padrão de 0.  
  
 [  **@pollinginterval=** ] *intervalo_de_sondagem*  
 Número de segundos entre ciclos de exame de log. *intervalo_de_sondagem* é **bigint** com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 sys.sp_cdc_scan será chamado internamente pelo sys.sp_MScdc_capture_job, se o trabalho de captura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estiver sendo usado pelo Change Data Capture. O procedimento não pode ser executado explicitamente quando uma operação de verificação de log do change data capture já estiver ativa ou quando o banco de dados está habilitado para replicação transacional. Esse procedimento armazenado deve ser usado por administradores que desejam personalizar o comportamento do trabalho de captura que é configurado automaticamente.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte também  
 [cdc_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
