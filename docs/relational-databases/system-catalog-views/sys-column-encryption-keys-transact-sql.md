---
title: sys. column_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_encryption_keys
- column_encryption_keys_TSQL
- sys.column_encryption_keys_TSQL
- column_encryption_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_keys catalog view
ms.assetid: 43980dd8-b9b1-4869-a304-2c183ae8977d
author: jaszymas
ms.author: jaszymas
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4cd6b4a4cb8eeed0dd0a2a78adc2d39c6a2e895d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73593724"
---
# <a name="syscolumn_encryption_keys--transact-sql"></a>sys. column_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]

  Retorna informações sobre CEKs (chaves de criptografia de coluna) criadas com a instrução [Create Column Encryption Key](../../t-sql/statements/create-column-encryption-key-transact-sql.md) . Cada linha representa um CEK.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do CMK.|  
|**column_encryption_key_id**|**int**|ID do CEK.|  
|**create_date**|**datetime**|Data em que o CEK foi criado.|  
|**modify_date**|**datetime**|Data em que a CEK foi modificada pela última vez.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **exibir qualquer chave de criptografia de coluna** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Para obter mais informações, consulte [configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR chave de criptografia de coluna &#40;&#41;Transact-SQL](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTERAR a chave de criptografia de coluna &#40;&#41;Transact-SQL](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [Descartar chave de criptografia de coluna &#40;&#41;Transact-SQL](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CRIAR chave mestra de coluna &#40;&#41;Transact-SQL](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted com enclaves seguro](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Visão geral do gerenciamento de chaves para Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)    

  
  
