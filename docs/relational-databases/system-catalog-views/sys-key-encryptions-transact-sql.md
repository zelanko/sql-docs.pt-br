---
title: key_encryptions (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a8fb9b2103316219bcdac74c1b861ac0a2668cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853680"
---
# <a name="syskeyencryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada criptografia de chave simétrica especificada usando a cláusula ENCRYPTION BY da instrução CREATE SYMMETRIC KEY.  

  
|Nomes de coluna|Tipos de dados|Description|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|ID da chave criptografada.|  
|**impressão digital**|**varbinary(32)**|O hash SHA-1 do certificado com o qual a chave é criptografada, ou o GUID da chave simétrica com a qual a chave é criptografada. |  
|**crypt_type**|**char(4)**|Tipo de criptografia:<br /><br /> ESKS = Criptografado com chave simétrica<br /><br /> ESP3, ESP2 ou ESKP = criptografado com senha<br /><br /> EPUC = Criptografado com certificado<br /><br /> EPUA = Criptografado com chave assimétrica<br /><br /> ESKM = Criptografado com chave mestra|  
|**crypt_type_desc**|**nvarchar(60)**|Descrição do tipo de criptografia:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(Começando com [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)], inclui um número de versão para ser usado por CSS.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> Observação: O Windows DPAPI é usado para proteger a chave mestra de serviço.|  
|**crypt_property**|**varbinary(max)**|Bits assinados ou criptografados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
