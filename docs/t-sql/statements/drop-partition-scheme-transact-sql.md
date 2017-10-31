---
title: "DESCARTAR o esquema de partição (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PARTITION SCHEME
- DROP_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP PARTITION SCHEME statement
- deleting partition schemes
- dropping partition schemes
- removing partition schemes
- partition schemes [SQL Server], removing
ms.assetid: 6efbc87c-1c92-4e43-96a7-e0f30f1db185
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1addeb0a836e7353e19f7676225799b58cee756c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-partition-scheme-transact-sql"></a>DROP PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um esquema de partição do banco de dados atual. Esquemas de partição são criados usando [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) e modificados usando [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP PARTITION SCHEME partition_scheme_name [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_scheme_name*  
 É o nome do esquema de partição a ser descartado.  
  
## <a name="remarks"></a>Comentários  
 Um esquema de partição poderá ser descartado apenas se não houver nenhuma tabela ou índice que use o esquema de partição atualmente. Se houver tabelas ou índices que usem o esquema de partição, DROP PARTITION SCHEME retornará um erro. DROP PARTITION SCHEME não remove os próprios grupos de arquivos.  
  
## <a name="permissions"></a>Permissões  
 As seguintes permissões podem ser usadas para executar DROP PARTITION SCHEME:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   Permissão CONTROL ou ALTER no banco de dados no qual o esquema de partição foi criado.  
  
-   Permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual o esquema de partição foi criado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o esquema de partição `myRangePS1` do banco de dados atual:  
  
```  
DROP PARTITION SCHEME myRangePS1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [sys. partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys. Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

