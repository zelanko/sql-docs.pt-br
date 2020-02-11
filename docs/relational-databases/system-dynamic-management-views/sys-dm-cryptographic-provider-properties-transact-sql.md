---
title: sys. dm_cryptographic_provider_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_properties_TSQL
- sys.dm_cryptographic_provider_properties
- sys.dm_cryptographic_provider_properties_TSQL
- dm_cryptographic_provider_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_properties dynamic management view
ms.assetid: 024b0095-6766-4189-a39a-d316c5ec2874
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc1e0915fb48b42429bb2821476f98154ac39451
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005105"
---
# <a name="sysdm_cryptographic_provider_properties-transact-sql"></a>sys.dm_cryptographic_provider_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre provedores criptográficos registrados.  
  
 
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|Número de identificação do provedor criptográfico.|  
|guid|**uniqueidentifier**|GUID de provedor exclusivo.|  
|provider_version|**nvarchar(256)**|Versão do provedor no formato '*AA.BB.cccc.DD*'.|  
|sqlcrypt_version|**nvarchar(256)**|Versão principal da API [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de criptografia no formato '*AA.BB.cccc.DD*'.|  
|friendly_name|**nvarchar (2048)**|Nome fornecido pelo provedor.|  
|authentication_type|**nvarchar(256)**|WINDOWS, básico ou outro.|  
|symmetric_key_support|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|symmetric_key_export|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|symmetric_key_import|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|symmetric_key_persistance|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|asymmetric_key_support|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|asymmetric_key_export|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|symmetric_key_import|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
|symmetric_key_persistance|**tinyint**|0 (sem suporte)<br /><br /> 1 (com suporte)|  
  
## <a name="remarks"></a>Comentários  
 A exibição de sys.dm_cryptographic_provider_properties é visível ao público.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
