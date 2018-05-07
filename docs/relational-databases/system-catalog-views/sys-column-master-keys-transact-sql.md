---
title: column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7f961586da2bb4bd9a3169fe955d989557535ba7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada chave mestra de banco de dados adicionada usando o [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) instrução. Cada linha representa uma chave mestra de coluna única (CMK).  
    
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome da CMK.|  
|**column_master_key_id**|**Int**|ID da chave mestra de coluna.|  
|**create_date**|**datetime**|Data em que a chave mestra de coluna foi criada.|  
|**modify_date**|**datetime**|Data em que a chave mestra de coluna foi modificada pela última vez.|  
|**key_store_provider_name**|**sysname**|Nome do provedor de repositório de chave mestra de coluna que contém a CMK. Valores permitidos são:<br /><br /> MSSQL_CERTIFICATE_STORE – se o repositório de chave mestra de coluna é um repositório de certificados.<br /><br /> Um valor definido pelo usuário, se o repositório de chave mestra de coluna for de um tipo personalizado.|  
|**key_path**|**nvarchar(4000)**|Um caminho de específicas do repositório de chave mestra de coluna da chave. O formato do caminho depende o tipo de repositório de chave mestra de coluna. Exemplo:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Para um repositório de chaves mestras de coluna personalizada, o desenvolvedor é responsável por definir que um caminho de chave é para o repositório de chaves mestras de coluna personalizada.|  
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW ANY COLUMN MASTER KEY** permissão.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
