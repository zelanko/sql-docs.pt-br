---
title: sp_stop_job (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1276a936bece39cc875e5f80e8da5465f51bb4ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a parar a execução de um trabalho.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_name =**] **'***job_name***'**  
 O nome do trabalho a ser interrompido. *job_name* é **sysname**, com um padrão NULL.  
  
 [ **@job_id =**] *job_id*  
 O número de identificação do trabalho a ser interrompido. *job_id* é **uniqueidentifier**, com um padrão NULL.  
  
 [ **@originating_server =**] **'***master_server***'**  
 O nome do servidor mestre. Se for especificado, todos os trabalhos multisservidor serão interrompidos. *master_server* é **nvarchar (128)**, com um padrão NULL. Especifique esse parâmetro somente ao chamar **sp_stop_job** em um servidor de destino.  
  
> [!NOTE]  
>  Apenas um dos três primeiros parâmetros pode ser especificado.  
  
 [ **@server_name =**] **'***target_server***'**  
 O nome do servidor de destino específico no qual um trabalho multisservidor será interrompido. *target_server* é **nvarchar (128)**, com um padrão NULL. Especifique esse parâmetro somente ao chamar **sp_stop_job** em um servidor mestre para um trabalho multisservidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_stop_job** envia um sinal de encerramento para o banco de dados. Alguns processos podem ser interrompidos imediatamente e alguns devem atingir um ponto estável (ou um ponto de entrada para o caminho de código) antes de eles podem parar. Algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] longas como BACKUP, RESTORE e alguns comandos DBCC podem levar muito tempo para terminar. Quando eles estão em execução, ele pode demorar um pouco antes do trabalho foi cancelado. A interrupção de um trabalho faz com que uma entrada "Trabalho Cancelado" seja registrada no histórico de trabalho.  
  
 Se um trabalho está executando uma etapa do tipo **CmdExec** ou **PowerShell**, o processo está sendo executado (por exemplo, MyProgram.exe) será forçado a terminar prematuramente. O fim prematuro pode resultar em comportamento imprevisível, como arquivos em uso pelo processo serem mantidos abertos. Consequentemente, **sp_stop_job** deve ser usado somente em circunstâncias extremas se o trabalho contiver etapas do tipo **CmdExec** ou **PowerShell**.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Membros de **SQLAgentUserRole** e **SQLAgentReaderRole** só podem parar trabalhos que possuem. Membros de **SQLAgentOperatorRole** pode interromper todos os trabalhos locais, incluindo os pertencentes a outros usuários. Membros de **sysadmin** podem parar todos os trabalhos locais e multisservidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir para um trabalho denominado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
