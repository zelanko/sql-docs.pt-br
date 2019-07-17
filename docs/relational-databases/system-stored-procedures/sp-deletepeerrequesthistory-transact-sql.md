---
title: sp_deletepeerrequesthistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords:
- sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
author: stevestein
ms.author: sstein
ms.openlocfilehash: e1af3aad1f66f3de7dd2fce44990718980018d3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111941"
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui histórico relacionado a uma solicitação de status de publicação, que inclui o histórico de solicitações ([MSpeer_request &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)), bem como o histórico de resposta ([MSpeer_response &#40; Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md)). Esse procedimento armazenado é executado no banco de dados de publicação em um publicador participante em uma topologia de replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Nome da publicação para o qual a solicitação de status foi feita. *publicação* está **sysname**, sem padrão.  
  
`[ @request_id = ] request_id` Especifica uma solicitação de status individuais, para que todas as respostas a essa solicitação sejam excluídas. *request_id* está **int**, com um valor padrão de NULL.  
  
`[ @cutoff_date = ] cutoff_date` Especifica uma data de corte antes da qual todos os registros de resposta anteriores são excluídos. *cutoff_date* está **datetime**, com um valor padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_deletepeerrequesthistory** é usado em uma topologia de replicação transacional ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Ao executar **sp_deletepeerrequesthistory**, ambos *request_id* ou *cutoff_date* deve ser especificado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_deletepeerrequesthistory**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
