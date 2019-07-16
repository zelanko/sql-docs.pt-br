---
title: sp_browsereplcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
ms.openlocfilehash: b29ee604f1b584fcbdcd0ef91e32c84d89cc5f96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045993"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados em uma versão legível dos comandos replicados armazenados no banco de dados de distribuição, e é usado como ferramenta de diagnóstico. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @xact_seqno_start = ] 'xact_seqno_start'` Especifica o número de sequência exato valor mais baixo para retornar. *xact_seqno_start* está **nchar (22)** , com um padrão de 0x00000000000000000000.  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'` Especifica o número de sequência exato mais alto para retornar. *xact_seqno_end* está **nchar (22)** , com um padrão de 0xFFFFFFFFFFFFFFFFFFFF.  
  
`[ @originator_id = ] 'originator_id'` Especifica se comandos com a especificada *originator_id* são retornados. *originator_id* está **int**, com um padrão NULL.  
  
`[ @publisher_database_id = ] 'publisher_database_id'` Especifica se comandos com a especificada *publisher_database_id* são retornados. *publisher_database_id* está **int**, com um padrão NULL.  
  
`[ @article_id = ] 'article_id'` Especifica se comandos com a especificada *article_id* são retornados. *article_id* está **int**, com um padrão NULL.  
  
`[ @command_id = ] command_id` É o local do comando na [MSrepl_commands &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) a ser decodificado. *command_id* está **int**, com um padrão NULL. Se for especificado, todos os outros parâmetros Além disso, devem ser especificados e *xact_seqno_start*deve ser idêntico ao *xact_seqno_end*.  
  
`[ @agent_id = ] agent_id` Especifica que somente os comandos para um agente de replicação específico são retornados. *agent_id* está **int**, com um valor padrão de NULL.  
  
`[ @compatibility_level = ] compatibility_level` É a versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual o *compatibility_level* está **int**, com um valor padrão de 9000000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Número de sequência do comando.|  
|**originator_srvname**|**sysname**|Servidor onde a transação originou.|  
|**originator_db**|**sysname**|Banco de dados onde a transação originou.|  
|**article_id**|**int**|ID do artigo.|  
|**type**|**int**|Tipo de comando.|  
|**partial_command**|**bit**|Indica se esse é um comando parcial ou não.|  
|**hashkey**|**int**|Somente para uso interno.|  
|**originator_publication_id**|**int**|ID da publicação de origem da transação.|  
|**originator_db_version**|**int**|Versão do banco de dados onde a transação originou.|  
|**originator_lsn**|**varbinary(16)**|Identifica o LSN (número de sequência de log) para o comando na publicação de origem. Usado em replicação transacional ponto a ponto.|  
|**command**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|**command_id**|**int**|ID do comando em [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 Comandos longos podem ser divididos em várias linhas nos conjuntos de resultados.  
  
## <a name="remarks"></a>Comentários  
 **sp_browsereplcmds** é usado em replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** fixo de função de servidor ou os membros da **db_owner** ou **replmonitor** funções de banco de dados fixa no banco de dados de distribuição podem executar **sp_browsereplcmds**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
