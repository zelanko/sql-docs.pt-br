---
title: sys.dm_xe_database_session_event_actions
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 48519fd9-c7c2-434b-848d-ccbf41133fdd
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-lt-2019
ms.openlocfilehash: c6e9cacb9f6249f98f1481049c3b55b58a247fdb
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627393"
---
# <a name="sysdm_xe_database_session_event_actions-azure-sql-database"></a>sys.dm_xe_database_session_event_actions (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre ações da sessão de evento. Quando eventos são disparados, são executadas ações. Esta exibição de gerenciamento agrega estatísticas sobre o número de vezes que uma ação foi executada e o tempo total de execução da ação.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a qualquer versão futura.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|O endereço da memória da sessão de evento. Não permite valor nulo.|  
|action_name|**nvarchar(60)**|O nome da ação. Não permite valor nulo.|  
|action_package_guid|**uniqueidentifier**|A GUID para o pacote que contém esta ação. Não permite valor nulo.|  
|event_name|**nvarchar(60)**|O nome do evento ao qual a ação está associada. Não permite valor nulo.|  
|event_package_guid|**uniqueidentifier**|O GUID do pacote que contém o evento. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys. dm_xe_database_session_event_actions. event_session_address|sys. dm_xe_database_sessions. Address|Muitos para um|  
|sys. dm_xe_database_session_event_actions. action_name<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name<br /><br /> sys. dm_xe_database_session_events. event_package_guid|Muitos para um|  
|sys. dm_xe_database_session_event_actions. event_name<br /><br /> sys. dm_xe_database_session_event_actions. event_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
