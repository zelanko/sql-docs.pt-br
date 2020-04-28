---
title: sys.dm_xe_database_session_targets
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 860faaa6c9e574feda8d5c28be17a265707fd72e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73844430"
---
# <a name="sysdm_xe_database_session_targets-azure-sql-database"></a>sys.dm_xe_database_session_targets (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre os destinos da sessão.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a qualquer versão futura.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|O endereço da memória da sessão de evento. Tem uma relação muitos para um com sys. dm_xe_database_sessions. Address. Não permite valor nulo.|  
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
|sys. dm_xe_database_session_targets. event_session_address|sys. dm_xe_database_sessions. Address|Muitos para um|  
  
  
