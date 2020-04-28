---
title: sp_delete_backuphistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_backuphistory
- sp_delete_backuphistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_backuphistory
ms.assetid: bdb56834-616e-47e4-b942-e895d2325e97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c538a217c5d86f2b59f079f8629a6f4cbe9fea3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68120061"
---
# <a name="sp_delete_backuphistory-transact-sql"></a>sp_delete_backuphistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reduz o tamanho das tabelas de histórico de backup e restauração excluindo as entradas de conjuntos de backup anteriores à data especificada. Linhas adicionais são adicionadas às tabelas de histórico de backup e restauração depois que cada operação de backup ou restauração é executada; Portanto, recomendamos que você execute periodicamente **sp_delete_backuphistory**.  
  
> [!NOTE]  
>  As tabelas de histórico de backup e restauração residem no banco de dados **msdb** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_backuphistory [ @oldest_date = ] 'oldest_date'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @oldest_date = ] 'oldest\_date'`É a data mais antiga retida nas tabelas de histórico de backup e restauração. *oldest_date* é **DateTime**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_backuphistory** deve ser executado no banco de dados **msdb** e afeta as seguintes tabelas:  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
  
-   [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
  
-   [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
  
 Os arquivos de backup físicos são preservados, até mesmo se todo o histórico for excluído.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** , mas as permissões podem ser concedidas a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui todas as entradas que são mais antigas do que 14 de janeiro de 2010, 00h00 nas tabela de histórico de backup e restauração.  
  
```  
USE msdb;  
GO  
EXEC sp_delete_backuphistory @oldest_date = '01/14/2010';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_delete_database_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
