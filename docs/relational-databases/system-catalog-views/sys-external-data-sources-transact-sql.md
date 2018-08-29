---
title: sys.external_data_sources (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6dec76073fbd0a6e0ed7da85dd247f3435dec85b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43064924"
---
# <a name="sysexternaldatasources-transact-sql"></a>sys.external_data_sources (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Contém uma linha para cada fonte de dados externa no banco de dados atual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Contém uma linha para cada fonte de dados externa no servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|Identificação do objeto de fonte de dados externa.||  
|nome|**sysname**|Nome da fonte de dados externa.||  
|local|**nvarchar(4000)**|A cadeia de conexão, que inclui o protocolo, endereço IP e porta para a fonte de dados externa.||  
|type_desc|**nvarchar(255)**|Tipo de fonte de dados exibido como uma cadeia de caracteres.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|Tipo|**tinyint**|Tipo de fonte de dados exibido como um número.|0 - HADOOP<br /><br /> 1 - RDBMS<br /><br /> 2 - SHARD_MAP_MANAGER<br /><br /> 3 - RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|Para o tipo de HADOOP, o IP e a porta local do Gerenciador de recursos do Hadoop. Isso é usado para enviar um trabalho em uma fonte de dados do Hadoop.<br /><br /> NULL para outros tipos de fontes de dados externas.||  
|credential_id|**int**|A ID de objeto do banco de dados com escopo de credencial usado para se conectar à fonte de dados externa.||  
|database_name|**sysname**|Tipo RDBMS, o nome do banco de dados remoto. Tipo, SHARD_MAP_MANAGER, o nome do que o banco de dados do Gerenciador de mapa do fragmento. NULL para outros tipos de fontes de dados externas.||  
|shard_map_name|**sysname**|Tipo SHARD_MAP_MANAGER, o nome do mapa de fragmentos. NULL para outros tipos de fontes de dados externas.||  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
