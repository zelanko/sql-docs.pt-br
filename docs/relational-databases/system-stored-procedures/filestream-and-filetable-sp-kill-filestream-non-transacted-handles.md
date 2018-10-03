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
manager: craigg
ms.openlocfilehash: a4f0308f8d04ae3dfb8fbefc2c6e7c70991b3afb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615584"
---
# <a name="spkillfilestreamnontransactedhandles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha identificadores de arquivos não transacionais para dados de FileTable.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] ‘table_name’, [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 O nome da tabela na qual fechar identificadores não transacionais.  
  
 Você pode passar *table_name* sem *handle_id* para fechar todos os abertos identificadores não transacionais da filetable.  
  
 É possível passar NULL para o valor de *table_name* para fechar todos os abertos identificadores não transacionais para todas as FileTables no banco de dados atual. O valor padrão é NULL.  
  
 *handle_id*  
 A ID opcional do identificador individual a ser fechado. Você pode obter o *handle_id* da [DM filestream_non_transacted_handles &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) exibição de gerenciamento dinâmico. Cada ID é exclusiva em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar *handle_id*, em seguida, você também precisa fornecer um valor para *table_name*.  
  
 É possível passar NULL para o valor de *handle_id* para fechar todos os abertos identificadores não transacionais da filetable especificada por *table_name*. O valor padrão é NULL.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O *handle_id* exigido pelo **sp_kill_filestream_non_transacted_handles** não está relacionado ao session_id ou unidade de trabalho que é usado em outros **kill** comandos.  
  
 Para obter mais informações, consulte [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre identificadores de arquivos não transacionais abertos, consulte a exibição de gerenciamento dinâmico [DM filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Você deve ter **VIEW DATABASE STATE** permissão para obter identificadores de arquivos das **DM filestream_non_transacted_handles** exibição de gerenciamento dinâmico e executar **sp_kill_filestream_non_ transacted_handles**.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar **sp_kill_filestream_non_transacted_handles** para fechar identificadores de arquivos não transacionais para dados de FileTable.  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’, @handle_id = 0xFFFAAADD  
```  
  
 O exemplo a seguir mostra como usar um script para obter um *handle_id* e fechá-la.  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
 [FileStream e exibições de gerenciamento dinâmico de FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[FileStream e exibições do catálogo FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
