---
title: sys.dm_database_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea8e6825a2019667734a9d68f5798da00084c71b
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583039"
---
# <a name="sysdmdatabaseencryptionkeys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre o estado de criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas. Para obter mais informações sobre a criptografia do banco de dados, confira [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados.|  
|encryption_state|**int**|Indica se o banco de dados está criptografado ou não.<br /><br /> 0 = Nenhuma chave de criptografia de banco de dados presente, nenhuma criptografia<br /><br /> 1 = Sem-criptografia<br /><br /> 2 = Criptografia em andamento<br /><br /> 3 = Criptografado<br /><br /> 4 = Alteração de chave em andamento<br /><br /> 5 = Descriptografia em andamento<br /><br /> 6 = Alteração de proteção em andamento (o certificado ou a chave assimétrica que está criptografando a chave de criptografia do banco de dados está sendo alterado)|  
|create_date|**datetime**|Exibe a data (em UTC) a chave de criptografia foi criada.|  
|regenerate_date|**datetime**|Exibe a data (em UTC) da chave de criptografia foi gerada novamente.|  
|modify_date|**datetime**|Exibe a data (em UTC) da chave de criptografia foi modificada.|  
|set_date|**datetime**|Exibe a data (em UTC), a chave de criptografia foi aplicada ao banco de dados.|  
|opened_date|**datetime**|Mostra quando (em UTC) a chave de banco de dados foi aberto pela última vez.|  
|key_algorithm|**nvarchar(32)**|Exibe o algoritmo que é usado para a chave.|  
|key_length|**int**|Exibe o comprimento da chave.|  
|encryptor_thumbprint|**varbinary(20)**|Mostra a impressão digital do criptografador.|  
|encryptor_type|**nvarchar(32)**|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> Descreve o criptografador.|  
|percent_complete|**real**|Porcentagem concluída da alteração de estado da criptografia do banco de dados. Será 0 se não houver nenhuma alteração de estado.|
|encryption_state_desc|**nvarchar(32)**|**Aplica-se ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores.<br><br> Cadeia de caracteres que indica se o banco de dados é criptografado ou não criptografado.<br><br>Nenhuma<br><br>NÃO CRIPTOGRAFADO<br><br>CRIPTOGRAFADO<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**Aplica-se ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores.<br><br>Indica o estado atual da verificação de criptografia. <br><br>0 = nenhuma verificação tiver sido iniciada, TDE não está habilitado.<br><br>1 = verificação estiver em andamento.<br><br>2 = verificação está em andamento, mas foi suspenso, o usuário pode retomar.<br><br>3 = verificação for concluída com êxito, a TDE é habilitada e a criptografia está concluída.<br><br>4 = verificação foi anulada por algum motivo, será necessária intervenção manual. Entre em contato com o Microsoft Support para obter mais assistência.|
|encryption_scan_state_desc|**nvarchar(32)**|**Aplica-se ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores.<br><br>Cadeia de caracteres que indica o estado atual da verificação de criptografia.<br><br> Nenhuma<br><br>RUNNING<br><br>SUSPENDED<br><br>CONCLUIR<br><br>ABORTED|
|encryption_scan_modify_date|**datetime**|**Aplica-se ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores.<br><br> Exibe a data (em UTC) o estado de verificação de criptografia foi modificado pela última vez.|
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   

## <a name="see-also"></a>Consulte também  

 [Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
