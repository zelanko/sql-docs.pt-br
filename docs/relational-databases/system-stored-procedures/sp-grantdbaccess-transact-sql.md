---
title: sp_grantdbaccess (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e8e67cc8f4672a650f7909fc71a759c3a856fcf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spgrantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um usuário ao banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***login* **'**  
 É o nome do grupo do Windows, logon do Windows ou logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser mapeado para o novo usuário do banco de dados. Nomes de grupos do Windows e logons do Windows devem ser qualificados com um nome de domínio do Windows no formato *domínio*\\*login*; por exemplo, **LONDON\Joeb**. O logon ainda não pode ser mapeado para um usuário no banco de dados. *logon* é um **sysname**, sem padrão.  
  
 [  **@name_in_db=**] **'***name_in_db***'** [ **saída**]  
 É o nome do novo usuário de banco de dados. *name_in_db* é uma variável de saída com um tipo de dados **sysname**e um padrão NULL. Se não for especificado, *login* é usado. Se for especificado como uma variável de saída com um valor nulo,  **@name_in_db**  é definido como *logon*. *name_in_db* ainda não deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_grantdbaccess** chama CREATE USER, que oferece suporte a opções adicionais. Para obter informações sobre como criar usuários de banco de dados, consulte [CREATE USER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-user-transact-sql.md). Para remover um usuário de banco de dados de um banco de dados, use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md).  
  
 **sp_grantdbaccess** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **db_owner** função de banco de dados fixa ou **db_accessadmin** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `CREATE USER` para adicionar um usuário de banco de dados para o logon do Windows `Edmonds\LolanSo` ao banco de dados atual. O novo usuário chama-se `Lolan`. Este é o método preferencial para criar um usuário de banco de dados.  
  
```  
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Remover usuário &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
