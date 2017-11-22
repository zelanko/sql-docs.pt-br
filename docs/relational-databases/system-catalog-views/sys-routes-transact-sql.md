---
title: Routes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e27f943e14ad6ef9340764bbd376d754f43dc26b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha por rota. O Service Broker usa rotas para localizar o endereço de rede para um serviço.   
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da rota, exclusivo no banco de dados. Não é NULLABLE.|  
|**route_id**|**int**|Identificador para a rota. Não é NULLABLE.|  
|**principal_id**|**int**|Identificador para o principal de banco de dados que é proprietário da rota. É NULLABLE.|  
|**remote_service_name**|**nvarchar(256)**|Nome do serviço remoto. É NULLABLE.|  
|**BROKER_INSTANCE**|**nvarchar (128)**|Identificador do agente que hospeda o serviço remoto. É NULLABLE.|  
|**tempo de vida**|**datetime**|A data e hora em que a rota expira. Observe que esse valor não usa o fuso horário local. Em vez disso, o valor mostra a hora de expiração para UTC. É NULLABLE.|  
|**endereço**|**nvarchar(256)**|Endereço de rede para o qual o Service Broker envia mensagens ao serviço remoto. É NULLABLE.|  
|**MIRROR_ADDRESS**|**nvarchar(256)**|Endereço de rede do parceiro de espelhamento para o servidor especificado no endereço. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
