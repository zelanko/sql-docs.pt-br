---
description: sp_catalogs (Transact-SQL)
title: sp_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_catalogs_TSQL
- sp_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_catalogs
ms.assetid: ebb29ee2-be65-4e09-9c53-e3c6d12633e1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2ff43c02d386f830b42c6cf45ff0261f771579a7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541936"
---
# <a name="sp_catalogs-transact-sql"></a>sp_catalogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna a lista de catálogos no servidor vinculado especificado. Isso é equivalente aos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_catalogs [ @server_name = ] 'linked_svr'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'linked_svr'` É o nome de um servidor vinculado. *linked_svr* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Catalog_name**|**nvarchar (** 128 **)**|Nome do catálogo.|  
|**Descrição**|**nvarchar (** 4000 **)**|Descrição do catálogo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de catálogo para o servidor vinculado `OLE DB ODBC Linked Server #3`.  
  
> [!NOTE]  
>  Para **sp_catalogs** fornecer informações úteis, o `OLE DB ODBC Linked Server #3` já deve existir.  
  
```  
USE master;  
GO  
EXEC sp_catalogs 'OLE DB ODBC Linked Server #3';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_columns_ex ](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_column_privileges ](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_foreignkeys ](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_indexes ](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_primarykeys ](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_tables_ex ](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_privileges ](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
