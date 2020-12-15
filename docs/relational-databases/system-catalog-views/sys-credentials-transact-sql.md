---
description: sys.credentials (Transact-SQL)
title: sys. Credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs:
- TSQL
helpviewer_keywords:
- sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3dfd50d16275a65c7e923a60c3c478b450e3e812
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472997"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  Retorna uma linha para cada credencial de nível de servidor.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|ID da credencial. É exclusivo no servidor.|  
|name|**sysname**|Nome da credencial. É exclusivo no servidor.|  
|credential_identity|**nvarchar(4000)**|Nome da identidade a ser usada. Geralmente é um usuário do Windows. Não precisa ser exclusivo.|  
|create_date|**datetime**|Hora em que a credencial foi criada.|  
|modify_date|**datetime**|Hora da última modificação feita na credencial.|  
|target_type|**nvarchar (100)**|Tipo de credencial. Retorna NULL para credenciais tradicionais e CRYPTOGRAPHIC PROVIDER para credenciais mapeadas para um provedor criptográfico. Para obter mais informações sobre provedores de gerenciamento de chaves externas, consulte [gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  
|target_id|**int**|ID do objeto para o qual a credencial é mapeada. Retorna 0 para credenciais tradicionais e um valor diferente de 0 para credenciais mapeadas para um provedor criptográfico. Para obter mais informações sobre provedores de gerenciamento de chaves externas, consulte [gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  

## <a name="remarks"></a>Comentários  
Para obter credenciais de nível de banco de dados, consulte [Sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).
  
## <a name="permissions"></a>Permissões  
 Requer `VIEW ANY DEFINITION` permissão ou `ALTER ANY CREDENTIAL` permissão. Além disso, a entidade de segurança não deve ter a permissão negada `VIEW ANY DEFINITION` .  
  
## <a name="see-also"></a>Consulte Também  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
