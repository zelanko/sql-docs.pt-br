---
title: sp_add_jobserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobserver
- sp_add_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobserver
ms.assetid: 485252cc-0081-490a-9bd1-cbbd68eea286
author: stevestein
ms.author: sstein
ms.openlocfilehash: bc4d3bca563079c7e1dd7f3ee93e5947f65700b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72305239"
---
# <a name="sp_add_jobserver-transact-sql"></a>sp_add_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tem como destino o trabalho especificado no servidor especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_jobserver [ @job_id = ] job_id | [ @job_name = ] 'job_name'  
     [ , [ @server_name = ] 'server' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @server_name = ] 'server'`O nome do servidor no qual direcionar o trabalho. o *servidor* é **nvarchar (30)**, com um padrão de N ' (local) '. o *servidor* pode ser **(local)** para um servidor local ou o nome de um servidor de destino existente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 automatic_post existe em **sp_add_jobserver**, mas não está listado em argumentos. ** \@** automatic_post é reservado para uso interno. ** \@**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_add_jobserver** para trabalhos que envolvem vários servidores.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-assigning-a-job-to-the-local-server"></a>a. Atribuindo um trabalho ao servidor local  
 O exemplo a seguir atribui o trabalho `NightlyBackups` para ser executado no servidor local.  
  
> [!NOTE]  
>  Este exemplo supõe que o `NightlyBackups` trabalho já existe.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-assigning-a-job-to-run-on-a-different-server"></a>B. Atribuindo um trabalho para ser executado em um servidor diferente  
 O exemplo a seguir atribui o trabalho de vários servidores `Weekly Sales Backups` ao servidor `SEATTLE2`.  
  
> [!NOTE]  
>  Este exemplo assume que o trabalho `Weekly Sales Backups` já exista e que `SEATTLE2` esteja registrado como um servidor de destino para a instância atual.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
