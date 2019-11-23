---
title: sp_grant_login_to_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: bdfeab5754a2397c01ace2bb9f822fa168eeef6b
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005859"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede um acesso de entidade de segurança a um proxy.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login_name = ] 'login_name'` o nome de logon para conceder acesso ao. O *login_name* é **nvarchar (256)** , com um padrão de NULL. Um dos **\@login_name**, **\@fixed_server_role**ou **\@** msdb_role deve ser especificado ou o procedimento armazenado falhará.  
  
`[ @fixed_server_role = ] 'fixed_server_role'` a função de servidor fixa para conceder acesso ao. O *fixed_server_role* é **nvarchar (256)** , com um padrão de NULL. Um dos **\@login_name**, **\@fixed_server_role**ou **\@** msdb_role deve ser especificado ou o procedimento armazenado falhará.  
  
`[ @msdb_role = ] 'msdb_role'` a função de banco de dados no banco de dados **msdb** para conceder acesso ao. O *msdb_role* é **nvarchar (256)** , com um padrão de NULL. Um dos **\@login_name**, **\@fixed_server_role**ou **\@** msdb_role deve ser especificado ou o procedimento armazenado falhará.  
  
`[ @proxy_id = ] id` o identificador do proxy para o qual conceder acesso. A *ID* é **int**, com um padrão de NULL. Um dos **\@proxy_id** ou **\@proxy_name** deve ser especificado ou o procedimento armazenado falha.  
  
`[ @proxy_name = ] 'proxy_name'` o nome do proxy para o qual conceder acesso. O *proxy_name* é **nvarchar (256)** , com um padrão de NULL. Um dos **\@proxy_id** ou **\@proxy_name** deve ser especificado ou o procedimento armazenado falha.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_grant_login_to_proxy** deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_grant_login_to_proxy**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir permite que o logon `adventure-works\terrid` use o proxy `Catalog application proxy`.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
