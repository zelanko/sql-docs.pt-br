---
title: sys. master_key_passwords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a29e6db2af545f919ad176f3b7453e237b08888b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883814"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Retorna uma linha para cada senha de chave mestra de banco de dados adicionada usando o procedimento armazenado **sp_control_dbmasterkey_password** . As senhas que são usadas para proteger as chaves mestras são armazenadas no armazenamento de credenciais. O nome da credencial segue este formato: # #DBMKEY_<database_family_guid>_<random_password_guid> # #. A senha é armazenada como o segredo de credencial. Para cada senha adicionada usando **sp_control_dbmasterkey_password**, há uma linha em **Sys. Credentials**.  
  
 Cada linha nessa exibição mostra uma **credential_id** e a **family_guid** de um banco de dados a chave mestra que é protegida pela senha associada a essa credencial. Uma junção com **Sys. Credentials** na **credential_id** retornará campos úteis, como o **create_date** e o nome da credencial.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|A ID da credencial à qual a senha pertence. Essa ID é exclusiva na instância de servidor.|  
|**family_guid**|**uniqueidentifier**|ID exclusiva do banco de dados original na criação. Esse GUID permanece o mesmo depois que o banco de dados é restaurado ou anexado, mesmo que o nome de banco de dados seja alterado.<br /><br /> Se a descriptografia automática pela chave mestra de serviço falhar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o usará o **family_guid** para identificar as credenciais que podem conter a senha usada para proteger a chave mestra do banco de dados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CRIAR chave simétrica &#40;&#41;Transact-SQL](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
