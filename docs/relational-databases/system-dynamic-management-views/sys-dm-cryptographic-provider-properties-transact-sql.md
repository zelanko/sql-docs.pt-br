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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be99b97a8dc873866a7437f2e11f7e5d3588fec8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717459"
---
# <a name="sysdm_cryptographic_provider_properties-transact-sql"></a>sys.dm_cryptographic_provider_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre provedores criptográficos registrados.  
  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|Número de identificação do provedor criptográfico.|  
|guid|**uniqueidentifier**|GUID de provedor exclusivo.|  
|provider_version|**nvarchar(256)**|Versão do provedor no formato '*AA.BB.cccc.DD*'.|  
|sqlcrypt_version|**nvarchar(256)**|Versão principal da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API de criptografia no formato '*AA.BB.cccc.DD*'.|  
|friendly_name|**nvarchar(2048)**|Nome fornecido pelo provedor.|  
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
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CRIAR provedor CRIPTOGRÁFICO &#40;&#41;Transact-SQL](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
