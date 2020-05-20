---
title: sys. sp_cdc_start_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_start_job
- sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job_TSQL
- sys.sp_cdc_start_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_start_job
ms.assetid: cf443a67-7705-4799-9f39-0e3a6a8a0708
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c475a13a64defecbd420d297fb5cd513178b47f4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834184"
---
# <a name="syssp_cdc_start_job-transact-sql"></a>sys.sp_cdc_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia uma limpeza do Change Data Capture ou o trabalho de captura do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_start_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ [ @job_type = ] 'job_type' ]`Tipo de trabalho a ser adicionado. *job_type* é **nvarchar (20)** com um padrão de **captura**. As entradas válidas são **Capture** e **Cleanup**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 sys.sp_cdc_start_job pode ser usado por um administrador para iniciar explicitamente o trabalho de captura ou de limpeza.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-starting-a-capture-job"></a>a. Iniciando um trabalho de captura  
 O exemplo a seguir inicia o trabalho de captura para o banco de dados `AdventureWorks2012`. Não é necessário especificar um valor para *job_type* porque o tipo de trabalho padrão é **captura**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [o dbo. cdc_jobs &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys. sp_cdc_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)  
  
  
