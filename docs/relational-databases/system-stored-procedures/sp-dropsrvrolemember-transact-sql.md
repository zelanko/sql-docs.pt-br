---
title: sp_dropsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ff304ce765010d2097c76574b0186df43d8b9104
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33242408"
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um usuário ou grupo do Windows de uma função de servidor fixa.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame **=** ] **'***login***'**  
 É o nome de um logon a ser removido da função de servidor fixa. *logon* é **sysname**, sem padrão. *logon* deve existir.  
  
 [ @rolename **=** ] **'***função***'**  
 É o nome de uma função de servidor. *função* é **sysname**, com um padrão NULL. *função* deve ser um dos seguintes valores:  
  
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
  
## <a name="remarks"></a>Remarks  
 Sp_dropsrvrolemember só pode ser usado para remover um logon de uma função de servidor fixa. Use sp_droprolemember para remover um membro de uma função de banco de dados.  
  
 O logon de sa não pode ser removido de qualquer função de servidor fixa.  
  
 sp_dropsrvrolemember não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação sysadmin fixa a função de servidor, ou a permissão ALTER ANY LOGIN no servidor e a associação na função da qual o membro está sendo descartado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o logon `JackO` da função de servidor fixa `sysadmin`.  
  
```  
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
