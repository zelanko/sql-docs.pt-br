---
title: symmetric_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
- symmetric_keys
- sys.symmetric_keys
- sys.symmetric_keys_TSQL
- symmetric_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.symmetric_keys catalog view
ms.assetid: d410eae1-3a52-45de-b9a1-52d2bd93a8eb
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bf3916f92f71e0d5ca7ec3b1a994b4c9a46bf913
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syssymmetrickeys-transact-sql"></a>sys.symmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada chave simétrica criada com a instrução CREATE SYMMETRIC KEY.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da chave. É exclusivo no c4database.|  
|**principal_id**|**Int**|ID da entidade de banco de dados que possui a chave.|  
|**symmetric_key_id**|**Int**|ID da chave. Exclusiva no banco de dados.|  
|**key_length**|**Int**|Comprimento da chave em bits.|  
|**key_algorithm**|**char(2)**|Algoritmo usado com a chave:<br /><br /> R2 = RC2<br /><br /> R4 = RC4<br /><br /> D = DES<br /><br /> D3 = DES triplo<br /><br /> DT = TRIPLE_DES_3KEY<br /><br /> DX = DESX<br /><br /> A1 = AES 128<br /><br /> A2 = AES 192<br /><br /> A3 = AES 256<br /><br /> NA = Chave EKM|  
|**algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo usado com a chave:<br /><br /> RC2<br /><br /> RC4<br /><br /> DES<br /><br /> Triple_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256<br /><br /> NULL (somente algoritmos de Gerenciador de Chave Extensível)|  
|**create_date**|**datetime**|A data em que a chave foi criada.|  
|**modify_date**|**datetime**|A data em que a chave foi modificada.|  
|**key_guid**|**uniqueidentifier**|Identificador globalmente exclusivo (GUID) associado à chave. É gerado automaticamente para chaves persistentes. Os GUIDs para chaves temporárias são derivados da frase secreta fornecida pelo usuário.|  
|**key_thumbprint**|**sql_variant**|Hash SHA-1 da chave. O hash é globalmente exclusivo. Para chaves de Gerenciamento de Chave não Extensível, esse valor será NULL.|  
|**provider_type**|**nvarchar(120)**|Tipo de provedor criptográfico:<br /><br /> CRYPTOGRAPHIC PROVIDER = Chaves de Gerenciamento de Chave Extensível<br /><br /> NULL = Chaves de Gerenciamento de Chave não Extensível|  
|**cryptographic_provider_guid**|**uniqueidentifier**|GUID do provedor criptográfico. Para chaves de Gerenciamento de Chave não Extensível, esse valor será NULL.|  
|**cryptographic_provider_algid**|**sql_variant**|ID de algoritmo do provedor criptográfico. Para chaves de Gerenciamento de Chave não Extensível, esse valor será NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Remarks  
 O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
 **Esclarecimento em relação aos algoritmos DES:**  
  
-   O DESX foi nomeado incorretamente. As chaves simétricas criadas com ALGORITHM = DESX na verdade usam a cifra TRIPLE DES com uma chave de 192 bits. O algoritmo DESX não é fornecido. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
-   As chaves simétricas criadas com ALGORITHM = TRIPLE_DES_3KEY usam TRIPLE DES com uma chave de 192 bits.  
  
-   As chaves simétricas criadas com ALGORITHM = TRIPLE_DES usam TRIPLE DES com uma chave de 128 bits.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
