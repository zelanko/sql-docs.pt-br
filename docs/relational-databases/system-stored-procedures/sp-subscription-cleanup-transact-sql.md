---
description: sp_subscription_cleanup (Transact-SQL)
title: sp_subscription_cleanup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_subscription_cleanup_TSQL
- sp_subscription_cleanup
helpviewer_keywords:
- sp_subscription_cleanup
ms.assetid: bdc8aaa0-ff2d-40c2-84b2-4ba513ced279
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d75293627b229b942e6d81753320a4bbb0fffbf9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489068"
---
# <a name="sp_subscription_cleanup-transact-sql"></a>sp_subscription_cleanup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove metadados quando uma assinatura é descartada em um Assinante. Para uma assinatura de transação de sincronização, inclui também gatilhos de atualização imediata. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_subscription_cleanup [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
    [ , [ @publication = ] 'publication']  
    [ , [ @reserved = ] 'reserved']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, com um padrão de NULL. Se for NULL, assinaturas que usam uma publicação de agente compartilhada no banco de dados de publicação serão excluídas.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_subscription_cleanup** é usado em replicação transacional e de instantâneo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_subscription_cleanup**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_expired_subscription_cleanup ](../../relational-databases/system-stored-procedures/sp-expired-subscription-cleanup-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_mergesubscription_cleanup ](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
