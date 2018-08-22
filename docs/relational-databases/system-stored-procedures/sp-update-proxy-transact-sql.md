---
title: sp_update_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31154f48d9d13e6ebb67b25919a45ff7a1f7db8b
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392924"
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um proxy existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id**= ] *id*  
 O número de identificação de proxy do proxy a ser alterado. O *proxy_id* é **int**, com um padrão NULL.  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 O nome do proxy a ser alterado. O *proxy_name* é **sysname**, com um padrão NULL.  
  
 [ **@credential_name** =] **'***credential_name***'**  
 O nome da nova credencial para o proxy. O *credential_name* é **sysname**, com um padrão NULL. Qualquer um dos *credential_name* ou *credential_id* pode ser especificado.  
  
 [ **@credential_id** =] *credential_id*  
 O número de identificação da nova credencial para o proxy. O *credential_id* é **int**, com um padrão NULL. Qualquer um dos *credential_name* ou *credential_id* pode ser especificado.  
  
 [ **@new_name**= ] **'***new_name***'**  
 O novo nome do proxy. O *new_name* é **sysname**, com um padrão NULL. Quando fornecido, o procedimento altera o nome do proxy a ser *new_name*. Quando esse argumento for NULL, o nome do proxy permanecerá inalterado.  
  
 [ **@enabled** =] *is_enabled*  
 É se o proxy está habilitado. O *is_enabled* sinalizador é **tinyint**, com um padrão NULL. Quando *is_enabled* é **0**, o proxy não está habilitado e não pode ser usado por uma etapa de trabalho. Quando esse argumento for NULL, o status do proxy permanecerá inalterado.  
  
 [ **@description**=] **'***descrição***'**  
 A nova descrição do proxy. O *descrição* é **nvarchar(512)**, com um padrão NULL. Quando esse argumento for NULL, a descrição do proxy permanecerá inalterada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Qualquer um dos **@proxy_name** ou **@proxy_id** deve ser especificado. Se os dois argumentos forem especificados, eles deverão se referir ao mesmo proxy, caso contrário o procedimento armazenado falhará.  
  
 Qualquer um dos **@credential_name** ou **@credential_id** deve ser especificado para alterar a credencial para o proxy. Se os dois argumentos forem especificados, eles deverão se referir à mesma credencial, caso contrário o procedimento armazenado falhará.  
  
 Esse procedimento altera o proxy, mas não altera o acesso a ele. Para alterar o acesso a um proxy, use **sp_grant_login_to_proxy** e **sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** fixo de segurança podem executar este procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define o valor habilitado para o proxy `Catalog application proxy` como `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
