---
title: sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d9a7d363dbab2a552c54bffedfc92fe6cf49a708
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contém uma linha por configuração. 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**Int**|ID da opção de configuração.|  
|**name**|**nvarchar(60)**|O nome da opção de configuração. Para obter informações sobre as configurações possíveis, consulte [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**value**|**sqlvariant**|O valor definido para essa opção de configuração para a réplica primária.|  
|**value_for_secondary**|**sqlvariant**|O valor definido para essa opção de configuração para as réplicas secundárias.|  
  
##  <a name="Permissions"></a> Permissões  
 Requer associação à função **pública** .  
  
## <a name="remarks"></a>Remarks  
 Quando NULL é retornado como o valor para **value_for_secondary**, isso significa que o secundário é definido como primário.  
 
 As definições de configurações no escopo do banco de dados serão transferidas para o banco de dados. Isso significa que quando um determinado banco de dados é restaurado ou anexado, as definições de configuração existentes permanecem.
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
