---
title: sp_addremotelogin (Transact-SQL) | Microsoft Docs
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
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7be04649abd0a9bfdfb502074fa2f80d3209b92c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023234"
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma nova ID de logon remoto no servidor local. Isso permite que os servidores remotos se conectem e executem chamadas de procedimento remoto.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Use procedimentos armazenados de servidor vinculado e servidores vinculados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 É o nome do servidor remoto ao qual o logon remoto se aplica. *remoteserver* está **sysname**, sem padrão. Se apenas *remoteserver* for especificado, todos os usuários no *remoteserver* são mapeados para logons existentes de mesmo nome no servidor local. O servidor deve ser conhecido do servidor local. Isso é adicionado usando sp_addserver. Quando os usuários na *remoteserver* conecte-se ao servidor local que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um procedimento armazenado remoto, eles se conectam com o logon local que corresponde ao seu próprio logon no *remoteserver* . *remoteserver* é o servidor que inicia a chamada de procedimento remoto.  
  
 [ @loginame **=** ] **'***logon***'**  
 É a ID do logon do usuário na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* é **sysname**, com um padrão de NULL. *login*já deve existir na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se *login* for especificado, todos os usuários no *remoteserver* são mapeados para esse logon local específico. Quando os usuários na *remoteserver* conecte-se à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um procedimento armazenado remoto, eles se conectam com *logon*.  
  
 [ @remotename **=** ] **'***remote_name***'**  
 É a ID do logon do usuário no servidor remoto. *remote_name* está **sysname**, com um padrão NULL. *remote_name* deve existir no *remoteserver*. Se *remote_name* for especificado, o usuário específico *remote_name* é mapeado para *logon* no servidor local. Quando *remote_name* nos *remoteserver* conecta-se à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um procedimento armazenado remoto, ele se conecta como *logon*. A ID de logon do *remote_name* pode ser diferente da ID de logon no servidor remoto, *login*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Para executar consultas distribuídas, use sp_addlinkedsrvlogin.  
  
 sp_addremotelogin não pode ser usado dentro de uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros do sysadmin e securityadmin fixo de funções de servidor podem executar sp_addremotelogin.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-mapping-one-to-one"></a>A. Mapeando um para um  
 O exemplo a seguir mapeia nomes remotos para nomes locais quando o servidor remoto `ACCOUNTS` e o servidor local usam os mesmos logons de usuário.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>B. Mapeando muitos para um  
 O exemplo a seguir cria uma entrada que mapeia todos os usuários do servidor remoto `ACCOUNTS` para a ID de logon local `Albert`.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. Usando um mapeamento um para um explícito  
 O exemplo a seguir mapeia um logon remoto de um usuário remoto `Chris` no servidor remoto `ACCOUNTS` para o usuário local `salesmgr`.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
