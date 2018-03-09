---
title: master_key_passwords (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bb1977fb034f2fd2c682b12b4466bd7914009dd
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysmasterkeypasswords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada senha de chave mestra de banco de dados adicionada usando o **sp_control_dbmasterkey_password** procedimento armazenado. As senhas que são usadas para proteger as chaves mestras são armazenadas no armazenamento de credenciais. O nome da credencial segue este formato: ##DBMKEY_<database_family_guid>_<random_password_guid>##. A senha é armazenada como o segredo de credencial. Para cada senha adicionada usando **sp_control_dbmasterkey_password**, há uma linha em **Credentials**.  
  
 Cada linha nessa exibição mostra uma **credential_id** e **family_guid** de um banco de dados que a chave mestra do que é protegida por senha associada a essa credencial. Uma junção com **Credentials** no **credential_id** retornará campos úteis, como o **create_date** e o nome da credencial.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|A ID da credencial à qual a senha pertence. Essa ID é exclusiva na instância de servidor.|  
|**family_guid**|**uniqueidentifier**|ID exclusiva do banco de dados original na criação. Esse GUID permanece o mesmo depois que o banco de dados é restaurado ou anexado, mesmo que o nome de banco de dados seja alterado.<br /><br /> Se a descriptografia automática feita pela chave mestra de serviço falhar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o **family_guid** para identificar as credenciais que podem conter a senha usada para proteger a chave mestra de banco de dados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
