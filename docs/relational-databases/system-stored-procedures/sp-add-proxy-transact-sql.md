---
title: sp_add_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4aa4120db7b45cb0b3a7d7a10bb53931b8300d9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088484"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona o proxy especificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_name = ] 'proxy_name'` O nome do proxy a ser criado. O *proxy_name* é **sysname**, com um padrão NULL. Quando o *proxy_name* é nulo ou uma cadeia de caracteres vazia, o nome do proxy assume como padrão para o *user_name* fornecido.  
  
`[ @enabled = ] is_enabled` Especifica se o proxy está habilitado. O *is_enabled* sinalizador é **tinyint**, com um padrão de 1. Quando *is_enabled* é **0**, o proxy não está habilitado e não pode ser usado por uma etapa de trabalho.  
  
`[ @description = ] 'description'` Uma descrição do proxy. A descrição é **nvarchar(512)** , com um padrão NULL. A descrição permite documentar o proxy, mas não é usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente. Portanto, este argumento é opcional.  
  
`[ @credential_name = ] 'credential_name'` O nome da credencial para o proxy. O *credential_name* é **sysname**, com um padrão NULL. Qualquer um dos *credential_name* ou *credential_id* deve ser especificado.  
  
`[ @credential_id = ] credential_id` O número de identificação da credencial para o proxy. O *credential_id* é **int**, com um padrão NULL. Qualquer um dos *credential_name* ou *credential_id* deve ser especificado.  
  
`[ @proxy_id = ] id OUTPUT` O número de identificação de proxy atribuído ao proxy se criado com êxito.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Esse procedimento armazenado deve ser executado **msdb** banco de dados.  
  
 Um proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent gerencia a segurança para etapas de trabalho que envolvem subsistemas diferentes do subsistema [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cada proxy corresponde a uma credencial de segurança. Um proxy pode ter acesso a qualquer número de subsistemas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** fixo de segurança podem executar este procedimento.  
  
 Os membros de **sysadmin** função de segurança fixa pode criar etapas de trabalho que usam qualquer proxy. Use o procedimento armazenado [sp_grant_login_to_proxy &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) conceder outro acesso de logon para o proxy.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo cria um proxy para a credencial `CatalogApplicationCredential`. O código supõe que a credencial já exista. Para obter mais informações sobre credenciais, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md).  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
