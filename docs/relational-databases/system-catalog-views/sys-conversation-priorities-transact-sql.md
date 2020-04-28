---
title: sys. conversation_priorities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_priorities_TSQL
- conversation_priorities
- sys.conversation_priorities_TSQL
- sys.conversation_priorities
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], priorities
- Service Broker, conversations
- sys.conversation_priorities catalog view
ms.assetid: 7cbb9171-3310-4aae-8458-755c882d6462
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a1278426b6774c8f5c2d9bb13577e1499930c13
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68109476"
---
# <a name="sysconversation_priorities-transact-sql"></a>sys.conversation_priorities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada prioridade de conversa criada no banco de dados atual, conforme mostrado na tabela a seguir: 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|Priority_id|**int**|Um número que identifica exclusivamente a prioridade de conversa. Não é NULLABLE.|  
|name|**sysname**|Nome da prioridade de conversa. Não é NULLABLE.|  
|service_contract_id|**int**|O identificador do contrato especificado para a prioridade de conversa. Ele pode ser unido à coluna de service_contract_id em sys.service_contracts. É NULLABLE.|  
|local_service_id|**int**|O identificador do serviço especificado como o serviço local para a prioridade de conversa. Esta coluna pode ser unida à coluna de service_id em sys.services. É NULLABLE.|  
|remote_service_name|**nvarchar(256)**|O nome do serviço especificado como o serviço remoto para a prioridade de conversa. É NULLABLE.|  
|priority|**tinyint**|O nível de prioridade especificado nesta prioridade de conversa. Não é NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista as prioridades de conversa usando junções para mostrar o contrato e os nomes de serviços locais.  
  
```  
SELECT scp.name AS priority_name,  
       ssc.name AS contract_name,  
       ssvc.name AS local_service_name,  
       scp.remote_service_name,  
       scp.priority AS priority_level  
FROM sys.conversation_priorities AS scp  
    INNER JOIN sys.service_contracts AS ssc  
       ON scp.service_contract_id = ssc.service_contract_id  
    INNER JOIN sys.services AS ssvc  
       ON scp.local_service_id = ssvc.service_id  
ORDER BY priority_name, contract_name,  
         local_service_name, remote_service_name;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CRIAR prioridade do agente &#40;&#41;Transact-SQL](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [Descartar prioridade do agente &#40;&#41;Transact-SQL](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys. Services &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)   
 [sys. service_contracts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-contracts-transact-sql.md)  
  
  
