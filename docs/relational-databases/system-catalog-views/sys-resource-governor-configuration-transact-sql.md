---
title: resource_governor_configuration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_configuration_TSQL
- sys.resource_governor_configuration
- resource_governor_configuration_TSQL
- resource_governor_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_configuration catalog view
ms.assetid: 89099668-1dc6-4b07-9d8b-49bc95c7bfc0
author: stevestein
ms.author: sstein
ms.openlocfilehash: c85332cb1c26f81cdbbaa7bffa5410cf29e711e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904555"
---
# <a name="sysresourcegovernorconfiguration-transact-sql"></a>sys.resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o estado armazenado do Administrador de Recursos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|A ID da função de classificador como está armazenada nos metadados. Não permite valor nulo.<br /><br /> **Observação** essa função é usada para classificar novas sessões e usa regras para encaminhar a carga de trabalho ao grupo de carga de trabalho adequado. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).|  
|is_enabled|**bit**|Indica o estado atual do Administrador de Recursos:<br /><br /> 0 = administrador de recursos não está habilitado.<br /><br /> 1 = administrador de recursos está habilitado.<br /><br /> Não permite valor nulo.|  
|max_outstanding_io_per_volume|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O número máximo de E/S pendente por volume.|  
  
## <a name="remarks"></a>Comentários  
 A exibição de catálogo mostra a configuração do Administrador de Recursos na forma como está armazenada nos metadados. Para verificar a configuração da memória, use a exibição de gerenciamento dinâmica correspondente.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION para exibir conteúdo e a permissão CONTROL SERVER para alterar conteúdo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como obter e comparar os valores de metadados armazenados e os valores na memória da configuração do Administrador de recursos.  
  
```  
USE master;  
GO  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
GO  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo do administrador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
