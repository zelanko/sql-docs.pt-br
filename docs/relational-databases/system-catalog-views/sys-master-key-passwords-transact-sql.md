---
description: sys.master_key_passwords (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c928b85aed482e774b8b180c6f97c2138f7ad0d0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539670"
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
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
