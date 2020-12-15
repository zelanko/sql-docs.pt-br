---
description: sys.key_encryptions (Transact-SQL)
title: sys.key_encryptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c841e05d54ee5ba672107426c2f10b2396b84a76
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472987"
---
# <a name="syskey_encryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada criptografia de chave simétrica especificada usando a cláusula ENCRYPTION BY da instrução CREATE SYMMETRIC KEY.  

  
|Nomes de coluna|Tipos de dados|Descrição|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|ID da chave criptografada.|  
|**thumbprint**|**varbinary(32)**|O hash SHA-1 do certificado com o qual a chave é criptografada, ou o GUID da chave simétrica com a qual a chave é criptografada. |  
|**crypt_type**|**Char (4)**|Tipo de criptografia:<br /><br /> ESKS = Criptografado com chave simétrica<br /><br /> ESKP, ESP2 ou ESP3 = criptografado por senha<br /><br /> EPUC = Criptografado com certificado<br /><br /> EPUA = Criptografado com chave assimétrica<br /><br /> ESKM = Criptografado com chave mestra|  
|**crypt_type_desc**|**nvarchar(60)**|Descrição do tipo de criptografia:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(Começando com [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] o, inclui um número de versão para uso pelo CSS.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> Observação: o Windows DPAPI é usado para proteger a chave mestra de serviço.|  
|**crypt_property**|**varbinary(max)**|Bits assinados ou criptografados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
