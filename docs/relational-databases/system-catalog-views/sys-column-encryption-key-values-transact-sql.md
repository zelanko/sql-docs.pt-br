---
title: sys. column_encryption_key_values (Transact-SQL) | Microsoft Docs
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
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e546c08ad979dbb06dec5557d0f19be2e15c26f6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43107617"
---
# <a name="syscolumnencryptionkeyvalues-transact-sql"></a>sys. column_encryption_key_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre valores criptografados da coluna de chaves de criptografia (CEKs) criadas com o a [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) ou o [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)instrução. Cada linha representa um valor de uma CEK criptografado com uma chave mestra de coluna (CMK).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|ID da CEK no banco de dados.|  
|**column_master_key_id**|**int**|ID da chave mestra de coluna que foi usada para criptografar o valor CEK.|  
|**encrypted_value**|**varbinary(8000)**|Valor CEK criptografado com a CMK especificada em column_master_key_id.|  
|**encryption_algorithm_name**|**sysname**|Nome de um algoritmo usado para criptografar o valor CEK.<br /><br /> Nome do algoritmo de criptografia usado para criptografar o valor. O algoritmo para os provedores de sistema deve ser **RSA_OAEP**.|  
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW ANY COLUMN ENCRYPTION KEY** permissão.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
