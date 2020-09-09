---
title: sp_replmonitorsubscriptionpendingcmds (T-SQL)
description: Descreve o sp_replmonitorsubscriptionpendingcmds procedimento armazenado que retorna informações sobre o número de comandos pendentes para uma assinatura de uma publicação transacional.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6b83c6492f065f29335bc4665156c02a18367795
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534892"
---
# <a name="sp_replmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Retorna informações sobre o número de comandos pendentes de uma assinatura de publicação transacional e uma estimativa aproximada de quanto tempo é necessário para processá-las. Esse procedimento armazenado retorna uma linha para cada assinatura retornada. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'` É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'` É o nome do Assinante. o *assinante* é **sysname**, sem padrão.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, sem padrão.  
  
`[ @subscription_type = ] subscription_type` Se o tipo de assinatura. *publication_type* é **int**, sem padrão e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Assinatura push.|  
|**1**|Assinatura pull|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|O número de comandos pendentes para a assinatura.|  
|**estimatedprocesstime**|**int**|Estimativa do número de segundos requerido para entregar todos os comandos pendentes ao Assinante.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorsubscriptionpendingcmds** é usado com a replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor ou membros da função de banco de dados fixa **db_owner** no banco de dados de distribuição podem executar **sp_replmonitorsubscriptionpendingcmds**. Os membros da lista de acesso à publicação para uma publicação que usa o banco de dados de distribuição podem executar **sp_replmonitorsubscriptionpendingcmds** para retornar comandos pendentes para essa publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
