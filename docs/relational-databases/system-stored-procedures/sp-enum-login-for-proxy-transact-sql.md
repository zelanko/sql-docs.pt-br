---
title: sp_enum_login_for_proxy (Transact-SQL) | Microsoft Docs
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
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3c4751f3d9dfaa60110f7e859bc8157de2c9246
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spenumloginforproxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista associações entre entidades de segurança e proxies.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@name**=] '*nome*'  
 O nome de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] principal, o logon, a função de servidor ou **msdb** função de banco de dados para listar proxies. O nome é **nvarchar (256)**, com um padrão NULL.  
  
 [ **@proxy_id**= ] *id*  
 O número de identificação de proxy do proxy para o qual listar informações. O *proxy_id* é **int**, com um padrão NULL. Ambos o *id* ou *proxy_name* pode ser especificado.  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 O nome do proxy para o qual listar informações. O *proxy_name* é **sysname**, com um padrão NULL. Ambos o *id* ou *proxy_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**Int**|Número de identificação de proxy.|  
|**proxy_name**|**sysname**|O nome do proxy.|  
|**name**|**sysname**|Nome da entidade de segurança da associação.|  
|**flags**|**Int**|Tipo da entidade de segurança.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon<br /><br /> **1** = função de sistema fixa<br /><br /> **2** = função de banco de dados em **msdb**|  
  
## <a name="remarks"></a>Remarks  
 Quando nenhum parâmetro for fornecido, **sp_enum_login_for_proxy** lista informações sobre todos os logons na instância para cada proxy.  
  
 Quando um id de proxy ou nome de proxy é fornecido, **sp_enum_login_for_proxy** lista logons que têm acesso ao proxy. Quando é fornecido um nome de logon, **sp_enum_login_for_proxy** lista os proxies que o logon tenha acessem.  
  
 Quando informações de proxy e um nome de logon são fornecidos, o conjunto de resultados retornará uma linha se o logon especificado tiver acesso ao proxy especificado.  
  
 Esse procedimento armazenado está localizado em **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-associations"></a>A. Listando todas as associações  
 O exemplo a seguir lista todas as permissões estabelecidas entre logons e proxies na instância atual.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. Listando proxies para um logon específico  
 O exemplo a seguir lista os proxies aos quais o `terrid` de logon tem acesso.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_help_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
