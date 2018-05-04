---
title: sp_purge_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2072d059f76f6268fd0a94ccecf47390399d64af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 O nome do trabalho para o qual os registros históricos serão excluídos. *job_name*é **sysname**, com um padrão NULL. O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
> [!NOTE]  
>  Membros do **sysadmin** fixo de função de servidor ou os membros do **SQLAgentOperatorRole** pode executar a função de banco de dados fixa **sp_purge_jobhistory** sem especificar um *job_name* ou *job_id*. Quando **sysadmin** os usuários não especificarem esses argumentos, o histórico do trabalho para todos os trabalhos locais e multisservidor será excluído no tempo especificado por *oldest_date*. Quando **SQLAgentOperatorRole** os usuários não especificarem esses argumentos, o histórico do trabalho para todos os trabalhos locais será excluído no tempo especificado por *oldest_date*.  
  
 [ **@job_id=** ] *job_id*  
 O número de identificação do trabalho cujos registros serão excluídos. *job_id*é **uniqueidentifier**, com um padrão NULL. O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos. Consulte a observação na descrição do **@job_name** para obter informações sobre como **sysadmin** ou **SQLAgentOperatorRole** os usuários podem usar esse argumento.  
  
 [ **@oldest_date** = ] *oldest_date*  
 O registro mais antigo a ser retido no histórico. *oldest_date* é **datetime**, com um padrão NULL. Quando *oldest_date* for especificado, **sp_purge_jobhistory** remove somente os registros mais antigos que o valor especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Quando **sp_purge_jobhistory** for concluído com êxito, uma mensagem será retornada.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros do **sysadmin** função de servidor fixa ou **SQLAgentOperatorRole** banco de dados fixa podem executar esse procedimento armazenado. Membros de **sysadmin** podem limpar o histórico de trabalho para todos os trabalhos locais e multisservidor. Membros de **SQLAgentOperatorRole** podem limpar o histórico de trabalho para todos os trabalhos locais apenas.  
  
 Outros usuários, incluindo membros de **SQLAgentUserRole** e membros de **SQLAgentReaderRole**, deve ser concedida explicitamente a permissão EXECUTE em **sp_purge_jobhistory**. Depois de receber a permissão EXECUTE nesse procedimento armazenado, esses usuários poderão limpar somente o histórico dos trabalhos que eles possuam.  
  
 O **SQLAgentUserRole**, **SQLAgentReaderRole**, e **SQLAgentOperatorRole** funções fixas de banco de dados estão no **msdb** banco de dados. Para obter detalhes sobre suas permissões, consulte [funções de banco de dados fixa do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
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
>  Somente membros do **sysadmin** fixo de função de servidor e membros do **SQLAgentOperatorRole** pode remover o histórico de todos os trabalhos. Quando **sysadmin** usuários executar esse procedimento armazenado sem parâmetros, o histórico do trabalho para todos os trabalhos locais e multisservidor será limpo. Quando **SQLAgentOperatorRole** usuários executar esse procedimento armazenado sem parâmetros, apenas o histórico do trabalho para todos os trabalhos locais será limpo.  
  
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
  
  
