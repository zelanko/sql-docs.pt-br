---
title: sys.server_triggers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_triggers
- sys.server_triggers_TSQL
- server_triggers_TSQL
- sys.server_triggers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_triggers catalog view
ms.assetid: 25926ff4-9271-45bf-bc32-d5d3344bd47a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b13aeed62a84258fcfbf5820c17dca59f4b5852
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62660747"
---
# <a name="sysservertriggers-transact-sql"></a>sys.server_triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém o conjunto de todos os gatilhos DDL no nível de servidor com object_type de TR ou TA. No caso de gatilhos CLR, o assembly deve ser carregado na **mestre** banco de dados. Todos os nomes de gatilho DDL no nível de servidor existem em um único escopo global.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do gatilho.|  
|**object_id**|**int**|A ID do objeto.|  
|**parent_class**|**tinyint**|Classe do pai. É sempre:<br /><br /> 100 = Servidor|  
|**parent_class_desc**|**nvarchar(60)**|Descrição de classe do pai. É sempre:<br /><br /> SERVER.|  
|**parent_id**|**int**|Sempre 0 para gatilhos no SERVER.|  
|**type**|**char(2)**|Tipo de objeto:<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL|  
|**type_desc**|**nvarchar(60)**|Descrição da classe do tipo de objeto.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|A data em que o gatilho foi criado.|  
|**modify_date**|**datetime**|A data em que o gatilho foi modificado pela última vez com o uso de uma instrução ALTER.|  
|**is_ms_shipped**|**bit**|O gatilho criado em nome do usuário por um componente interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_disabled**|**bit**|1 = O gatilho está desabilitado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
