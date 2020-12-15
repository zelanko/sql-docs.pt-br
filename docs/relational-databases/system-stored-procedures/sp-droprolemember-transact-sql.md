---
description: sp_droprolemember (Transact-SQL)
title: sp_droprolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
ms.author: vanto
author: VanMSFT
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 013cd061a96bd4f199591fa65f15718d27056d89
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440557"
---
# <a name="sp_droprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Remove uma conta de segurança de uma função do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [ALTER role](../../t-sql/statements/alter-role-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>Sintaxe para o SQL Server e o banco de dados SQL do Azure

```syntaxsql  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-synapse-analytics-and-parallel-data-warehouse"></a>Sintaxe para a análise de Synapse do Azure e Parallel data warehouse

```syntaxsql  
sp_droprolemember 'role' ,  
     'security_account'  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>Arguments  
`[ @rolename = ] 'role'` É o nome da função da qual o membro está sendo removido. *role* é **sysname**, sem padrão. a *função* deve existir no banco de dados atual.  
  
`[ @membername = ] 'security_account'` É o nome da conta de segurança que está sendo removida da função. *security_account* é **sysname**, sem padrão. *security_account* pode ser um usuário de banco de dados, outra função de banco de dados, um logon do Windows ou um grupo do Windows. *security_account* deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_droprolemember remove um membro de uma função de banco de dados excluindo uma linha da tabela sysmembers. Quando um membro é removido de uma função, ele perde qualquer permissão que tenha através da associação nessa função.  
  
 Para remover um usuário de uma função de servidor fixa, use sp_dropsrvrolemember. Os usuários não podem ser removidos da função pública, e dbonão pode ser removido de qualquer função.  
  
 Use sp_helpuser para ver os membros de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função e use ALTER role para adicionar um membro a uma função.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER na função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o usuário `JonB` da função `Sales`.  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir remove o usuário `JonB` da função `Sales`.  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsrvrolemember ](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpuser ](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

