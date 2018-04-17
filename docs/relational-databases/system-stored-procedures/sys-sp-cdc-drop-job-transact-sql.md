---
title: sp_cdc_drop_job (Transact-SQL) | Microsoft Docs
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
- sys.sp_cdc_drop_job_TSQL
- sp_cdc_drop_job_TSQL
- sp_cdc_drop_job
- sys.sp_cdc_drop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_drop_job
ms.assetid: e8265846-8051-4848-b28e-fac27c10bdeb
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 157b0b02373b18e545d081a8584bdccd66cef539
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysspcdcdropjob-transact-sql"></a>sys.sp_cdc_drop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma limpeza do Change Data Capture ou do trabalho de captura do banco de dados atual do msdb.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_drop_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @job_type **=** ] '*job_type*'  
 Tipo de trabalho a ser removido. *job_type* é **nvarchar (20)** e não pode ser NULL. As entradas válidas são 'capture' e 'cleanup'.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nones  
  
## <a name="remarks"></a>Remarks  
 sp_cdc_drop_job é chamado internamente pelo [sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o trabalho de limpeza do banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_drop_job @job_type = N'cleanup';  
```  
  
## <a name="see-also"></a>Consulte também  
 [cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_disable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)   
 [sys. sp_cdc_add_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
