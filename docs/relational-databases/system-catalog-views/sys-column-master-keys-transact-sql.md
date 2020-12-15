---
description: sys.column_master_keys (Transact-SQL)
title: sys.column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9b62a54ec2ab17d76f5f726dbd26f28a60d79afc
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429570"
---
# <a name="syscolumn_master_keys-transact-sql"></a>sys.column_master_keys (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Retorna uma linha para cada chave mestra de banco de dados adicionada usando a instrução [Create Master Key](../../t-sql/statements/create-column-master-key-transact-sql.md) . Cada linha representa uma única chave mestra de coluna (CMK).  
    
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do CMK.|  
|**column_master_key_id**|**int**|ID da chave mestra de coluna.|  
|**create_date**|**datetime**|Data em que a chave mestra de coluna foi criada.|  
|**modify_date**|**datetime**|Data em que a chave mestra de coluna foi modificada pela última vez.|  
|**key_store_provider_name**|**sysname**|Nome do provedor para o repositório de chave mestra de coluna que contém o CMK. Valores permitidos são:<br /><br /> MSSQL_CERTIFICATE_STORE – se o repositório de chaves mestras de coluna for um repositório de certificados.<br /><br /> Um valor definido pelo usuário, se o repositório de chave mestra de coluna for de um tipo personalizado.|  
|**key_path**|**nvarchar(4000)**|Um caminho específico do repositório da chave mestra de coluna. O formato do caminho depende do tipo de repositório de chave mestra de coluna. Exemplo:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Para um repositório de chaves mestras de coluna personalizado, o desenvolvedor é responsável por definir o que é um caminho de chave para o repositório de chaves mestras de coluna personalizada.|  
|**allow_enclave_computations**|**bit**|Indica se a chave mestra de coluna está habilitada para enclave (se as chaves de criptografia de coluna, criptografadas com essa chave mestra, podem ser usadas para cálculos dentro do enclaves seguro do lado do servidor). Para obter mais informações, consulte [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).|  
|**assinatura**|**varbinary(max)**|Uma assinatura digital de **key_path** e **allow_enclave_computations**, produzida usando a chave mestra de coluna, referenciada por **key_path**.|


  
## <a name="permissions"></a>Permissões  
 Requer a permissão **exibir qualquer chave mestra de coluna** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Visão geral do gerenciamento de chaves do Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
 
  
  
