---
description: sys.certificates (Transact-SQL)
title: sys. Certificates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 95e4d3b3b1b06810fc1e60564a4ad7c84e85189a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486503"
---
# <a name="syscertificates-transact-sql"></a>sys.certificates (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada certificado no banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do certificado. É exclusiva no banco de dados.|  
|**certificate_id**|**int**|ID do certificado. É exclusiva no banco de dados.|  
|**principal_id**|**int**|ID do principal de banco de dados que é o proprietário deste certificado.|  
|**pvt_key_encryption_type**|**char(2)**|Como a chave privada é criptografada.<br /><br /> NA = Não há nenhuma chave privada para o certificado<br /><br /> MK = A chave privada é criptografada pela chave mestra<br /><br /> PW = A chave privada é criptografada por uma senha definida pelo usuário<br /><br /> SK = A chave privada é criptografada pela chave mestra de serviço|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|Descrição de como a chave privada é criptografada.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|Se for 1, este certificado é usado para iniciar caixas de diálogo de serviço criptografadas.|  
|**issuer_name**|**nvarchar (442)**|Nome do emissor do certificado.|  
|**cert_serial_number**|**nvarchar (64)**|Número de série do certificado.|  
|**sid**|**varbinary (85)**|SID de logon para este certificado.|  
|**string_sid**|**nvarchar(128)**|Representação da cadeia de caracteres do SID de logon para este certificado|  
|**subject**|**nvarchar(4000)**|Assunto deste certificado.|  
|**expiry_date**|**datetime**|Quando o certificado expira.|  
|**start_date**|**datetime**|Quando o certificado é validado.|  
|**digitais**|**varbinary(32)**|Hash SHA-1 do certificado. O hash SHA-1 é globalmente exclusivo.|  
|**attested_by**|**nvarchar(260)**|Somente para uso do sistema.|  
|**pvt_key_last_backup_date**|**datetime**|A data e a hora em que a chave privada do certificado foi exportada pela última vez.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
