---
title: KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 94782ca3b2837889211752fb915c73ea6f713ef5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove as assinaturas de notificação de consulta da instância. Essa instrução pode remover uma assinatura específica ou todas as assinaturas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>Argumentos  
 ALL  
 Remove todas as assinaturas na instância.  
  
 *subscription_id*  
 Remove a assinatura com a ID da assinatura *subscription_id*.  
  
## <a name="remarks"></a>Remarks  
 A instrução KILL QUERY NOTIFICATION SUBSCRIPTION remove assinaturas de notificação de consulta sem produzir uma mensagem de notificação.  
  
 *subscription_id* é a ID da assinatura, conforme mostrado na exibição de gerenciamento dinâmico [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 Se a identificação de assinatura especificada não existir, a instrução produzirá um erro.  
  
## <a name="permissions"></a>Permissões  
 A permissão para executar essa instrução está restrita a membros da função de servidor fixa **sysadmin**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
