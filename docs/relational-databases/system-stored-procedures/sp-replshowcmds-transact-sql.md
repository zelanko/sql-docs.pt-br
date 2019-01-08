---
title: sp_replshowcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18ccbda41c5b7683c33bc0258a05738ab227ec69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813309"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os comandos para transações marcadas para replicação em formato legível. **sp_replshowcmds** pode ser executado apenas quando as conexões de cliente (incluindo a conexão atual) não estão lendo transações replicadas do log. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@maxtrans** =] *maxtrans*  
 É o número de transações sobre as quais retornar informações. *maxtrans* está **int**, com um padrão de **1**, que especifica o número máximo de transações pendentes de replicação para o qual **sp_replshowcmds** Retorna informações.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_replshowcmds** é um procedimento de diagnóstico que retorna informações sobre o banco de dados de publicação do qual ele é executado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|Número de sequência do comando.|  
|**originator_id**|**int**|ID do originador do comando, sempre **0**.|  
|**publisher_database_id**|**int**|ID do banco de dados publicador, sempre **0**.|  
|**article_id**|**int**|ID do artigo.|  
|**type**|**int**|Tipo de comando.|  
|**command**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="remarks"></a>Comentários  
 **sp_replshowcmds** é usado em replicação transacional.  
  
 Usando o **sp_replshowcmds**, você pode exibir transações atualmente não distribuídas (aquelas transações permanecem no log de transações que não foram enviadas ao distribuidor).  
  
 Clientes que executam **sp_replshowcmds** e **sp_replcmds** dentro do mesmo banco de dados recebem erro 18752.  
  
 Para evitar esse erro, o primeiro cliente deve ser desconectado ou a função do cliente como o leitor de log deve ser liberada, executando **sp_replflush**. Depois que todos os clientes foram desconectados do log reader **sp_replshowcmds** pode ser executado com êxito.  
  
> [!NOTE]  
>  **sp_replshowcmds** deve ser executado apenas para solucionar problemas de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_replshowcmds**.  
  
## <a name="see-also"></a>Consulte também  
 [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
