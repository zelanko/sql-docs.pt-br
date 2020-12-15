---
description: sys.dm_xe_database_session_events (Banco de Dados SQL do Azure)
title: sys.dm_xe_database_session_events
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 9e985a19-f93f-4c56-b644-12c529298011
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 7810edf96b148e6539f7c713c886a91fb6f28af0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474727"
---
# <a name="sysdm_xe_database_session_events-azure-sql-database"></a>sys.dm_xe_database_session_events (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Retorna informações sobre os eventos da sessão. Eventos são pontos de execução discretos. Predicados poderão ser se aplicados a eventos para fazer com que parem de acionar caso o evento não contiver a informação exigida.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a todas as versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|O endereço da memória da sessão de evento. Não permite valor nulo.|  
|event_name|**nvarchar(60)**|O nome do evento ao qual uma ação está associada. Não permite valor nulo.|  
|event_package_guid|**uniqueidentifier**|A GUID para o pacote que contém o evento. Não permite valor nulo.|  
|event_predicate|**nvarchar(2048)**|Uma representação XML da árvore de predicado que é aplicada ao evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_events sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions. Address|Muitos para um|  
|sys. dm _xe_database_session_events. event_package_guid, sys. dm _xe_database_session_events. event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Muitos para um|  
  
  
