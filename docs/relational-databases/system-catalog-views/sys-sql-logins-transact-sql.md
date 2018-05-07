---
title: sys. sql_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cdf6447b7673606224852078f80306c4b7fb4632
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syssqllogins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Retorna uma linha para todo logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**|--|Herda de **sys. server_principals**.|  
|**is_policy_checked**|**bit**|Política de Senha é verificada.|  
|**is_expiration_checked**|**bit**|Expiração de Senha é verificada.|  
|**password_hash**|**varbinary(256)**|Hash de SQL logon senha. Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.|  
  
 Para obter uma lista de colunas que essa exibição herda valores, consulte [sys. server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Para exibir tanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons de autenticação e logons de autenticação do Windows, consulte [sys. server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Quando estiver contido os usuários de banco de dados estão habilitados, conexões podem ser feitas sem logons. Para identificar essas contas, consulte [database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Os logons de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ver seu próprio nome de logon e o logon de sa. Ver outros logons requer ALTER ANY LOGIN ou uma permissão no logon.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Política de senha](../../relational-databases/security/password-policy.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
