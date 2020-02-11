---
title: sp_enum_login_for_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: ee6b6a701d4ff81863973c4c8e098bd9ed49c967
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124677"
---
# <a name="sp_enum_login_for_proxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista associações entre entidades de segurança e proxies.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`O nome de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entidade de segurança, logon, função de servidor ou função de banco de dados **msdb** para listar proxies. O nome é **nvarchar (256)**, com um padrão de NULL.  
  
`[ @proxy_id = ] id`O número de identificação de proxy do proxy para o qual listar informações. O *proxy_id* é **int**, com um padrão de NULL. A *ID* ou a *proxy_name* pode ser especificada.  
  
`[ @proxy_name = ] 'proxy_name'`O nome do proxy para o qual listar informações. O *proxy_name* é **sysname**, com um padrão de NULL. A *ID* ou a *proxy_name* pode ser especificada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Número de identificação de proxy.|  
|**proxy_name**|**sysname**|O nome do proxy.|  
|**name**|**sysname**|Nome da entidade de segurança da associação.|  
|**flags**|**int**|Tipo da entidade de segurança.<br /><br /> **** =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon<br /><br /> **1** = função de sistema fixa<br /><br /> **2** = função de banco de dados no **msdb**|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Comentários  
 Quando nenhum parâmetro é fornecido, **sp_enum_login_for_proxy** lista informações sobre todos os logons na instância para cada proxy.  
  
 Quando um ID de proxy ou nome de proxy é fornecido, **sp_enum_login_for_proxy** lista logons que têm acesso ao proxy. Quando um nome de logon é fornecido, **sp_enum_login_for_proxy** lista os proxies aos quais o logon tem acesso.  
  
 Quando informações de proxy e um nome de logon são fornecidos, o conjunto de resultados retornará uma linha se o logon especificado tiver acesso ao proxy especificado.  
  
 Esse procedimento armazenado está localizado no **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-associations"></a>a. Listando todas as associações  
 O exemplo a seguir lista todas as permissões estabelecidas entre logons e proxies na instância atual.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. Listando proxies para um logon específico  
 O exemplo a seguir lista os proxies aos quais o `terrid` de logon tem acesso.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_help_proxy](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grant_login_to_proxy](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revoke_login_from_proxy](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
