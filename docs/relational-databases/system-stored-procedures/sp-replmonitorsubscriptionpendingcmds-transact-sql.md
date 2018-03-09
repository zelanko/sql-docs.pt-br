---
title: sp_replmonitorsubscriptionpendingcmds (Transact-SQL) | Microsoft Docs
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
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c135e779e1d1f6fd0b5da12f3b9a24f2ade96eea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spreplmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre o número de comandos pendentes de uma assinatura de publicação transacional e uma estimativa aproximada de quanto tempo é necessário para processá-las. Esse procedimento armazenado retorna uma linha para cada assinatura retornada. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher**  =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 É o nome do banco de dados publicado. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication**  =] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@subscriber**  =] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, sem padrão.  
  
 [  **@subscriber_db**  =] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, sem padrão.  
  
 [  **@subscription_type**  =] *subscription_type*  
 Se o tipo de assinatura. *publication_type* é **int**, sem padrão e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Assinatura push.|  
|**1**|Assinatura Pull|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|O número de comandos pendentes para a assinatura.|  
|**estimatedprocesstime**|**int**|Estimativa do número de segundos requerido para entregar todos os comandos pendentes ao Assinante.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorsubscriptionpendingcmds** é usado com replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** a função de servidor fixa no distribuidor ou membros do **db_owner** função de banco de dados fixa no banco de dados de distribuição pode executar **SP _ replmonitorsubscriptionpendingcmds**. A lista de membros de acesso à publicação de uma publicação que usa o banco de dados de distribuição pode executar **sp_replmonitorsubscriptionpendingcmds** para retornar comandos pendentes para aquela publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
