---
title: conversation_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- conversation_endpoints_TSQL
- conversation_endpoints
- sys.conversation_endpoints
- sys.conversation_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_endpoints catalog view
ms.assetid: 2ed758bc-2a9d-4831-8da2-4b80e218f3ea
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d6c99e2fa7c25011befd0cbdb5aca4bbe45d09f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181902"
---
# <a name="sysconversationendpoints-transact-sql"></a>sys.conversation_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cada lado de uma conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é representado por um ponto de extremidade de conversação. Esta exibição do catálogo contém uma linha para cada ponto de extremidade de conversação no banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|conversation_handle|**uniqueidentifier**|Identificador deste ponto de extremidade de conversação. Não é NULLABLE.|  
|conversation_id|**uniqueidentifier**|Identificador da conversa. Este identificador é compartilhado por ambos os participantes da conversa. Junto com a coluna is_initiator, é exclusivo no banco de dados. Não é NULLABLE.|  
|is_initiator|**tinyint**|Se este ponto de extremidade é o iniciador ou o destino da conversa.  Não é NULLABLE.<br /><br /> 1 = Iniciador<br /><br /> 0 = Destino|  
|service_contract_id|**Int**|Identificador do contrato desta conversa. Não é NULLABLE.|  
|conversation_group_id|**uniqueidentifier**|O identificador do grupo de conversa ao qual esta conversa pertence. Não é NULLABLE.|  
|service_id|**Int**|Identificador do serviço para este lado da conversa. Não é NULLABLE.|  
|lifetime|**datetime**|Data/hora de validade desta conversa. Não é NULLABLE.|  
|state|**char(2)**|O estado atual da conversa. Não é NULLABLE. Um dos seguintes:<br /><br /> PORTANTO saída iniciada. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processou BEGIN CONVERSATION para esta conversa, mas nenhuma mensagem foi enviada ainda.<br /><br /> SI entrada iniciada. Outra instância iniciou uma nova conversa com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda não recebeu completamente a primeira mensagem. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá criar a conversa neste estado se a primeira mensagem estiver fragmentada ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receber mensagens fora de ordem. No entanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode criar a conversa no estado CO (em conversação) se a primeira transmissão recebida para a conversa contiver a primeira mensagem completa.<br /><br /> CO em conversa. A conversa está estabelecida, e ambos os lados da conversa podem enviar mensagens. A maior parte da comunicação para um serviço típico acontece quando a conversa está neste estado.<br /><br /> Disconnected DI entrada. O lado remoto da conversa emitiu uma instrução END CONVERSATION. A conversa permanecerá nesse estado até o lado local emitir uma instrução END CONVERSATION. Um aplicativo ainda pode receber mensagens para a conversa. Como o lado remoto da conversa encerrou a conversa, um aplicativo não pode enviar mensagens nesta conversa. Quando um aplicativo emite uma instrução END CONVERSATION, a conversa passa para o estado CD (Fechado).<br /><br /> DO saída desconectada. O lado local da conversa emitiu uma instrução END CONVERSATION. A conversa permanecerá neste estado até o lado remoto da conversa reconhecer a instrução END CONVERSATION. Um aplicativo não pode enviar ou receber mensagens para a conversa. Quando o lado remoto da conversa reconhece a instrução END CONVERSATION, a conversa passa para o estado CD (Fechada).<br /><br /> ER erro. Ocorreu um erro neste ponto de extremidade. A mensagem de erro é colocada na fila de aplicativos. Se a fila de aplicativos estiver vazia, isso indicará que o aplicativo já consumiu a mensagem de erro.<br /><br /> CD fechado. O ponto de extremidade da conversa não está mais em uso.|  
|state_desc|**nvarchar(60)**|Descrição do estado do ponto de extremidade de conversação. Esta coluna é NULLABLE. Um dos seguintes:<br /><br /> **STARTED_OUTBOUND**<br /><br /> **STARTED_INBOUND**<br /><br /> **CONVERSAR**<br /><br /> **DISCONNECTED_INBOUND**<br /><br /> **DISCONNECTED_OUTBOUND**<br /><br /> **FECHADO**<br /><br /> **ERROR**|  
|far_service|**nvarchar(256)**|Nome do serviço no lado remoto da conversa. Não é NULLABLE.|  
|far_broker_instance|**nvarchar(128)**|A instância do agente do lado remoto da conversa. É NULLABLE.|  
|principal_id|**Int**|Identificador da entidade cujo certificado é usado pelo lado local do diálogo. Não é NULLABLE.|  
|far_principal_id|**Int**|Identificador do usuário cujo certificado é usado pelo lado remoto do diálogo. Não é NULLABLE.|  
|outbound_session_key_identifier|**uniqueidentifier**|Identificador da chave de criptografia de saída para este diálogo. Não é NULLABLE.|  
|inbound_session_key_identifier|**uniqueidentifier**|Identificador da chave de criptografia de entrada para este diálogo. Não é NULLABLE.|  
|security_timestamp|**datetime**|Hora em que a chave de sessão local foi criada. Não é NULLABLE.|  
|dialog_timer|**datetime**|A hora em que o temporizador de conversa deste diálogo envia uma mensagem DialogTimer. Não é NULLABLE.|  
|send_sequence|**bigint**|Número da próxima mensagem na sequência de envio. Não é NULLABLE.|  
|last_send_tran_id|**binary(6)**|ID da transação interna da última transação para enviar uma mensagem. Não é NULLABLE.|  
|end_dialog_sequence|**bigint**|O número de sequência da mensagem Terminar Diálogo. Não é NULLABLE.|  
|receive_sequence|**bigint**|Próximo número de mensagem esperado na sequência de recebimento de mensagem. Não é NULLABLE.|  
|receive_sequence_frag|**Int**|Próximo número de fragmento de mensagem esperado na sequência de recebimento de mensagem. Não é NULLABLE.|  
|system_sequence|**bigint**|O número de sequência da última mensagem do sistema para este diálogo. Não é NULLABLE.|  
|first_out_of_order_sequence|**bigint**|O número de sequência da primeira das mensagens fora de ordem para este diálogo. Não é NULLABLE.|  
|last_out_of_order_sequence|**bigint**|O número de sequência da última mensagem nas mensagens fora de ordem deste diálogo. Não é NULLABLE.|  
|last_out_of_order_frag|**Int**|O número de sequência da última mensagem nos fragmentos fora de ordem deste diálogo. Não é NULLABLE.|  
|is_system|**bit**|1 se este for um diálogo do sistema. Não é NULLABLE.|  
|priority|**tinyint**|A prioridade de conversa que é atribuída a este ponto de extremidade de conversação. Não é NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
