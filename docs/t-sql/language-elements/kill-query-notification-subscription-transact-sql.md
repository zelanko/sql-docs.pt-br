---
title: KILL QUERY NOTIFICATION SUBSCRIPTION
description: Remova as assinaturas de notificação de consulta de uma instância. Essa instrução pode remover uma assinatura específica ou todas as assinaturas.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0434642595fb334c138e1c3d1764384760a38407
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193366"
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove as assinaturas de notificação de consulta da instância. Essa instrução pode remover uma assinatura específica ou todas as assinaturas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 ALL  
 Remove todas as assinaturas na instância.  
  
 *subscription_id*  
 Remove a assinatura com a ID da assinatura *subscription_id*.  
  
## <a name="remarks"></a>Comentários  
 A instrução KILL QUERY NOTIFICATION SUBSCRIPTION remove assinaturas de notificação de consulta sem produzir uma mensagem de notificação.  
  
 *subscription_id* é a ID da assinatura, conforme mostrado na exibição de gerenciamento dinâmico [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 Se a identificação de assinatura especificada não existir, a instrução produzirá um erro.  
  
## <a name="permissions"></a>Permissões  
 A permissão para executar essa instrução está restrita a membros da função de servidor fixa **sysadmin**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>a. Removendo todas as assinaturas de notificação de consulta na instância.  
 O exemplo a seguir remove todas as assinaturas de notificação de consulta na instância.  
  
```sql  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. Removendo uma única assinatura de notificação de consulta  
 O exemplo a seguir remove a assinatura de notificação da consulta com a identificação `73`.  
  
```sql  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
