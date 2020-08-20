---
description: sys. column_encryption_key_values (Transact-SQL)
title: sys. column_encryption_key_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aee9c14d1b59055cc968e9b51fa2e07005ae94bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470002"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys. column_encryption_key_values (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre valores criptografados de chaves de criptografia de coluna (CEKs) criados com a instrução [Create Column Encryption Key](../../t-sql/statements/create-column-encryption-key-transact-sql.md) ou [ALTER column Encryption Key &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) Statement. Cada linha representa um valor de um CEK, criptografado com uma CMK (chave mestra de coluna).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|ID do CEK no banco de dados.|  
|**column_master_key_id**|**int**|ID da chave mestra de coluna que foi usada para criptografar o valor de CEK.|  
|**encrypted_value**|**varbinary(8000)**|Valor CEK criptografado com o CMK especificado em column_master_key_id.|  
|**encryption_algorithm_name**|**sysname**|Nome de um algoritmo usado para criptografar o valor de CEK.<br /><br /> Nome do algoritmo de criptografia usado para criptografar o valor. O algoritmo para os provedores de sistema deve ser  **RSA_OAEP**.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **exibir qualquer chave de criptografia de coluna** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR chave de criptografia de coluna &#40;&#41;Transact-SQL ](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTERAR a chave de criptografia de coluna &#40;&#41;Transact-SQL ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [Descartar chave de criptografia de coluna &#40;&#41;Transact-SQL ](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CRIAR chave mestra de coluna &#40;&#41;Transact-SQL ](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys. column_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys. column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted com enclaves seguro](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Visão geral do gerenciamento de chaves para Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
