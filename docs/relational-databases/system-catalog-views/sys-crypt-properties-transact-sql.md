---
description: sys.crypt_properties (Transact-SQL)
title: sys. crypt_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- crypt_properties
- crypt_properties_TSQL
- sys.crypt_properties_TSQL
- sys.crypt_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.crypt_properties catalog view
ms.assetid: d5684f5a-30b1-418e-ae4d-ab040db9257e
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4feac22b04fb06053441e046fd9f35ece6dbd33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469942"
---
# <a name="syscrypt_properties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada propriedade criptográfica associada a um item protegível.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|Identifica a classe na qual a propriedade existe.<br /><br /> 1 = Objeto ou coluna<br /> 5 = Assembly|  
|**class_desc**|**nvarchar(60)**|Descrição da classe na qual a propriedade existe.<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|ID na qual a propriedade existe, interpretada de acordo com a classe.|  
|**digitais**|**varbinary(32)**|Hash SHA-1 do certificado ou chave assimétrica usado.|  
|**crypt_type**|**Char (4)**|Tipo de criptografia.<br /><br /> SPVC = assinado por chave privada do certificado<br /><br /> SPVA = assinado por chave privada assimétrica<br /><br /> CPVC = Assinatura do contador pela chave privada de certificado<br /><br /> CPVA = Assinatura do contador pela chave assimétrica|  
|**crypt_type_desc**|**nvarchar(60)**|Descrição do tipo de criptografia.<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|Bits assinados ou criptografados. Para um módulo assinado, esses são os bits de assinatura do módulo.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
