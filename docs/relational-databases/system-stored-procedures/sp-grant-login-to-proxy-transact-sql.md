---
title: sp_grant_login_to_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 913c86bce2b9e003c3e5c9f701ba5824611459d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spgrantlogintoproxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)
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
 [ **@login_name** = ] **'***login_name***'**  
 O nome de logon para o qual o acesso será concedido. O *login_name* é **nvarchar (256)**, com um padrão NULL. Um dos **@login_name**, **@fixed_server_role**, ou **@msdb_role** devem ser especificados, ou o procedimento armazenado falhará.  
  
 [ **@fixed_server_role**= ] **'***fixed_server_role***'**  
 A função de servidor fixa para a qual o acesso será concedido. O *fixed_server_role* é **nvarchar (256)**, com um padrão NULL. Um dos **@login_name**, **@fixed_server_role**, ou **@msdb_role** devem ser especificados, ou o procedimento armazenado falhará.  
  
 [ **@msdb_role**= ] '*msdb_role*'  
 A função de banco de dados no **msdb** banco de dados para conceder acesso a. O *msdb_role* é **nvarchar (256)**, com um padrão NULL. Um dos **@login_name**, **@fixed_server_role**, ou **@msdb_role** devem ser especificados, ou o procedimento armazenado falhará.  
  
 [ **@proxy_id**= ] *id*  
 O identificador do proxy ao qual o acesso será concedido. O *id* é **int**, com um padrão NULL. Um dos **@proxy_id** ou **@proxy_name** devem ser especificados, ou o procedimento armazenado falhará.  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 O nome do proxy ao qual o acesso será concedido. O *proxy_name* é **nvarchar (256)**, com um padrão NULL. Um dos **@proxy_id** ou **@proxy_name** devem ser especificados, ou o procedimento armazenado falhará.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_grant_login_to_proxy** deve ser executado a partir de **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_grant_login_to_proxy**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir permite que o logon `adventure-works\terrid` use o proxy `Catalog application proxy`.  
  
```  
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
  
  
