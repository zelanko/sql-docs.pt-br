---
title: sp_dropsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 213b8301a471e00107ce7d3ac6bf493e6aea87c4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85662470"
---
# <a name="sp_dropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-SQL)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Remove um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um usuário ou grupo do Windows de uma função de servidor fixa.

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [ALTER Server Role](../../t-sql/statements/alter-server-role-transact-sql.md) .

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## <a name="arguments"></a>Argumentos

**[ @loginame =]** '_logon_'  
É o nome de um logon a ser removido da função de servidor fixa. o *logon* é **sysname**, sem padrão. o *logon* deve existir.  

**[ @rolename =]** '_função_'  
É o nome de uma função de servidor. *role* é **sysname**, com um padrão de NULL. a *função* deve ser um dos seguintes valores:  

-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin 
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Somente sp_dropsrvrolemember pode ser usado para remover um logon de uma função de servidor fixa. Use sp_droprolemember para remover um membro de uma função de banco de dados.  
  
 O logon sa não pode ser removido de qualquer função de servidor fixa.  
  
 sp_dropsrvrolemember não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou a permissão ALTER ANY LOGIN no servidor e a associação na função da qual o membro está sendo descartado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o logon `JackO` da função de servidor fixa `sysadmin`.  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR função de servidor &#40;&#41;Transact-SQL](../../t-sql/statements/create-server-role-transact-sql.md)   
 [Descartar função de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droprolemember](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
