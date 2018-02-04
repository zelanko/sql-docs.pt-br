---
title: dbo.sysjobsteps (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f29d3ef22b724abc095da01ea5eef70aa9c447dd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém as informações de cada etapa em um trabalho a ser executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Identificação do trabalho.|  
|**step_id**|**Int**|ID da etapa no trabalho.|  
|**step_name**|**sysname**|Nome da etapa do trabalho.|  
|**subsystem**|**nvarchar(40)**|Nome do subsistema usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar a etapa de trabalho.|  
|**command**|**nvarchar(max)**|O comando a ser executado pelo **subsistema**.|  
|**flags**|**Int**|Reservado.|  
|**additional_parameters**|**ntext**|Reservado.|  
|**cmdexec_success_code**|**Int**|Valor de nível de erro retornado pelo **CmdExec** etapas do subsistema para indicar êxito.|  
|**on_success_action**|**tinyint**|Ação a ser executada quando uma etapa é executada com êxito.|  
|**on_success_step_id**|**Int**|ID da próxima etapa a ser executada quando uma etapa for executada com êxito.|  
|**on_fail_action**|**tinyint**|Ação a ser executada quando uma etapa não é executada com êxito.|  
|**on_fail_step_id**|**Int**|ID da próxima etapa a ser executada quando uma etapa não for executada com êxito.|  
|**server**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Nome do banco de dados no qual **comando** será executada se **subsistema** for TSQL.|  
|**database_user_name**|**sysname**|Nome do usuário de banco de dados cuja conta será usada ao executar a etapa.|  
|**retry_attempts**|**Int**|Número de novas tentativas feitas se a etapa apresentar falha.|  
|**retry_interval**|**Int**|Quantidade de tempo a ser aguardada entre as novas tentativas.|  
|**os_run_priority**|**Int**|Reservado.|  
|**output_file_name**|**nvarchar(200)**|Nome do arquivo no qual a saída da etapa será salva quando **subsistema** é TSQL, PowerShell ou **CmdExec *.*|  
|**last_run_outcome**|**Int**|Resultado da execução anterior da etapa do trabalho.<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **2** = repetir<br /><br /> **3** = cancelada<br /><br /> **5** = desconhecido|  
|**last_run_duration**|**Int**|Duração (hhmmss) da etapa na última vez que foi executada.|  
|**last_run_retries**|**Int**|Número de novas tentativas na última execução da etapa do trabalho.|  
|**last_run_date**|**Int**|Data (yyyymmdd) da última execução iniciada da etapa.|  
|**last_run_time**|**Int**|Hora (yyyymmdd) da última execução iniciada da etapa.|  
|**proxy_id**|**Int**|Proxy da etapa do trabalho.|  
|**step_uid**|**uniqueidentifier**|Identificador da etapa do trabalho.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas do SQL Server Agent &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
