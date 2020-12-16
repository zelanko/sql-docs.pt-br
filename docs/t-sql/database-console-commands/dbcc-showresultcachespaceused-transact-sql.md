---
description: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 08aabeafd830a6f037814e53903d0afcafef4422
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480477"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Mostra o espaço de armazenamento usado no cache do conjunto de resultados de um banco de dados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] do Azure.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>Comentários

O comando `DBCC SHOWRESULTCACHESPACEUSED` não usa nenhum parâmetro e retorna o espaço usado pelo banco de dados no qual o comando é executado.

## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Coluna|Tipo de Dados|DESCRIÇÃO|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Espaço total usado para o banco de dados, em KB. Esse número será alterado conforme o conjunto de resultados armazenado em cache aumentar.|  
|data_space|BIGINT|Espaço usado para dados, em KB.|  
|index_space|BIGINT|Espaço usado para índices, em KB.|  
|unused_space|BIGINT|O espaço que faz parte do espaço reservado e não é usado, em KB.|  

## <a name="see-also"></a>Confira também

[Ajuste de desempenho com cache de conjunto de resultados](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../statements/alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](../statements/alter-database-transact-sql.md?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](../statements/set-result-set-caching-transact-sql.md)</br>
[DBCC DROPRESULTSETCACHE &#40;Transact-SQL&#41;](./dbcc-dropresultsetcache-transact-sql.md)