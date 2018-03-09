---
title: key_encryptions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba1c62078f0400436a21749b28c302d2f8a2509e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="syskeyencryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada criptografia de chave simétrica especificada usando a cláusula ENCRYPTION BY da instrução CREATE SYMMETRIC KEY.  

  
|Nomes de coluna|Tipos de dados|Description|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|ID da chave criptografada.|  
|**impressão digital**|**varbinary(32)**|O hash SHA-1 do certificado com o qual a chave é criptografada, ou o GUID da chave simétrica com a qual a chave é criptografada. |  
|**crypt_type**|**char(4)**|Tipo de criptografia:<br /><br /> ESKS = Criptografado com chave simétrica<br /><br /> ESP3, ESP2 ou ESKP = criptografado com senha<br /><br /> EPUC = Criptografado com certificado<br /><br /> EPUA = Criptografado com chave assimétrica<br /><br /> ESKM = Criptografado com chave mestra|  
|**crypt_type_desc**|**nvarchar (60)**|Descrição do tipo de criptografia:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(Começando com [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)], inclui um número de versão para uso pelo CSS.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> Observação: O Windows DPAPI é usado para proteger a chave mestra de serviço.|  
|**crypt_property**|**varbinary(max)**|Bits assinados ou criptografados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
