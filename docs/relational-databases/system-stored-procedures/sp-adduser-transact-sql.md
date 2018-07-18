---
title: sp_adduser (Transact-SQL) | Microsoft Docs
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
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4f7afe6646fd22ff24aa6aee4e5dcde416420e9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036094"
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo usuário ao banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [criar usuário](../../t-sql/statements/create-user-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***logon***'**  
 É o nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do logon do Windows. *login* é um **sysname**, sem padrão. *login* deve ser um existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou logon do Windows.  
  
 [  **@name_in_db =** ] **'***usuário***'**  
 É o nome do novo usuário de banco de dados. *usuário* é um **sysname**, com um padrão NULL. Se *usuário* não for especificado, o nome do novo usuário de banco de dados assumirá o *login* nome. Especificando *usuário* fornece um nome do novo usuário no banco de dados diferente do nome de logon de nível de servidor.  
  
 [  **@grpname =** ] **'***função***'**  
 É a função de banco de dados da qual o novo usuário se torna um membro. *função* está **sysname**, com um padrão NULL. *função* deve ser uma função de banco de dados válido no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_adduser** também criará um esquema que tem o nome do usuário.  
  
 Depois que um usuário for adicionado, use as instruções GRANT, DENY e REVOKE para definir as permissões que controlam as atividades executadas pelo usuário.  
  
 Use **sys. server_principals** para exibir uma lista de nomes de logon válido.  
  
 Use **sp_helprole** para exibir uma lista dos nomes de função válido. Quando você especifica uma função, o usuário automaticamente ganha as permissões definidas para ela. Se uma função não for especificada, o usuário ganhará as permissões concedidas para o padrão **pública** função. Para adicionar um usuário a uma função, um valor para o *nome de usuário* deve ser fornecido. (*nome de usuário* pode ser o mesmo que *login_id*.)  
  
 Usuário **convidado** já existe em cada banco de dados. Adicionando usuário **convidado** habilitará esse usuário, se ele foi previamente desabilitado. Por padrão, usuário **convidado** está desabilitado em novos bancos de dados.  
  
 **sp_adduser** não pode ser executado dentro de uma transação definida pelo usuário.  
  
 Não é possível adicionar um **convidado** usuário porque um **convidado** já existe um usuário dentro de cada banco de dados. Para habilitar o **convidado** usuário, conceder **convidado** permissão CONNECT conforme mostrado:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Permissões  
 Requer propriedade do banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-database-user"></a>A. Adicionando um usuário de banco de dados  
 O exemplo a seguir adicionar o usuário de banco de dados `Vidur` à função existente `Recruiting` no banco de dados atual, usando o logon existente `Vidur` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. Adicionando um usuário de banco de dados com a mesma ID de logon  
 O exemplo a seguir adiciona o usuário `Arvind` ao banco de dados atual para o logon `Arvind` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse usuário pertence ao padrão **pública** função.  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. Adicionando um usuário de banco de dados com um nome diferente de seu logon em nível de servidor  
 O exemplo a seguir adiciona o logon `BjornR` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao banco de dados atual que possui um nome de usuário `Bjorn`, e adiciona o usuário de banco de dados `Bjorn` à função de banco de dados `Production`.  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
