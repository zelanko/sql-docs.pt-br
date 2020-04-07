---
title: sys.master_key_passwords (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 926acd9beb00102e19dbc2844e282d74bc890915
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752900"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Retorna uma linha para cada senha de chave-mestre do banco de dados adicionada usando o **procedimento sp_control_dbmasterkey_password** armazenado. As senhas que são usadas para proteger as chaves mestras são armazenadas no armazenamento de credenciais. O nome da credencial segue este formato: ##DBMKEY_<database_family_guid>_<<random_password_guid>##. A senha é armazenada como o segredo de credencial. Para cada senha adicionada usando **sp_control_dbmasterkey_password,** há uma linha em **sys.credentials**.  
  
 Cada linha nesta exibição mostra um **credential_id** e a **family_guid** de um banco de dados a chave mestra da qual é protegida pela senha associada a essa credencial. Uma adesão com **sys.credentials** no **credential_id** retornará campos úteis, como o **create_date** e o nome de credencial.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**credential_id**|**Int**|A ID da credencial à qual a senha pertence. Essa ID é exclusiva na instância de servidor.|  
|**family_guid**|**Uniqueidentifier**|ID exclusiva do banco de dados original na criação. Esse GUID permanece o mesmo depois que o banco de dados é restaurado ou anexado, mesmo que o nome de banco de dados seja alterado.<br /><br /> Se a descriptografia automática pela tecla mestre do serviço falhar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use o **family_guid** para identificar credenciais que possam conter a senha usada para proteger a chave mestra do banco de dados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizações do catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Visualizações do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CRIE&#41;de &#40;de chave simétrica Transact-SQL](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Hierarquia de Criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
