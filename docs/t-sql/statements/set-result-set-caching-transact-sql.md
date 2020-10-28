---
description: SET RESULT_SET_CACHING (Transact-SQL)
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 93dfd425619744107fcf1123862cd0df76cad5ce
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300806"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Controla o comportamento de cache do conjunto de resultados da sessão do cliente atual.  

Aplica-se ao [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe

```syntaxsql
SET RESULT_SET_CACHING { ON | OFF };
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>Comentários  

Execute este comando quando estiver conectado ao banco de dados do usuário para o qual você deseja definir a configuração result_set_caching.

**Ligado**   
Habilita o armazenamento em cache do conjunto de resultados da sessão do cliente atual.  O armazenamento em cache do conjunto de resultados não poderá ser ATIVADO para uma sessão se estiver DESATIVADO no nível do banco de dados.

**Desligado**   
Desabilita o armazenamento em cache do conjunto de resultados da sessão do cliente atual.

## <a name="examples"></a>Exemplos

Consulte a coluna result_cache_hit em [sys.dm_pdw_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) com o request_id de uma consulta para ver se essa consulta foi executada com um acerto ou erro do cache de resultados.

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>Permissões

Requer associação à função pública

## <a name="see-also"></a>Confira também

- [Ajuste de desempenho com cache de conjunto de resultados](/azure/sql-data-warehouse/performance-tuning-result-set-caching)
- [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](./alter-database-transact-sql-set-options.md?preserve-view=true&view=azure-sqldw-latest)
- [ALTER DATABASE &#40;Transact-SQL&#41;](./alter-database-transact-sql.md?preserve-view=true&view=azure-sqldw-latest)
- [DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](../database-console-commands/dbcc-showresultcachespaceused-transact-sql.md)
- [DBCC DROPRESULTSETCACHE (Transact-SQL)](../database-console-commands/dbcc-dropresultsetcache-transact-sql.md)