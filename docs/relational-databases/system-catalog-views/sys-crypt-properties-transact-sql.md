---
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
ms.openlocfilehash: 9655866d4fd2d6f98b38532f77f94bc12f16f9b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68109478"
---
# <a name="syscrypt_properties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada propriedade criptográfica associada a um item protegível.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**classe**|**tinyint**|Identifica a classe na qual a propriedade existe.<br /><br /> 1 = Objeto ou coluna<br /> 5 = Assembly|  
|**class_desc**|**nvarchar(60)**|Descrição da classe na qual a propriedade existe.<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|ID na qual a propriedade existe, interpretada de acordo com a classe.|  
|**thumbprint**|**varbinary(32)**|Hash SHA-1 do certificado ou chave assimétrica usado.|  
|**crypt_type**|**Char (4)**|Tipo de criptografia.<br /><br /> SPVC = assinado por chave privada do certificado<br /><br /> SPVA = assinado por chave privada assimétrica<br /><br /> CPVC = Assinatura do contador pela chave privada de certificado<br /><br /> CPVA = Assinatura do contador pela chave assimétrica|  
|**crypt_type_desc**|**nvarchar(60)**|Descrição do tipo de criptografia.<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|Bits assinados ou criptografados. Para um módulo assinado, esses são os bits de assinatura do módulo.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Protegíveis](../../relational-databases/security/securables.md)   
 [CRIAR certificado &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CRIAR chave simétrica &#40;&#41;Transact-SQL](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CRIAR chave assimétrica &#40;&#41;Transact-SQL](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
