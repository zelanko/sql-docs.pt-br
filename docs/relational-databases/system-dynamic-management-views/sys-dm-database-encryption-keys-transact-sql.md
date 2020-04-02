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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e716c826fd366fda4505b7fcf9ec8e3b756ec25
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531056"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre o estado de criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas. Para obter mais informações sobre a criptografia do banco de dados, confira [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**Int**|ID do banco de dados.|  
|encryption_state|**Int**|Indica se o banco de dados está criptografado ou não.<br /><br /> 0 = Nenhuma chave de criptografia de banco de dados presente, nenhuma criptografia<br /><br /> 1 = Sem-criptografia<br /><br /> 2 = Criptografia em andamento<br /><br /> 3 = Criptografado<br /><br /> 4 = Alteração de chave em andamento<br /><br /> 5 = Descriptografia em andamento<br /><br /> 6 = Alteração de proteção em andamento (o certificado ou a chave assimétrica que está criptografando a chave de criptografia do banco de dados está sendo alterado)|  
|create_date|**Datetime**|Exibe a data (em UTC) a chave de criptografia foi criada.|  
|regenerate_date|**Datetime**|Exibe a data (em UTC) a chave de criptografia foi regenerada.|  
|modify_date|**Datetime**|Exibe a data (em UTC) a chave de criptografia foi modificada.|  
|set_date|**Datetime**|Exibe a data (em UTC) a chave de criptografia foi aplicada ao banco de dados.|  
|opened_date|**Datetime**|Mostra quando (em UTC) a chave de banco de dados foi aberta pela última vez.|  
|key_algorithm|**nvarchar(32)**|Exibe o algoritmo que é usado para a chave.|  
|key_length|**Int**|Exibe o comprimento da chave.|  
|encryptor_thumbprint|**varbinary(20)**|Mostra a impressão digital do criptografador.|  
|encryptor_type|**nvarchar(32)**|**Aplica-se** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] : (através da [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> Descreve o criptografador.|  
|percent_complete|**real**|Porcentagem concluída da alteração de estado da criptografia do banco de dados. Será 0 se não houver nenhuma alteração de estado.|
|encryption_state_desc|**nvarchar(32)**|**Aplica-se** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e depois.<br><br> String que indica se o banco de dados está criptografado ou não criptografado.<br><br>Nenhuma<br><br>Criptografado<br><br>Criptografado<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**Int**|**Aplica-se** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e depois.<br><br>Indica o estado atual da varredura de criptografia. <br><br>0 = Nenhuma varredura foi iniciada, o TDE não está habilitado<br><br>1 = A varredura está em andamento.<br><br>2 = A varredura está em andamento, mas foi suspensa, o usuário pode retomar.<br><br>3 = A varredura foi abortada por algum motivo, é necessária uma intervenção manual. Entre em contato com o Suporte da Microsoft para obter mais assistência.<br><br>4 = A varredura foi concluída com sucesso, o TDE está ativado e a criptografia está completa.|
|encryption_scan_state_desc|**nvarchar(32)**|**Aplica-se** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e depois.<br><br>String que indica o estado atual da varredura de criptografia.<br><br> Nenhuma<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>Completa|
|encryption_scan_modify_date|**Datetime**|**Aplica-se** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e depois.<br><br> Exibe a data (em UTC) o estado de varredura de criptografia foi modificado pela última vez.|
  
## <a name="permissions"></a>Permissões

Ligado, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] `VIEW SERVER STATE` requer permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Níveis Premium, `VIEW DATABASE STATE` requer a permissão no banco de dados. Nos [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] níveis Padrão e Básico, requer o **administrador do Servidor** ou uma conta de administração do **Azure Active Directory.**   

## <a name="see-also"></a>Consulte também  

 [Visualizações e funções de gerenciamento dinâmico relacionadas à segurança &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Criptografia de dados transparente &#40;&#41;TDE](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [Criptografia do servidor SQL](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Chaves de criptografia de servidor e banco de dados sql &#40;&#41;do mecanismo de banco de dados](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Hierarquia de Criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTERAR opções de conjunto de banco de dados &#40;&#41;Transact-SQL](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CRIAR CHAVE DE CRIPTOGRAFIA DE BANCO DE DADOS &#40;transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
