---
title: Routes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 89fb63380c95e38f97f02b24eb68c178182b873a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220057"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha por rota. O Service Broker usa rotas para localizar o endereço de rede para um serviço.   

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da rota, exclusivo no banco de dados. Não é NULLABLE.|  
|**route_id**|**Int**|Identificador para a rota. Não é NULLABLE.|  
|**principal_id**|**Int**|Identificador para o principal de banco de dados que é proprietário da rota. É NULLABLE.|  
|**remote_service_name**|**nvarchar(256)**|Nome do serviço remoto. É NULLABLE.|  
|**broker_instance**|**nvarchar(128)**|Identificador do agente que hospeda o serviço remoto. É NULLABLE.|  
|**lifetime**|**datetime**|A data e hora em que a rota expira. Observe que esse valor não usa o fuso horário local. Em vez disso, o valor mostra a hora de expiração para UTC. É NULLABLE.|  
|**address**|**nvarchar(256)**|Endereço de rede para o qual o Service Broker envia mensagens ao serviço remoto. É NULLABLE. Para a instância da gerenciados de banco de dados SQL, o endereço deve ser local.|  
|**mirror_address**|**nvarchar(256)**|Endereço de rede do parceiro de espelhamento para o servidor especificado no endereço. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
