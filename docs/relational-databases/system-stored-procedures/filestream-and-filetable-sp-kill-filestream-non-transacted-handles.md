---
title: sp_kill_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs: TSQL
helpviewer_keywords: sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7958e7a6513363030d8962774a28992bd055661d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="filestream-and-filetable---spkillfilestreamnontransactedhandles"></a>FileStream e FileTable - sp_kill_filestream_non_transacted_handles
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha identificadores de arquivos não transacionais para dados de FileTable.  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] ‘table_name’, [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 O nome da tabela na qual fechar identificadores não transacionais.  
  
 Você pode passar *table_name* sem *handle_id* para fechar todos os abertos identificadores não transacionais da filetable.  
  
 É possível passar NULL para o valor de *table_name* para fechar todos os não-transacional identificadores abertos para todas as FileTables no banco de dados atual. O valor padrão é NULL.  
  
 *handle_id*  
 A ID opcional do identificador individual a ser fechado. Você pode obter o *handle_id* do [sys.DM filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) exibição de gerenciamento dinâmico. Cada ID é exclusiva em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar *handle_id*, em seguida, você também precisa fornecer um valor para *table_name*.  
  
 É possível passar NULL para o valor de *handle_id* para fechar todos os abertos identificadores não transacionais da filetable especificada por *table_name*. O valor padrão é NULL.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O *handle_id* exigido pelo **sp_kill_filestream_non_transacted_handles** não está relacionado ao session_id ou unidade de trabalho que é usada em outros **kill** comandos.  
  
 Para obter mais informações, consulte [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre identificadores de arquivos não transacionais abertos, consulte a exibição de gerenciamento dinâmico [sys.DM filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Você deve ter **VIEW DATABASE STATE** permissão para obter os identificadores de arquivos do **sys.DM filestream_non_transacted_handles** exibição de gerenciamento dinâmico e executar **sp_kill_filestream_non_ transacted_handles**.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como chamar **sp_kill_filestream_non_transacted_handles** para fechar identificadores de arquivos não transacionais para dados de FileTable.  
  
```tsql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’, @handle_id = 0xFFFAAADD  
```  
  
 O exemplo a seguir mostra como usar um script para obter um *handle_id* e fechá-la.  
  
```tsql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
