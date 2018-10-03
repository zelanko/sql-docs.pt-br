---
title: DM broker_forwarded_messages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ce05635464cc9b02e419c4f0a5b162a14042d51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633294"
---
# <a name="sysdmbrokerforwardedmessages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada mensagem do Service Broker que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em processo de encaminhamento.  
  

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|ID da conversa à qual esta mensagem pertence. É NULLABLE.|  
|**is_initiator**|**bit**|Indica se esta mensagem é do iniciador da conversa.  É NULLABLE.<br /><br /> 0 = Não é do iniciador<br /><br /> 1 = É do iniciador|  
|**to_service_name**|**nvarchar(512)**|Nome do serviço ao qual esta mensagem é enviada. É NULLABLE.|  
|**to_broker_instance**|**nvarchar(512)**|Identificador do agente que hospeda o serviço ao qual esta mensagem é enviada. É NULLABLE.|  
|**from_service_name**|**nvarchar(512)**|Nome do serviço de onde se origina essa mensagem. É NULLABLE.|  
|**from_broker_instance**|**nvarchar(512)**|Identificador do agente que hospeda o serviço do qual esta mensagem se origina. É NULLABLE.|  
|**adjacent_broker_address**|**nvarchar(512)**|Endereço de rede ao qual esta mensagem está sendo enviada. É NULLABLE.|  
|**message_sequence_number**|**bigint**|Número de sequência da mensagem na caixa de diálogo. É NULLABLE.|  
|**message_fragment_number**|**int**|Se a mensagem de diálogo estiver fragmentada, este será o número do fragmento que esta mensagem de transporte contém. É NULLABLE.|  
|**hops_remaining**|**tinyint**|Número de vezes que a mensagem pode ser retransmitida antes de chegar ao destino final. Cada vez a mensagem é encaminhada, esse número diminui em 1. É NULLABLE.|  
|**time_to_live**|**int**|Tempo máximo para a mensagem permanecer ativa. Quando chegar a 0, a mensagem será descartada. É NULLABLE.|  
|**time_consumed**|**int**|Tempo que a mensagem esteve ativa. Cada vez a mensagem é encaminhada, é diminuído desse número o tempo que levou para a mensagem ser encaminhada. Não é NULLABLE.|  
|**message_id**|**uniqueidentifier**|A identificação da mensagem. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

