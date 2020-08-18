---
description: sys.transmission_queue (Transact-SQL)
title: sys. transmission_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e3fbd63f399b54af919fd791f33e5d6f7b75a93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400292"
---
# <a name="systransmission_queue-transact-sql"></a>sys.transmission_queue (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta exibição do catálogo contém uma linha para cada mensagem na fila de transmissão, como mostra a tabela a seguir:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|Identificador da conversa à qual pertence essa mensagem. Não é NULLABLE.|  
|**to_service_name**|**nvarchar(256)**|Nome do serviço a que se destina essa mensagem. É NULLABLE.|  
|**to_broker_instance**|**nvarchar(128)**|Identificador do agente que hospeda o serviço a que se destina essa mensagem. É NULLABLE.|  
|**from_service_name**|**nvarchar(256)**|Nome do serviço de onde se origina essa mensagem. É NULLABLE.|  
|**service_contract_name**|**nvarchar(256)**|Nome do contrato seguido pela conversa para essa mensagem. É NULLABLE.|  
|**enqueue_time**|**datetime**|Hora em que a mensagem foi inserida na fila. Este valor usa o UTC, independentemente do fuso horário local para a instância. Não é NULLABLE.|  
|**message_sequence_number**|**bigint**|Número de sequência da mensagem. Não é NULLABLE.|  
|**message_type_name**|**nvarchar(256)**|Nome do tipo da mensagem. É NULLABLE.|  
|**is_conversation_error**|**bit**|Indica se esta mensagem é uma mensagem de erro.<br /><br /> 0 = Não é uma mensagem de erro.<br /><br /> 1 = Mensagem de erro.<br /><br /> Não é NULLABLE.|  
|**is_end_of_dialog**|**bit**|Indica se esta mensagem é uma mensagem de término de conversa. Não é NULLABLE.<br /><br /> 0 = Não é uma mensagem de término de conversa.<br /><br /> 1 = Mensagem de término de conversa.<br /><br /> Não é NULLABLE.|  
|**message_body**|**varbinary(max)**|O corpo desta mensagem. É NULLABLE.|  
|**transmission_status**|**nvarchar(4000)**|Motivo que explica por que esta mensagem está na fila. Normalmente, é uma mensagem de erro que explica por que o envio da mensagem falhou. Se estiver em branco, a mensagem ainda não foi enviada. É NULLABLE.|  
|**priority**|**tinyint**|O nível de prioridade atribuído a essa mensagem. Não é NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
