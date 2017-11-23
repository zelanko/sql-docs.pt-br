---
title: "ELIMINAR assinatura de notificação de consulta (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bcb57bef390c6aa6e3debd5592ee7030c5c6b645
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove as assinaturas de notificação de consulta da instância. Essa instrução pode remover uma assinatura específica ou todas as assinaturas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>Argumentos  
 ALL  
 Remove todas as assinaturas na instância.  
  
 *SUBSCRIPTION_ID*  
 Remove a assinatura com a id da assinatura *subscription_id*.  
  
## <a name="remarks"></a>Comentários  
 A instrução KILL QUERY NOTIFICATION SUBSCRIPTION remove assinaturas de notificação de consulta sem produzir uma mensagem de notificação.  
  
 *SUBSCRIPTION_ID* é a id da assinatura, conforme mostrado na exibição de gerenciamento dinâmico [sys.DM qn_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 Se a identificação de assinatura especificada não existir, a instrução produzirá um erro.  
  
## <a name="permissions"></a>Permissões  
 Permissão para executar essa instrução é restrito a membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>A. Removendo todas as assinaturas de notificação de consulta na instância.  
 O exemplo a seguir remove todas as assinaturas de notificação de consulta na instância.  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. Removendo uma única assinatura de notificação de consulta  
 O exemplo a seguir remove a assinatura de notificação da consulta com a identificação `73`.  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.DM qn_subscriptions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
