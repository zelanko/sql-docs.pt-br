---
title: sp_helppeerrequests (Transact-SQL) | Microsoft Docs
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
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d2ea35c01385de46ded538c98faf701e34d3892
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre todas as solicitações de status recebidas por participantes em uma topologia de replicação ponto a ponto, em que essas solicitações foram inicializadas executando [sp_requestpeerresponse &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) em qualquer banco de dados publicado na topologia. Esse procedimento armazenado é executado no banco de dados de publicação em um Publicador que participa de uma topologia de replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication** =] **'***publicação***'**  
 É o nome da publicação em uma topologia ponto a ponto para a qual as solicitações de status foram enviadas. *publicação* é **sysname**, sem padrão.  
  
 [  **@description** =] **'***descrição***'**  
 Valor que pode ser usado para identificar solicitações de status individuais, que permitem filtrar respostas retornadas com base em informações definidas pelo usuário ao chamar [sp_requestpeerresponse &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *Descrição* é **nvarchar (4000)**, com um padrão de  **%** . Por padrão, todas as solicitações de status para a publicação são retornadas. Esse parâmetro é usado para retornar somente solicitações de status com uma descrição correspondente ao valor fornecido em *descrição*, onde as cadeias de caracteres são correspondidas usando um [como &#40; Transact-SQL &#41; ](../../t-sql/language-elements/like-transact-sql.md) cláusula.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica uma solicitação.|  
|**publicação**|**sysname**|Nome da publicação para a qual a solicitação de status foi enviada.|  
|**sent_date**|**datetime**|Data e hora de envio da solicitação de status.|  
|**Descrição**|**nvarchar(4000)**|Informações que podem ser usadas para identificar solicitações de status individuais definido pelo usuário.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helppeerrequests** é usado em replicação transacional ponto a ponto.  
  
 **sp_helppeerrequests** é usado ao restaurar um banco de dados publicado em uma topologia ponto a ponto.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_helppeerrequests**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_deletepeerrequesthistory &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
