---
title: sp_addrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1711ec3941a5fced5ef9e0c32808d6153b673e2b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68030926"
---
# <a name="sp_addrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma nova função de banco de dados no banco de dados atual.  
  
> [!IMPORTANT]
>  o **sp_addrole** está incluído para compatibilidade com versões anteriores [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do e pode não ter suporte em uma versão futura. Em vez disso, use [CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É o nome da nova função de banco de dados. *role* é um **sysname**, sem padrão. a *função* deve ser um identificador válido (ID) e ainda não deve existir no banco de dados atual.  
  
`[ @ownername = ] 'owner'`É o proprietário da nova função de banco de dados. *Owner* é um **sysname**, com um padrão do usuário em execução atual. o *proprietário* deve ser um usuário de banco de dados ou uma função de banco de dados no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Os nomes de funções de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ter de 1 a 128 caracteres, incluindo letras, símbolos e números. Os nomes das funções de banco de dados não podem: conter um\\caractere de barra invertida (), ser nulo ou uma cadeia de caracteres vazia (**' '**).  
  
 Depois de adicionar uma função de banco de dados, use [sp_addrolemember &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) para adicionar entidades de segurança à função. Quando as instruções GRANT, DENY ou REVOKE são usadas para aplicar permissões na função de banco de dados, os membros da função de banco de dados herdam essas permissões como se elas fossem aplicadas diretamente em suas contas.  
  
> [!NOTE]  
>  Novas funções de servidor não podem ser criadas. As funções podem ser criadas somente no nível do banco de dados.  
  
 **sp_addrole** não pode ser usada dentro de uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE ROLE no banco de dados. Se estiver criando um esquema, requer CREATE SCHEMA no banco de dados. Se o *proprietário* for especificado como um usuário ou grupo, o exigirá representação nesse usuário ou grupo. Se o *proprietário* for especificado como uma função, exigirá a permissão ALTER nessa função ou em um membro dessa função. Se o proprietário for especificado como uma função de aplicativo, requer a permissão ALTER nessa função de aplicativo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona uma nova função chamada `Managers` ao banco de dados atual.  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
