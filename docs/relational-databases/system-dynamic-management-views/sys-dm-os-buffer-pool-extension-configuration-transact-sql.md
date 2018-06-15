---
title: sys.DM os_buffer_pool_extension_configuration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ecc569a1f112bba0ec49c46da77c1dbc29fcddab
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464222"
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Retorna informações de configuração sobre a extensão do pool de buffers no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Retorna uma linha para cada arquivo de extensão do pool de buffers.  
  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|path|**nvarchar**(256)|O caminho e o nome de arquivo do cache de extensão do pool de buffers. Anulável.|  
|file_id|**Int**|ID do arquivo de extensão do pool de buffers. Não permite valor nulo.|  
|state|**Int**|O estado do recurso de extensão do pool de buffers. Não permite valor nulo.<br /><br /> 0 - Extensão do pool de buffers desabilitada<br /><br /> 1 - Extensão do pool de buffers desabilitando<br /><br /> 2 - reservado para uso futuro<br /><br /> 3 - Extensão do pool de buffers habilitando<br /><br /> 4 - Reservado para uso futuro<br /><br /> 5 - Extensão do pool de buffers habilitada|  
|state_description|**nvarchar**(60)|Descreve o estado do recurso de extensão do pool de buffers. Permite valor nulo.<br /><br /> 0 = EXTENSÃO DO POOL DE BUFFERS DESABILITADA<br /><br /> 1 = EXTENSÃO DO POOL DE BUFFERS HABILITADA|  
|current_size_in_kb|**bigint**|Tamanho atual do arquivo de extensão do pool de buffers. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>A. Retornando informações de configuração da extensão do pool de buffers  
 O exemplo a seguir retorna todas as colunas da DMV sys.dm_os_buffer_pool_extension_configruation.  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>B. Retornando o número de páginas armazenadas em cache do arquivo de extensão do pool de buffers  
 O exemplo a seguir retorna o número de páginas armazenadas em cache de cada arquivo de extensão do pool de buffers.  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensão do Pool de buffers](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.DM os_buffer_descriptors & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
