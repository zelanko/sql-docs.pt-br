---
title: DM xe_database_session_targets (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8978a41b22beb36ccc31d1cfdc0a73eaf2da34ec
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041014"
---
# <a name="sysdmxedatabasesessiontargets-azure-sql-database"></a>DM xe_database_session_targets (banco de dados SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre os destinos de sessão.  
  
||  
|-|  
|**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|O endereço da memória da sessão de evento. Tem uma relação muitos-para-um com sys.dm_xe_database_sessions.address. Não permite valor nulo.|  
|target_name|**nvarchar(60)**|O nome do destino em uma sessão. Não permite valor nulo.|  
|target_package_guid|**uniqueidentifier**|O GUID do pacote que contém o destino. Não permite valor nulo.|  
|execution_count|**bigint**|O número de horas que o destino foi executado para a sessão. Não permite valor nulo.|  
|execution_duration_ms|**bigint**|O total de tempo, em milissegundos, em que o destino esteve em execução. Não permite valor nulo.|  
|target_data|**nvarchar(max)**|Os dados que o destino mantém, como informações de agregação de evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_targets.event_session_address|sys.dm_xe_database_sessions.address|Muitos para um|  
  
  
