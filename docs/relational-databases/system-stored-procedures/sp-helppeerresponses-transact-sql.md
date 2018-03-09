---
title: sp_helppeerresponses (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44abb0462f6360ea1823383f318c41998240545e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppeerresponses-transact-sql"></a>sp_helppeerresponses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna todas as respostas a uma solicitação de status específica recebida de um participante em uma topologia de replicação ponto a ponto, em que a solicitação foi iniciada pela execução [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) em qualquer banco de dados publicado na topologia. Esse procedimento armazenado é executado no banco de dados de publicação em um Publicador que participa de uma topologia de replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@request_id** =] *request_id*  
 É a ID de uma solicitação de status específica. *request_id* é **int**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|ID da solicitação de status.|  
|**ponto a ponto**|**sysname**|O nome do nível correspondente que gerou a resposta.|  
|**peer_db**|**sysname**|O nome do banco de dados no nível que gerou a resposta.|  
|**received_date**|**datetime**|A data e a hora em que o solicitante recebeu a resposta do par que a enviou.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helppeerresponses** é usado em replicação transacional ponto a ponto.  
  
 **sp_helppeerresponses** procedimento é usado ao restaurar um banco de dados publicado em uma topologia ponto a ponto.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_helppeerresponses**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_deletepeerrequesthistory &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
