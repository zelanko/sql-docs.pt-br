---
description: sys.endpoints (Transact-SQL)
title: pontos de extremidade (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73555ee11e3f03c8478ca170039b7b367036fc4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548745"
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha por ponto de extremidade que é criado no sistema. Sempre há exatamente um ponto de extremidade SYSTEM.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do ponto de extremidade. É exclusivo no servidor. Não permite valor nulo.|  
|**endpoint_id**|**int**|ID do ponto de extremidade. É exclusivo no servidor. Um ponto de extremidade com uma ID inferior a 65536 é um ponto de extremidade de sistema. Não permite valor nulo.|  
|**principal_id**|**int**|ID do principal do servidor que criou e detém esse ponto de extremidade. Permite valor nulo.|  
|**protocol**|**tinyint**|Protocolo de ponto de extremidade.<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = Pipes de nome<br /><br /> 4 = Memória compartilhada<br /><br /> 5 = Adaptador de interface virtual (VIA)<br /><br /> Não permite valor nulo.|  
|**protocol_desc**|**nvarchar(60)**|Descrição do protocolo de ponto de extremidade. É NULLABLE. Um dos seguintes valores:<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **Via** Observação: o protocolo VIA foi preterido. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**tipo**|**tinyint**|Tipo de carga de ponto de extremidade.<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> Não permite valor nulo.|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de carga de ponto de extremidade. Permite valor nulo. Um dos seguintes valores:<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**state**|**tinyint**|Estado de ponto de extremidade.<br /><br /> 0 = STARTED, escutando e processando solicitações.<br /><br /> 1 = STOPPED, escutando, mas não processando solicitações.<br /><br /> 2 = DISABLED, não escutando.<br /><br /> O estado padrão é 1. Permite valor nulo.|  
|**state_desc**|**nvarchar(60)**|Descrição do estado do ponto de extremidade.<br /><br /> STARTED = Escutando e processando solicitações.<br /><br /> STOPPED = Escutando, mas não processando solicitações.<br /><br /> DISABLED = Não escutando.<br /><br /> O estado padrão é STOPPED.<br /><br /> Permite valor nulo.|  
|**is_admin_endpoint**|**bit**|Indica se o ponto de extremidade é para uso administrativo.<br /><br /> 0 = Ponto de extremidade não administrativo.<br /><br /> 1 = Ponto de extremidade administrativo.<br /><br /> Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
