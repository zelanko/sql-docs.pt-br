---
title: sp_revoke_login_from_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 193760ec432a67b8cf428f7e0207d6fd8174a5c6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750500"
---
# <a name="sp_revoke_login_from_proxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove o acesso a um proxy para um principal de segurança.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`O nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, da função de servidor ou da função de banco de dados **msdb** para a qual remover o acesso. *nome* é **nvarchar (256)** sem padrão.  
  
`[ @proxy_id = ] id`A ID do proxy para o qual remover o acesso. A *ID* ou a *proxy_name* deve ser especificada, mas não é possível especificá-las. A *ID* é **int**, com um padrão de NULL.  
  
`[ @proxy_name = ] 'proxy_name'`O nome do proxy para o qual remover o acesso. A *ID* ou a *proxy_name* deve ser especificada, mas não é possível especificá-las. O *proxy_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Os trabalhos que pertencem ao logon que referencia esse proxy não serão executados.  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir revoga o acesso para o logon `terrid` para acessar o proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grant_login_to_proxy](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_proxy](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
