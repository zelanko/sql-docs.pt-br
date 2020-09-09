---
description: sys.dm_xe_database_session_event_actions (Banco de Dados SQL do Azure)
title: sys.dm_xe_database_session_event_actions
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 48519fd9-c7c2-434b-848d-ccbf41133fdd
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-lt-2019
ms.openlocfilehash: 750bfeae27269acf4b8d3fb1e64b7f8944f8ebbe
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546405"
---
# <a name="sysdm_xe_database_session_event_actions-azure-sql-database"></a>sys.dm_xe_database_session_event_actions (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

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
  
  
