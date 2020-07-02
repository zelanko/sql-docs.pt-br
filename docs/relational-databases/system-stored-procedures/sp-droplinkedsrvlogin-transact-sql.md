---
title: sp_droplinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a06023c8747c4226f7387b0f68bba13220707b99
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786894"
---
# <a name="sp_droplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove um mapeamento existente entre um logon no servidor local que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um logon no servidor vinculado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rmtsrvname = ] 'rmtsrvname'`É o nome de um servidor vinculado ao qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeamento de logon se aplica. *rmtsrvname* é **sysname**, sem padrão. *rmtsrvname* já deve existir.  
  
`[ @locallogin = ] 'locallogin'`É o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon no servidor local que tem um mapeamento para o servidor vinculado *rmtsrvname*. *locallogin* é **sysname**, sem padrão. Um mapeamento para *locallogin* para *rmtsrvname* já deve existir. Se NULL, o mapeamento padrão criado por **sp_addlinkedserver**, que mapeia todos os logons no servidor local para logons no servidor vinculado, é excluído.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando o mapeamento existente para um logon é excluído, o servidor local usa o mapeamento padrão criado pelo **sp_addlinkedserver** quando ele se conecta ao servidor vinculado em nome desse logon. Para alterar o mapeamento padrão, use **sp_addlinkedsrvlogin**.  
  
 Se o mapeamento padrão também for excluído, somente os logons que receberam explicitamente um mapeamento de logon para o servidor vinculado, usando **sp_addlinkedsrvlogin**, poderão acessar o servidor vinculado.  
  
 **sp_droplinkedsrvlogin** não pode ser executado de dentro de uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>a. Removendo o mapeamento de logon para um usuário existente  
 O exemplo a seguir remove o mapeamento para o logon `Mary` do servidor local para o servidor vinculado `Accounts`. Portanto, o logon `Mary` usa o mapeamento de logon padrão.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. Removendo o mapeamento de logon padrão  
 O exemplo a seguir remove o mapeamento de logon padrão originalmente criado executando `sp_addlinkedserver` no servidor vinculado `Accounts`.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
