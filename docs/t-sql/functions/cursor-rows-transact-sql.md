---
title: '@@CURSOR_ROWS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 481c4205bec9032b31b4405830827405050abb8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="x40x40cursorrows-transact-sql"></a>&#x40;&#x40;CURSOR_ROWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o número de linhas de qualificação atualmente no último cursor aberto na conexão. Para melhorar o desempenho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode popular cursores estáticos e conjuntos de chaves grandes assincronamente. @@CURSOR_ROWS pode ser chamado para determinar que o número das linhas que se qualificam para um cursor é recuperado no momento em que @@CURSOR_ROWS é chamado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>Tipos de retorno
**inteiro**
  
## <a name="return-value"></a>Valor retornado  
  
|Valor retornado|Description|  
|---|---|
|-*m*|A tabela de cursor é populada de forma assíncrona. O valor retornado (-*m*) é o número de linhas atualmente no conjunto de chaves.|  
|-1|O cursor é dinâmico. Como os cursores dinâmicos refletem todas as alterações, o número de linhas que se qualificam para o cursor são alterados constantemente. Nunca se pode afirmar de forma definitiva que todas as linhas qualificadas foram recuperadas.|  
|0|Nenhum cursor foi aberto, nenhuma linha se qualificou para o último cursor aberto ou o último cursor aberto foi fechado ou desalocado.|  
|*n*|A tabela está totalmente populada. O valor retornado (*n*) é o número total de linhas no cursor.|  
  
## <a name="remarks"></a>Remarks  
O número retornado por @@CURSOR_ROWS é negativo se o último cursor foi aberto de forma assíncrona. Os cursores controlados por conjunto de chaves ou estáticos são abertos de forma assíncrona se o valor do limite do cursor sp_configure é maior que 0 e o número de linhas no conjunto de resultados do cursor é maior que o limite do cursor.
  
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
  
## <a name="see-also"></a>Confira também
[Funções do cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  
