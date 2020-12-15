---
description: sys.sql_logins (Transact-SQL)
title: sys.sql_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb0fc659d82024dbbc52dc777b9f6ae5da3062ac
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477327"
---
# <a name="syssql_logins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Retorna uma linha para todo logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|Herda de **Sys.server_principals**.|  
|**com_política_verificada**|**bit**|Política de Senha é verificada.|  
|**com_expiração_verificada**|**bit**|Expiração de Senha é verificada.|  
|**password_hash**|**varbinary(256)**|Hash de SQL logon senha. Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.|  
  
 Para obter uma lista de colunas que essa exibição herda, consulte [sys.server_principals &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). As colunas `owning_principal_id` e `is_fixed_role` não são herdadas de sys.server_principals.
  
## <a name="remarks"></a>Comentários  
 Para exibir os logons de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação e os logons de autenticação do Windows, confira [sys.server_principals &#40;&#41;TRANSACT-SQL ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Quando os usuários de banco de dados independentes estiverem habilitados, as conexões poderão ser feitas sem logons. Para identificar essas contas, confira  [sys.database_principals &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Os logons de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ver seu próprio nome de logon e o logon de sa. Ver outros logons requer ALTER ANY LOGIN ou uma permissão no logon.  
 Para exibir o conteúdo da coluna password_hash, a permissão CONTROL SERVER é necessária.
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Política de senha](../../relational-databases/security/password-policy.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
