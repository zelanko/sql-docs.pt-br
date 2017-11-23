---
title: sp_cdc_start_job (Transact-SQL) | Microsoft Docs
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
- sp_cdc_start_job
- sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job
dev_langs: TSQL
helpviewer_keywords: sp_cdc_start_job
ms.assetid: cf443a67-7705-4799-9f39-0e3a6a8a0708
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aeecac9fcbdc7356280128842d96a4abe1809bb3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysspcdcstartjob-transact-sql"></a>sys.sp_cdc_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma limpeza do Change Data Capture ou o trabalho de captura do banco de dados atual.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_start_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [[  **@job_type=** ] **'***job_type***'** ]  
 Tipo de trabalho a adicionar. *job_type* é **nvarchar (20)** com um padrão de **capturar**. As entradas válidas são **capturar** e **limpeza**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 sys.sp_cdc_start_job pode ser usado por um administrador para iniciar explicitamente o trabalho de captura ou de limpeza.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-starting-a-capture-job"></a>A. Iniciando um trabalho de captura  
 O exemplo a seguir inicia o trabalho de captura para o banco de dados `AdventureWorks2012`. Especificar um valor para *job_type* não é necessário porque o tipo de trabalho padrão é **capturar**.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_start_job;  
GO  
```  
  
### <a name="b-starting-a-cleanup-job"></a>B. Iniciando um trabalho de limpeza  
 O exemplo a seguir inicia um trabalho de limpeza para o banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_start_job @job_type = N'cleanup';  
```  
  
## <a name="see-also"></a>Consulte também  
 [cdc_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_stop_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)  
  
  
