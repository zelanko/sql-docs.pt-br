---
description: sp_start_job (Transact-SQL)
title: sp_start_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e7a86d9ea25b4d9ae412b922cc6f36ddce27c20
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545930"
---
# <a name="sp_start_job-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a executar um trabalho imediatamente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_name = ] 'job_name'` O nome do trabalho a ser iniciado. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados. *job_name* é **sysname**, com um padrão de NULL.  
  
`[ @job_id = ] job_id` O número de identificação do trabalho a ser iniciado. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'` O servidor de destino no qual iniciar o trabalho. *server_name* é **nvarchar (128)**, com um padrão de NULL. *server_name* deve ser um dos servidores de destino aos quais o trabalho está atualmente direcionado.  
  
`[ @step_name = ] 'step_name'` O nome da etapa na qual começar a execução do trabalho. Aplica-se apenas a trabalhos locais. *step_name* é **sysname**, com um padrão de NULL  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Esse procedimento armazenado está no banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** e **SQLAgentReaderRole** só podem iniciar trabalhos que possuem. Os membros de **SQLAgentOperatorRole** podem iniciar todos os trabalhos locais, incluindo aqueles que pertencem a outros usuários. Os membros do **sysadmin** podem iniciar todos os trabalhos locais e multisservidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir inicia um trabalho denominado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_delete_job ](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_job ](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_stop_job ](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_job ](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
