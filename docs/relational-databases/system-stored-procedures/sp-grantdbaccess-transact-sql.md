---
title: sp_grantdbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 3b88badb8b1852617d9edd8acd31f2c19258cca7
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304869"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um usuário ao banco de dados atual.  
  
> [!IMPORTANT]  
>  em vez disso, [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] use [Create User](../../t-sql/statements/create-user-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login_ '` é o nome do grupo do Windows, logon do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon a ser mapeado para o novo usuário do banco de dados. Os nomes de grupos do Windows e logons do Windows devem ser qualificados com um nome de domínio do Windows no formato *domínio*\\*logon*; por exemplo, **LONDON\Joeb**. O logon ainda não pode ser mapeado para um usuário no banco de dados. o *logon* é um **sysname**, sem padrão.  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]`` é o nome do novo usuário de banco de dados. *name_in_db* é uma variável de saída com um tipo de dados **sysname**e um padrão de NULL. Se não for especificado, o *logon* será usado. Se especificado como uma variável de saída com um valor de NULL, **\@name_in_db** será definido como *logon*. *name_in_db* ainda não deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_grantdbaccess** chama Create User, que dá suporte a opções adicionais. Para obter informações sobre como criar usuários de banco de dados, consulte [Create User &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md). Para remover um usuário de banco de dados do, use [drop User](../../t-sql/statements/drop-user-transact-sql.md).  
  
 **sp_grantdbaccess** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** ou **db_accessadmin** função de banco de dados fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `CREATE USER` para adicionar um usuário de banco de dados para o logon do Windows `Edmonds\LolanSo` ao banco de dados atual. O novo usuário chama-se `Lolan`. Este é o método preferencial para criar um usuário de banco de dados.  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
