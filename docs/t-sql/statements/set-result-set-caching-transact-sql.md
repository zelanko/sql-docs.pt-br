---
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: a9f050fd8e95a7dba255cf7aa164f1d58179182e
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67564116"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Controla o comportamento de cache do conjunto de resultados da sessão do cliente atual.  

Aplica-se a ao SQL Data Warehouse do Azure (versão prévia)
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

**Ligado**   
Habilita o armazenamento em cache do conjunto de resultados da sessão do cliente atual.  O armazenamento em cache do conjunto de resultados não poderá ser ATIVADO para uma sessão se estiver DESATIVADO no nível do banco de dados.

**Desligado**   
Desabilita o armazenamento em cache do conjunto de resultados da sessão do cliente atual.

## <a name="examples"></a>Exemplos

Consulte a coluna result_cache_hit em [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql) com o request_id de uma consulta para ver se essa consulta foi executada com um acerto ou erro do cache de resultados.

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>Permissões

Requer associação à função pública

## <a name="see-also"></a>Confira também

[Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)</br>
[DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)