---
title: sys. Endpoints (Transact-SQL) | Microsoft Docs
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
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
caps.latest.revision: "45"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ded68aefc2121f651b9005fe3e75b64ec80dc0c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha por ponto de extremidade que é criado no sistema. Sempre há exatamente um ponto de extremidade SYSTEM.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do ponto de extremidade. É exclusivo dentro do servidor. Não permite valor nulo.|  
|**endpoint_id**|**int**|ID do ponto de extremidade. É exclusivo dentro do servidor. Um ponto de extremidade com uma ID inferior a 65536 é um ponto de extremidade de sistema. Não permite valor nulo.|  
|**principal_id**|**int**|ID do principal do servidor que criou e detém esse ponto de extremidade. Permite valor nulo.|  
|**protocolo**|**tinyint**|Protocolo de ponto de extremidade.<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = Pipes de nome<br /><br /> 4 = Memória compartilhada<br /><br /> 5 = Adaptador de interface virtual (VIA)<br /><br /> Não permite valor nulo.|  
|**protocol_desc**|**nvarchar (60)**|Descrição do protocolo de ponto de extremidade. É NULLABLE. Um dos valores seguintes:<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **Por meio de** Observação: O protocolo VIA foi preterido. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**tipo**|**tinyint**|Tipo de carga de ponto de extremidade.<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> Não permite valor nulo.|  
|**type_desc**|**nvarchar (60)**|Descrição do tipo de carga de ponto de extremidade. Permite valor nulo. Um dos valores seguintes:<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**estado**|**tinyint**|Estado de ponto de extremidade.<br /><br /> 0 = STARTED, escutando e processando solicitações.<br /><br /> 1 = STOPPED, escutando, mas não processando solicitações.<br /><br /> 2 = DISABLED, não escutando.<br /><br /> O estado padrão é 1. Permite valor nulo.|  
|**state_desc**|**nvarchar (60)**|Descrição do estado do ponto de extremidade.<br /><br /> STARTED = Escutando e processando solicitações.<br /><br /> STOPPED = Escutando, mas não processando solicitações.<br /><br /> DISABLED = Não escutando.<br /><br /> O estado padrão é STOPPED.<br /><br /> Permite valor nulo.|  
|**is_admin_endpoint**|**bit**|Indica se o ponto de extremidade é para uso administrativo.<br /><br /> 0 = Ponto de extremidade não administrativo.<br /><br /> 1 = Ponto de extremidade administrativo.<br /><br /> Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo de pontos de extremidade &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
