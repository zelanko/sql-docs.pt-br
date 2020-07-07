---
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8be7e84ccd80d80c1345adec3450e5bc8e0f4da6
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012702"
---
# <a name="sp_droprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Remove uma conta de segurança de uma função do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [ALTER role](../../t-sql/statements/alter-role-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>Sintaxe para o SQL Server e o banco de dados SQL do Azure

```  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Sintaxe para o Azure SQL Data Warehouse e Parallel data warehouse

```  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É o nome da função da qual o membro está sendo removido. *role* é **sysname**, sem padrão. a *função* deve existir no banco de dados atual.  
  
`[ @membername = ] 'security_account'`É o nome da conta de segurança que está sendo removida da função. *security_account* é **sysname**, sem padrão. *security_account* pode ser um usuário de banco de dados, outra função de banco de dados, um logon do Windows ou um grupo do Windows. *security_account* deve existir no banco de dados atual.  
  
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
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droprole](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsrvrolemember](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpuser](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

