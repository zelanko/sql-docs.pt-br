---
title: sp_purge_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 1807fb797b7bd3d53f83cae60c4b876fcb91b74f
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393979"
---
# <a name="sppurgejobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove os registros históricos de um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_name=** ] **'***job_name***'**  
 O nome do trabalho para o qual os registros históricos serão excluídos. *job_name*está **sysname**, com um padrão NULL. Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
> [!NOTE]  
>  Membros do **sysadmin** fixo de função de servidor ou os membros da **SQLAgentOperatorRole** banco de dados fixa podem executar **sp_purge_jobhistory** sem especificar um *job_name* ou *job_id*. Quando **sysadmin** os usuários não especificarem esses argumentos, o histórico de trabalhos para todos os trabalhos locais e multisservidor será excluído no tempo especificado por *oldest_date*. Quando **SQLAgentOperatorRole** os usuários não especificarem esses argumentos, o histórico de trabalhos de todos os trabalhos locais será excluído no tempo especificado por *oldest_date*.  
  
 [ **@job_id=** ] *job_id*  
 O número de identificação do trabalho cujos registros serão excluídos. *job_id*está **uniqueidentifier**, com um padrão NULL. Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados. Consulte a observação na descrição da **@job_name** para obter informações sobre como **sysadmin** ou **SQLAgentOperatorRole** os usuários podem usar esse argumento.  
  
 [ **@oldest_date** = ] *oldest_date*  
 O registro mais antigo a ser retido no histórico. *oldest_date* está **datetime**, com um padrão NULL. Quando *oldest_date* for especificado, **sp_purge_jobhistory** remove somente os registros mais antigos que o valor especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Remarks  
 Quando **sp_purge_jobhistory** concluída com êxito, uma mensagem será retornada.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros dos **sysadmin** função de servidor fixa ou o **SQLAgentOperatorRole** função fixa de banco de dados pode executar esse procedimento armazenado. Os membros **sysadmin** podem limpar o histórico de trabalho para todos os trabalhos locais e multisservidor. Os membros **SQLAgentOperatorRole** podem limpar o histórico de trabalho para todos os trabalhos locais apenas.  
  
 Outros usuários, incluindo os membros **SQLAgentUserRole** e os membros **SQLAgentReaderRole**, deve ser concedido explicitamente a permissão EXECUTE em **sp_purge_jobhistory**. Depois de receber a permissão EXECUTE nesse procedimento armazenado, esses usuários poderão limpar somente o histórico dos trabalhos que eles possuam.  
  
 O **SQLAgentUserRole**, **SQLAgentReaderRole**, e **SQLAgentOperatorRole** funções fixas de banco de dados estão no **msdb** banco de dados. Para obter detalhes sobre suas permissões, consulte [funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. Remover histórico de um trabalho específico  
 O exemplo a seguir remove o histórico de um trabalho denominado `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. Remover histórico de todos os trabalhos  
  
> [!NOTE]  
>  Somente os membros do **sysadmin** fixo de função de servidor e os membros a **SQLAgentOperatorRole** podem remover o histórico de todos os trabalhos. Quando **sysadmin** usuários executar esse procedimento armazenado sem parâmetros, o histórico de trabalhos para todos os trabalhos locais e multisservidor será limpo. Quando **SQLAgentOperatorRole** usuários executar esse procedimento armazenado sem parâmetros, somente o histórico de trabalho para todos os trabalhos locais será limpo.  
  
 O exemplo a seguir executa o procedimento sem parâmetros para remover todos os registros históricos.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
