---
title: Certificates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- certificates
- certificates_TSQL
- sys.certificates_TSQL
- sys.certificates
dev_langs:
- TSQL
helpviewer_keywords:
- sys.certificates catalog view
ms.assetid: e5046102-a65c-401e-b80d-05636884dec9
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3616c3aa2b141f5f6467d048a2baa92511f1090e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syscertificates-transact-sql"></a>sys.certificates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada certificado no banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do certificado. É exclusiva no banco de dados.|  
|**certificate_id**|**Int**|ID do certificado. É exclusiva no banco de dados.|  
|**principal_id**|**Int**|ID do principal de banco de dados que é o proprietário deste certificado.|  
|**pvt_key_encryption_type**|**char(2)**|Como a chave privada é criptografada.<br /><br /> NA = Não há nenhuma chave privada para o certificado<br /><br /> MK = A chave privada é criptografada pela chave mestra<br /><br /> PW = A chave privada é criptografada por uma senha definida pelo usuário<br /><br /> SK = A chave privada é criptografada pela chave mestra de serviço|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|Descrição de como a chave privada é criptografada.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|Se for 1, este certificado é usado para iniciar caixas de diálogo de serviço criptografadas.|  
|**issuer_name**|**nvarchar(442)**|Nome do emissor do certificado.|  
|**cert_serial_number**|**nvarchar(64)**|Número de série do certificado.|  
|**sid**|**varbinary(85)**|SID de logon para este certificado.|  
|**string_sid**|**nvarchar(128)**|Representação da cadeia de caracteres do SID de logon para este certificado|  
|**subject**|**nvarchar(4000)**|Assunto deste certificado.|  
|**expiry_date**|**datetime**|Quando o certificado expira.|  
|**start_date**|**datetime**|Quando o certificado é validado.|  
|**Impressão digital**|**varbinary(32)**|Hash SHA-1 do certificado. O hash SHA-1 é globalmente exclusivo.|  
|**attested_by**|**nvarchar(260)**|Somente para uso do sistema.|  
|pvt_key_last_backup_date|**datetime**|A data e hora da última exportação da chave privada do certificado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
