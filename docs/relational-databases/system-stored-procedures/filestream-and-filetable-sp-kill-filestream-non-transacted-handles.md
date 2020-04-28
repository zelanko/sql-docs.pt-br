---
title: sp_kill_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
author: stevestein
ms.author: sstein
ms.openlocfilehash: 98c986c26c8d0d0cc6e2b8ff3573f0a20d938975
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942260"
---
# <a name="sp_kill_filestream_non_transacted_handles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha identificadores de arquivos não transacionais para dados de FileTable.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] 'table_name', [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 O nome da tabela na qual fechar identificadores não transacionais.  
  
 Você pode passar *table_name* sem *handle_id* para fechar todos os identificadores não transacionais abertos para a filetable.  
  
 Você pode passar NULL para o valor de *table_name* para fechar todos os identificadores não transacionais abertos para todas as filetables no banco de dados atual. O valor padrão é NULL.  
  
 *handle_id*  
 A ID opcional do identificador individual a ser fechado. Você pode obter a *handle_id* da exibição de gerenciamento dinâmico do [Transact-SQL&#41;dm_filestream_non_transacted_handles &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) . Cada ID é exclusiva em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar *handle_id*, também precisará fornecer um valor para *table_name*.  
  
 Você pode passar NULL para o valor de *handle_id* fechar todos os identificadores não transacionais abertos para a filetable especificada por *table_name*. O valor padrão é NULL.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O *handle_id* exigido pelo **sp_kill_filestream_non_transacted_handles** não está relacionado à session_id ou unidade de trabalho usada em outros comandos **Kill** .  
  
 Para obter mais informações, consulte [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre como abrir identificadores de arquivos não transacionais, consulte a exibição de gerenciamento dinâmico [Sys. dm_filestream_non_transacted_handles &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Você deve ter a permissão **View Database State** para obter identificadores de arquivo da exibição de gerenciamento dinâmico **Sys. dm_FILESTREAM_non_transacted_handles** e para executar **sp_kill_filestream_non_transacted_handles**.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar **sp_kill_filestream_non_transacted_handles** para fechar identificadores de arquivos não transacionais para dados filetable.  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable'  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable', @handle_id = 0xFFFAAADD  
```  
  
 O exemplo a seguir mostra como usar um script para obter um *handle_id* e fechá-lo.  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
 [Exibições de gerenciamento dinâmico de FileStream e Filetable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[Exibições de catálogo FileStream e Filetable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
