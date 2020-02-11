---
title: sp_renamedb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_renamedb
- sp_renamedb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_renamedb
ms.assetid: 7dd9d4ff-20e1-4857-9a8e-a5bff767cf76
author: stevestein
ms.author: sstein
ms.openlocfilehash: eebf9be216d61163c018e0d43075e636cb383d28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006930"
---
# <a name="sp_renamedb-transact-sql"></a>sp_renamedb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Altera o nome de um banco de dados  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use ALTER DATABASE MODIFY NAME. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_renamedb [ @dbname = ] 'old_name' , [ @newname = ] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'old_name'`É o nome atual do banco de dados. *old_name* é **sysname**, sem padrão.  
  
`[ @newname = ] 'new_name'`É o novo nome do banco de dados. *new_name* deve seguir as regras para identificadores. *new_name* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação nas funções de servidor fixas **sysadmin** ou **dbcreator** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria o banco de dados `Accounting` e altera o seu nome para `Financial`. Em seguida, a exibição de catálogo `sys.databases` será consultada para verificar o novo nome do banco de dados.  
  
```  
USE master;  
GO  
CREATE DATABASE Accounting;  
GO  
EXEC sp_renamedb N'Accounting', N'Financial';  
GO  
SELECT name, database_id, modified_date  
FROM sys.databases  
WHERE name = N'Financial';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdb](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
