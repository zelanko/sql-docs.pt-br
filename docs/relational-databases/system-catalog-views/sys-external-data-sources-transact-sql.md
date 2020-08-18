---
description: sys.external_data_sources (Transact-SQL)
title: sys. external_data_sources (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74546998aeba42167659eabcbed4571c2f15c492
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88401712"
---
# <a name="sysexternal_data_sources-transact-sql"></a>sys.external_data_sources (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada fonte de dados externa no banco de dado atual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
 Contém uma linha para cada fonte de dados externa no servidor para o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|ID de objeto para a fonte de dados externa.||  
|name|**sysname**|Nome da fonte de dados externa.||  
|local|**nvarchar(4000)**|A cadeia de conexão, que inclui o protocolo, o endereço IP e a porta para a fonte de dados externa.||  
|type_desc|**nvarchar(255)**|Tipo de fonte de dados exibido como uma cadeia de caracteres.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|type|**tinyint**|Tipo de fonte de dados exibido como um número.|0-HADOOP<br /><br /> 1-RDBMS<br /><br /> 2-SHARD_MAP_MANAGER<br /><br /> 3-RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|Para o tipo HADOOP, a localização do IP e da porta do Gerenciador de recursos do Hadoop. Isso é usado para enviar um trabalho em uma fonte de dados do Hadoop.<br /><br /> NULO para outros tipos de fontes de dados externas.||  
|credential_id|**int**|A ID de objeto da credencial no escopo do banco de dados usada para se conectar à fonte externa.||  
|database_name|**sysname**|Para o tipo RDBMS, o nome do banco de dados remoto. Para tipo, SHARD_MAP_MANAGER, o nome do banco de dados do Gerenciador de mapa de fragmentos. NULO para outros tipos de fontes de dados externas.||  
|shard_map_name|**sysname**|Para o tipo SHARD_MAP_MANAGER, o nome do mapa de fragmentos. NULO para outros tipos de fontes de dados externas.||  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys. external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
