---
description: sp_addremotelogin (Transact-SQL)
title: sp_addremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
ms.openlocfilehash: de4f54972fb4a749e6466a81fef88ae8630be698
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464608"
---
# <a name="sp_addremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adiciona uma nova ID de logon remoto no servidor local. Isso permite que os servidores remotos se conectem e executem chamadas de procedimento remoto.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Use procedimentos armazenados de servidor vinculado e servidores vinculados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @remoteserver **=** ] **'**_servidor_remoto_**'**  
 É o nome do servidor remoto ao qual o logon remoto se aplica. o *servidor_remoto* é **sysname**, sem padrão. Se apenas o *servidor_remoto* for especificado, todos os usuários no *servidor_remoto* serão mapeados para os logons existentes de mesmo nome no servidor local. O servidor deve ser conhecido do servidor local. Ele é adicionado usando sp_addserver. Quando os usuários no *servidor_remoto* se conectam ao servidor local que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um procedimento armazenado remoto, eles se conectam como o logon local que corresponde ao seu próprio logon no *servidor_remoto*. *servidor_remoto* é o servidor que inicia a chamada de procedimento remoto.  
  
 [ @loginame **=** ] **'**_logon_**'**  
 É a ID do logon do usuário na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* é **sysname**, com um padrão de NULL. o *logon*já deve existir na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se o *logon* for especificado, todos os usuários no *servidor_remoto* serão mapeados para esse logon local específico. Quando os usuários no *servidor_remoto* se conectam à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um procedimento armazenado remoto, eles se conectam como *logon*.  
  
 [ @remotename **=** ] **'**_remote_name_**'**  
 É a ID do logon do usuário no servidor remoto. *remote_name* é **sysname**, com um padrão de NULL. *remote_name* deve existir no *servidor_remoto*. Se *remote_name* for especificado, o usuário específico *remote_name* será mapeado para *fazer logon* no servidor local. Quando *remote_name* no *servidor_remoto* se conecta à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um procedimento armazenado remoto, ele se conecta como *logon*. A ID de logon de *remote_name* pode ser diferente da ID de logon no servidor remoto, *logon*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Para executar consultas distribuídas, use sp_addlinkedsrvlogin.  
  
 sp_addremotelogin não pode ser usado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Somente membros das funções de servidor fixas sysadmin e securityadmin podem executar sp_addremotelogin.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-mapping-one-to-one"></a>a. Mapeando um para um  
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
  
## <a name="see-also"></a>Consulte Também  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addserver ](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropremotelogin ](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin ](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpremotelogin ](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_remoteoption ](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokelogin ](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
