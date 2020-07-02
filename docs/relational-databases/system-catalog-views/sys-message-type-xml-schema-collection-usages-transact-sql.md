---
title: sys. message_type_xml_schema_collection_usages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- message_type_xml_schema_collection_usages_TSQL
- sys.message_type_xml_schema_collection_usages_TSQL
- sys.message_type_xml_schema_collection_usages
- message_type_xml_schema_collection_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.message_type_xml_schema_collection_usages catalog view
ms.assetid: 544f61a1-c7b7-44b4-bf8d-980ba87d0665
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 253b26786ff05028471fe1ad514905d2225ccc90
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760339"
---
# <a name="sysmessage_type_xml_schema_collection_usages-transact-sql"></a>sys.message_type_xml_schema_collection_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Esta exibição do catálogo retorna uma linha para cada tipo de mensagem de serviço que é validado por uma coleção de esquemas XML.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**message_type_id**|**int**|A ID do tipo de mensagem de serviço. Não é NULLABLE.|  
|**xml_collection_id**|**int**|A ID da coleção que contém o namespace do esquema XML de validação. Não é NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
