---
description: sys.dm_xe_database_session_object_columns (Banco de Dados SQL do Azure)
title: sys.dm_xe_database_session_object_columns
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0e6adc54-4d97-4ef0-bf4f-b4538d69f136
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 78543caf023e0cdb9d677dcd43e7b62143b461a1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546403"
---
# <a name="sysdm_xe_database_session_object_columns-azure-sql-database"></a>sys.dm_xe_database_session_object_columns (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Mostra os valores de configuração de objetos associados a uma sessão.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a todas as versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|O endereço da memória da sessão de evento. Tem uma relação muitos para um com sys. dm_xe_database_sessions. Address. Não permite valor nulo.|  
|column_name|**nvarchar(60)**|O nome do valor de configuração. Não permite valor nulo.|  
|column_id|**int**|A ID da coluna. É exclusiva no objeto. Não permite valor nulo.|  
|column_value|**nvarchar(2048)**|O valor configurado da coluna. Permite valor nulo.|  
|object_type|**nvarchar(60)**|O tipo do objeto.  Não permite valor nulo. object_type é um de:<br /><br /> event<br /><br /> destino|  
|object_name|**nvarchar(60)**|O nome do objeto ao qual a coluna pertence. Não permite valor nulo.|  
|object_package_guid|**uniqueidentifier**|O GUID do pacote que contém o objeto. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_xe_database_session_object_columns. object_name<br /><br /> dm_xe_database_session_object_columns. object_package_guid|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|Muitos para um|  
|dm_xe_database_session_object_columns. column_name<br /><br /> dm_xe_database_session_object_columns. column_id|sys.dm_xe_object_columns.name<br /><br /> sys.dm_xe_object_columns.column_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
