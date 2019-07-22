---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuL-Preview
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 59946e45bbb14fb68e2fc28bcc81c2cf2d534758
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930642"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Mostra o espaço de armazenamento usado no cache do conjunto de resultados de um banco de dados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] do Azure.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  

## <a name="remarks"></a>Remarks

O comando `DBCC SHOWRESULTCACHESPACEUSED` não usa nenhum parâmetro e retorna o espaço usado pelo banco de dados no qual o comando é executado.

O tamanho máximo do cache de conjunto de resultados é de 1 TB por banco de dados.  O SQL Data Warehouse do Azure automaticamente remove entradas no cache de conjunto de resultados:

- a cada 48 horas, se o conjunto de resultados não foi usado.
- Quando o cache do conjunto de resultados se aproxima do tamanho máximo.

Os usuários podem esvaziar manualmente o cache do conjunto de resultados de um banco de dados ao desativar o recurso de cache de conjunto de resultados ou usando o comando `DBCC DROPRESULTSETCACHE`.   Pausar um banco de dados não esvazia o cache de conjunto de resultados.  

## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.
  
## <a name="see-also"></a>Confira também

[Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)