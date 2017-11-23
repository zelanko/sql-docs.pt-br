---
title: '@@CURSOR_ROWS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8c4c1fac4c5d9dacddfb942a3e5b9238e5be16a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40cursorrows-transact-sql"></a>& #x 40; & #x 40. CURSOR_ROWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o número de linhas de qualificação atualmente no último cursor aberto na conexão. Para melhorar o desempenho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode popular cursores estáticos e conjuntos de chaves grandes assincronamente. @@CURSOR_ROWS pode ser chamado para determinar que o número de linhas que se qualificam para um cursor é recuperado no momento @@CURSOR_ROWS é chamado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="return-value"></a>Valor de retorno  
  
|Valor de retorno|Description|  
|---|---|
|-*m*|A tabela de cursor é populada de forma assíncrona. O valor retornado (-*m*) é o número de linhas atualmente no conjunto de chaves.|  
|-1|O cursor é dinâmico. Como os cursores dinâmicos refletem todas as alterações, o número de linhas que se qualificam para o cursor são alterados constantemente. Nunca se pode afirmar de forma definitiva que todas as linhas qualificadas foram recuperadas.|  
|0|Nenhum cursor foi aberto, nenhuma linha se qualificou para o último cursor aberto ou o último cursor aberto foi fechado ou desalocado.|  
|*n*|A tabela está totalmente populada. O valor retornado (*n*) é o número total de linhas no cursor.|  
  
## <a name="remarks"></a>Comentários  
O número retornado por@CURSOR_ROWS é negativo se o último cursor tiver sido aberto assincronamente. Driver de conjunto de chaves ou Cursores estáticos serão abertos assincronamente se o valor de limite do cursor sp_configure for maior que 0 e o número de linhas no conjunto de resultados de cursor for maior que o limite do cursor.
  
## <a name="examples"></a>Exemplos  
O exemplo seguinte declara um cursor e usa `SELECT` para exibir o valor de `@@CURSOR_ROWS`. A configuração tem um valor de `0` antes de o cursor ser aberto e um valor de `-1` para indicar que o conjunto de chaves do cursor é populado assincronamente.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@CURSOR_ROWS;  
DECLARE Name_Cursor CURSOR FOR  
SELECT LastName ,@@CURSOR_ROWS FROM Person.Person;  
OPEN Name_Cursor;  
FETCH NEXT FROM Name_Cursor;  
SELECT @@CURSOR_ROWS;  
CLOSE Name_Cursor;  
DEALLOCATE Name_Cursor;  
GO             
```  
  
Estes são os conjuntos de resultados.
  
```
-----------
0  
```

```
LastName
---------------
Sanchez
```

```
-----------
-1
```  
  
## <a name="see-also"></a>Consulte também
[Funções de cursor &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[Abrir &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  
