---
title: sys. service_message_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7fca6309675975b6c03c46f7724eb6acfe91e580
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752878"
---
# <a name="sysservice_message_types-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Esta exibição do catálogo contém uma linha por tipo de mensagem registrado no agente de serviços.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de tipo de mensagem, exclusivo no banco de dados. Não é NULLABLE.|  
|**message_type_id**|**int**|Identificador do tipo de mensagem, exclusivo no banco de dados. Não é NULLABLE.|  
|**principal_id**|**int**|Identificador para a entidade de banco de dados que possui este tipo de mensagem. É NULLABLE.|  
|**validation**|**char(2)**|Validação feita pelo Broker antes de enviar mensagens desse tipo. Não é NULLABLE. Um destes:<br /><br /> N = Nenhum<br /><br /> X = XML<br /><br /> E = vazio|  
|**validation_desc**|**nvarchar(60)**|Descrição da validação feita pelo Broker antes de enviar mensagens desse tipo. É NULLABLE. Um destes:<br /><br /> NONE<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|Para validação que usa um esquema de XML, o identificador para a coleção de esquema usada.<br /><br /> Caso contrário, NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
