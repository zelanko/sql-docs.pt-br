---
title: sp_purge_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ad5e7a1d03dde408da52ca2b5ebe6b40f10c06c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72313763"
---
# <a name="sp_purge_jobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove os registros de histórico de um trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_name = ] 'job_name'`O nome do trabalho para o qual os registros de histórico são excluídos. *job_name*é **sysname**, com um padrão de NULL. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
> [!NOTE]  
>  Os membros da função de servidor fixa **sysadmin** ou os membros da função de banco de dados fixa **SQLAgentOperatorRole** podem executar **sp_purge_jobhistory** sem especificar um *job_name* ou *job_id*. Quando os usuários do **sysadmin** não especificam esses argumentos, o histórico de trabalhos de todos os trabalhos locais e multisservidor é excluído dentro do tempo especificado pelo *oldest_date*. Quando os usuários do **SQLAgentOperatorRole** não especificam esses argumentos, o histórico de trabalhos de todos os trabalhos locais é excluído dentro do tempo especificado pelo *oldest_date*.  
  
`[ @job_id = ] job_id`O número de identificação do trabalho para os registros a serem excluídos. *job_id* é **uniqueidentifier**, com um padrão de NULL. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados. Consulte a observação na descrição de ** \@job_name** para obter informações sobre como os usuários **sysadmin** ou **SQLAgentOperatorRole** podem usar esse argumento.  
  
`[ @oldest_date = ] oldest_date`O registro mais antigo a ser mantido no histórico. *oldest_date* é **DateTime**, com um padrão de NULL. Quando *oldest_date* é especificado, **sp_purge_jobhistory** remove apenas os registros que são mais antigos que o valor especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Quando **sp_purge_jobhistory** for concluída com êxito, uma mensagem será retornada.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **SQLAgentOperatorRole** podem executar esse procedimento armazenado. Os membros do **sysadmin** podem limpar o histórico de trabalhos para todos os trabalhos locais e multisservidor. Os membros de **SQLAgentOperatorRole** podem limpar o histórico de trabalhos somente para todos os trabalhos locais.  
  
 Outros usuários, incluindo membros de **SQLAgentUserRole** e membros de **SQLAgentReaderRole**, devem receber explicitamente a permissão EXECUTE em **sp_purge_jobhistory**. Depois de receber a permissão EXECUTE nesse procedimento armazenado, esses usuários poderão limpar somente o histórico dos trabalhos que eles possuam.  
  
 As funções de banco de dados fixas **SQLAgentUserRole**, **SQLAgentReaderRole**e **SQLAgentOperatorRole** estão no banco de dados **msdb** . Para obter detalhes sobre suas permissões, consulte [SQL Server Agent funções de banco de dados fixas](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-remove-history-for-a-specific-job"></a>a. Remover histórico de um trabalho específico  
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
>  Somente os membros da função de servidor fixa **sysadmin** e os membros de **SQLAgentOperatorRole** podem remover o histórico de todos os trabalhos. Quando os usuários do **sysadmin** executam esse procedimento armazenado sem parâmetros, o histórico de trabalhos de todos os trabalhos locais e multisservidor é limpo. Quando os usuários do **SQLAgentOperatorRole** executam esse procedimento armazenado sem parâmetros, somente o histórico de trabalhos de todos os trabalhos locais é limpo.  
  
 O exemplo a seguir executa o procedimento sem parâmetros para remover todos os registros históricos.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_help_job](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_jobhistory](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
