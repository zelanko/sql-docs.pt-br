---
description: sp_deletepeerrequesthistory (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 11773aa1e2a03ccc9b729c902a99cda10088c718
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474334"
---
# <a name="sp_deletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui o histórico relacionado a uma solicitação de status de publicação, que inclui o histórico de solicitações ([MSpeer_request &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/mspeer-request-transact-sql.md)), bem como o histórico de respostas ([MSpeer_response &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/mspeer-response-transact-sql.md)). Esse procedimento armazenado é executado no banco de dados de publicação em um Publicador que participa de uma topologia de replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Nome da publicação para a qual a solicitação de status foi feita. a *publicação* é **sysname**, sem padrão.  
  
`[ @request_id = ] request_id` Especifica uma solicitação de status individual para que todas as respostas a essa solicitação sejam excluídas. *request_id* é **int**, com um valor padrão de NULL.  
  
`[ @cutoff_date = ] cutoff_date` Especifica uma data de corte, antes da qual todos os registros de resposta anteriores são excluídos. *cutoff_date* é **DateTime**, com um valor padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_deletepeerrequesthistory** é usado em uma topologia de replicação transacional ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Ao executar **sp_deletepeerrequesthistory**, *request_id* ou *cutoff_date* deve ser especificado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_deletepeerrequesthistory**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_helppeerrequests ](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppeerresponses ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_requestpeerresponse ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
