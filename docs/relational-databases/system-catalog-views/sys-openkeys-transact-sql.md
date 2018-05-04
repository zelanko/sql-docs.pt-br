---
title: sys.openkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- openkeys_TSQL
- sys.openkeys_TSQL
- openkeys
- sys.openkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.openkeys catalog view
ms.assetid: 719a1259-2398-4fcb-ba05-aeabba7aec21
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6e16cc3964806c3e92b6add8add18572a64b0bfc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysopenkeys-transact-sql"></a>sys.openkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esta exibição do catálogo retorna informações sobre as chaves de criptografia que estão abertas na sessão atual.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|ID do banco de dados que contém a chave.|  
|**database_name**|**sysname**|Nome do banco de dados que contém a chave.|  
|**key_id**|**Int**|ID da chave. A ID é exclusiva no banco de dados.|  
|**key_name**|**sysname**|Nome da chave. Exclusiva no banco de dados.|  
|**key_guid**|**varbinary**|GUID da chave. Exclusiva no banco de dados.|  
|**opened_date**|**datetime**|Data e hora em que a chave foi aberta.|  
|**status**|**Int**|1 se a chave for válida em metadados. 0 se a chave não for localizada em metadados.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)  
  
  
