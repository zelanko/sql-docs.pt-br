---
title: sys. dm_qn_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c748dd4980fb7b3b142893f5a04dd36f1676f8a6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85635011"
---
# <a name="query-notifications---sysdm_qn_subscriptions"></a>Notificações de consulta-sys. dm_qn_subscriptions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre as assinaturas de notificações de consulta ativa no servidor. Você pode usar essa exibição para verificar assinaturas ativas no servidor ou em um banco de dados especificado, ou verificar um principal de servidor especificado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID de uma assinatura.|  
|**database_id**|**int**|ID do banco de dados no qual a consulta de notificação foi executada. Esse banco de dados armazena informações relativas a essa assinatura.|  
|**sid**|**varbinary (85)**|ID de segurança do principal do servidor que criou e detém essa assinatura.|  
|**object_id**|**int**|ID da tabela interna que armazena informações sobre parâmetros de assinatura.|  
|**created**|**datetime**|Data e hora em que a assinatura foi criada.|  
|**timeout**|**int**|Tempo limite para a assinatura em segundos. A notificação será sinalizada para disparar após o decorrer desse período.<br /><br /> Observação: a hora de acionamento real pode ser maior que o tempo limite especificado. No entanto, se uma alteração que invalida a assinatura ocorrer após o tempo limite especificado, mas antes de a assinatura ser acionada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acionamento ocorrerá no momento em que a alteração foi feita.|  
|**status**|**int**|Indica o status da assinatura. Veja a tabela abaixo dos comentários para obter a lista de códigos.|  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Ativado|Tipo|  
|----------|--------|--------|----------|  
|**sys.dm_qn_subscriptions**|**sys.databases**|**database_id**|Muitos para um|  
|**sys.dm_qn_subscriptions**|**sys.internal_tables**|**object_id**|Muitos para um|  
  
## <a name="remarks"></a>Comentários  
 O código de status 0 indica um status indefinido.  
  
 Os códigos de status a seguir indicam que uma assinatura foi acionada devido a uma alteração:  
  
|Código|Status secundário|Informações|  
|----------|------------------|----------|  
|65798|Assinatura acionada porque os dados foram alterados|Assinatura disparada por inserção|  
|65799|Assinatura acionada porque os dados foram alterados|Excluir|  
|65800|Assinatura acionada porque os dados foram alterados|Atualização|  
|65801|Assinatura acionada porque os dados foram alterados|Mesclar|  
|65802|Assinatura acionada porque os dados foram alterados|Truncar tabela|  
|66048|Assinatura acionada porque o tempo limite expirou|Modo de informações indefinido|  
|66315|Assinatura acionada porque os objetos foram alterados|objeto ou usuário removido|  
|66316|Assinatura acionada porque os objetos foram alterados|objeto alterado|  
|66565|Assinatura acionada porque o banco de dados foi desanexado ou removido|servidor ou db reiniciado|  
|66571|Assinatura acionada porque o banco de dados foi desanexado ou removido|objeto ou usuário removido|  
|66572|Assinatura acionada porque o banco de dados foi desanexado ou removido|objeto alterado|  
|67341|assinatura disparada devido à falta de recursos no servidor|assinatura disparada devido à falta de recursos no servidor|  
  
 Os códigos de status a seguir indicam que uma assinatura não pôde ser criada:  
  
|Código|Status secundário|Informações|  
|----------|------------------|----------|  
|132609|A criação de assinatura falhou porque não há suporte à instrução|Consulta muito complexa|  
|132610|A criação de assinatura falhou porque não há suporte à instrução|Instrução inválida para assinatura|  
|132611|A criação de assinatura falhou porque não há suporte à instrução|Opções definidas inválidas para assinatura|  
|132612|A criação de assinatura falhou porque não há suporte à instrução|Nível de isolamento inválido|  
|132622|A criação de assinatura falhou porque não há suporte à instrução|usado internamente|  
|132623|A criação de assinatura falhou porque não há suporte à instrução|acima do limite do modelo por tabela|  
  
 Os códigos de status a seguir são usados internamente e são classificados como modos de check kill e init:  
  
|Código|Status secundário|Informações|  
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
  
### <a name="a-return-active-query-notification-subscriptions-for-the-current-user"></a>a. Retornar assinaturas ativas de notificação de consulta para o usuário atual  
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
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas a notificações de consulta &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/92eb22d8-33f3-4c17-b32e-e23acdfbd8f4)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)  
  
  
