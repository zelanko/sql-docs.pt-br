---
title: sys.DM qn_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_qn_subscriptions
- dm_qn_subscriptions_TSQL
- sys.dm_qn_subscriptions
- sys.dm_qn_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_qn_subscriptions dynamic management view
ms.assetid: a3040ce6-f5af-48fc-8835-c418912f830c
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df9fefcb59549dc330a214a916244deae09d0227
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="query-notifications---sysdmqnsubscriptions"></a>Consultar notificações - sys.DM qn_subscriptions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre as assinaturas de notificações de consulta ativa no servidor. Você pode usar essa exibição para verificar assinaturas ativas no servidor ou em um banco de dados especificado, ou verificar um principal de servidor especificado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**Int**|ID de uma assinatura.|  
|**database_id**|**Int**|ID do banco de dados no qual a consulta de notificação foi executada. Esse banco de dados armazena informações relativas a essa assinatura.|  
|**sid**|**varbinary(85)**|ID de segurança do principal do servidor que criou e detém essa assinatura.|  
|**object_id**|**Int**|ID da tabela interna que armazena informações sobre parâmetros de assinatura.|  
|**created**|**datetime**|Data e hora em que a assinatura foi criada.|  
|**timeout**|**Int**|Tempo limite para a assinatura em segundos. A notificação será sinalizada para disparar após o decorrer desse período.<br /><br /> Observação: O tempo real do disparo pode ser maior que o tempo limite especificado. No entanto, se uma alteração que invalida a assinatura ocorrer após o tempo limite especificado, mas antes de a assinatura ser disparada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegurará que o disparo ocorra no momento em que a alteração for realizada.|  
|**status**|**Int**|Indica o status da assinatura. Veja a tabela abaixo dos comentários para obter a lista de códigos.|  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Em|Tipo|  
|----------|--------|--------|----------|  
|**sys.dm_qn_subscriptions**|**sys.databases**|**database_id**|Muitos para um|  
|**sys.dm_qn_subscriptions**|**sys.internal_tables**|**object_id**|Muitos para um|  
  
## <a name="remarks"></a>Remarks  
 O código de status 0 indica um status indefinido.  
  
 Os códigos de status a seguir indicam que uma assinatura foi acionada devido a uma alteração:  
  
|Código|Status secundário|informações de|  
|----------|------------------|----------|  
|65798|Assinatura acionada porque os dados foram alterados|Assinatura disparada por inserção|  
|65799|Assinatura acionada porque os dados foram alterados|Delete (excluir)|  
|65800|Assinatura acionada porque os dados foram alterados|Update (atualizar)|  
|65801|Assinatura acionada porque os dados foram alterados|Mesclagem|  
|65802|Assinatura acionada porque os dados foram alterados|Truncar tabela|  
|66048|Assinatura acionada porque o tempo limite expirou|Modo de informações indefinido|  
|66315|Assinatura acionada porque os objetos foram alterados|objeto ou usuário removido|  
|66316|Assinatura acionada porque os objetos foram alterados|objeto alterado|  
|66565|Assinatura acionada porque o banco de dados foi desanexado ou removido|servidor ou db reiniciado|  
|66571|Assinatura acionada porque o banco de dados foi desanexado ou removido|objeto ou usuário removido|  
|66572|Assinatura acionada porque o banco de dados foi desanexado ou removido|objeto alterado|  
|67341|assinatura disparada devido à falta de recursos no servidor|assinatura disparada devido à falta de recursos no servidor|  
  
 Os códigos de status a seguir indicam que uma assinatura não pôde ser criada:  
  
|Código|Status secundário|informações de|  
|----------|------------------|----------|  
|132609|A criação de assinatura falhou porque não há suporte à instrução|Consulta muito complexa|  
|132610|A criação de assinatura falhou porque não há suporte à instrução|Instrução inválida para assinatura|  
|132611|A criação de assinatura falhou porque não há suporte à instrução|Opções definidas inválidas para assinatura|  
|132612|A criação de assinatura falhou porque não há suporte à instrução|Nível de isolamento inválido|  
|132622|A criação de assinatura falhou porque não há suporte à instrução|usado internamente|  
|132623|A criação de assinatura falhou porque não há suporte à instrução|acima do limite do modelo por tabela|  
  
 Os códigos de status a seguir são usados internamente e são classificados como modos de check kill e init:  
  
|Código|Status secundário|informações de|  
|----------|------------------|----------|  
|198656|Usado internamente: modos check kill e init|Modo de informações indefinido|  
|198928|Assinatura destruída|Assinatura acionada porque o banco de dados foi anexado|  
|198929|Assinatura destruída|Assinatura acionada porque o usuário foi removido|  
|198930|Assinatura destruída|Assinatura removida devido a uma nova assinatura|  
|198931|Assinatura destruída|assinatura eliminada|  
|199168|Assinatura ativa|Modo de informações indefinido|  
|199424|Assinatura inicializada, mas não ativa ainda|Modo de informações indefinido|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor.  
  
> [!NOTE]  
>  Se o usuário não tiver a permissão VIEW SERVER STATE, essa exibição retornará informações sobre as assinaturas de propriedade do usuário atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-active-query-notification-subscriptions-for-the-current-user"></a>A. Retornar assinaturas ativas de notificação de consulta para o usuário atual  
 O exemplo a seguir retorna assinaturas ativas de notificação de consulta para o usuário atual. Se o usuário tiver permissões VIEW SERVER STATE, todas as assinaturas ativas no servidor serão retornadas.  
  
```  
SELECT id, database_id, sid, object_id, created, timeout, status  
FROM sys.dm_qn_subscriptions;  
GO  
```  
  
### <a name="b-returning-active-query-notification-subscriptions-for-a-specified-user"></a>B. Retornar assinaturas ativas de notificação de consulta para um usuário especificado  
 O exemplo a seguir retorna assinaturas ativas de notificação de consulta feitas pelo logon `Ruth0`.  
  
```  
SELECT id, database_id, sid, object_id, created, timeout, status  
FROM sys.dm_qn_subscriptions  
WHERE sid = SUSER_SID('Ruth0');  
GO  
```  
  
### <a name="c-returning-internal-table-metadata-for-query-notification-subscriptions"></a>C. Retornando metadados de tabela interna para assinaturas de notificação de consulta  
 O exemplo a seguir retorna os metadados de tabela interna para assinaturas de notificação de consulta.  
  
```  
SELECT qn.id AS query_subscription_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.dm_qn_subscriptions AS qn ON it.object_id = qn.object_id  
WHERE it.internal_type_desc = 'QUERY_NOTIFICATION';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas às notificações de consulta &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/92eb22d8-33f3-4c17-b32e-e23acdfbd8f4)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)  
  
  
