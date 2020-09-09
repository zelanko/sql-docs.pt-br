---
description: sys.conversation_groups (Transact-SQL)
title: sys. conversation_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_groups_TSQL
- conversation_groups
- sys.conversation_groups
- sys.conversation_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_groups catalog view
ms.assetid: 3f35815e-2de4-42a2-a972-8f0141dad0b3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ffea98db7c6d1a2a673b7a8bd8d358578d81d43b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537447"
---
# <a name="sysconversation_groups-transact-sql"></a>sys.conversation_groups (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta exibição do catálogo contém uma linha para cada grupo de conversa.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**conversation_group_id**|**uniqueidentifier**|Identificador do grupo de conversa. Não é NULLABLE.|  
|**service_id**|**int**|Identificador do serviço para conversas neste grupo. Não é NULLABLE.|  
|**is_system**|**bit**|Indica se esta é uma instância de sistema ou não. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
