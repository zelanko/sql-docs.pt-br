---
title: sys.service_message_types (Transact-SQL) | Microsoft Docs
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
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e499fa009f74a6613eb78b8cecd93ee59f43b236
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha por tipo de mensagem registrado no agente de serviços.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de tipo de mensagem, exclusivo no banco de dados. Não é NULLABLE.|  
|**message_type_id**|**Int**|Identificador do tipo de mensagem, exclusivo no banco de dados. Não é NULLABLE.|  
|**principal_id**|**Int**|Identificador para a entidade de banco de dados que possui este tipo de mensagem. É NULLABLE.|  
|**validation**|**char(2)**|Validação feita pelo Broker antes de enviar mensagens desse tipo. Não é NULLABLE. Um dos seguintes:<br /><br /> N = Nenhum<br /><br /> X = XML<br /><br /> E = vazio|  
|**validation_desc**|**nvarchar(60)**|Descrição da validação feita pelo Broker antes de enviar mensagens desse tipo. É NULLABLE. Um dos seguintes:<br /><br /> Nenhuma<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**Int**|Para validação que usa um esquema de XML, o identificador para a coleção de esquema usada.<br /><br /> Caso contrário, NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
