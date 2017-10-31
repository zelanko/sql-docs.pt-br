---
title: CEILING (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CEILING_TSQL
- CEILING
dev_langs:
- TSQL
helpviewer_keywords:
- smallest integer great than or equal to expression
- integers [SQL Server]
- CEILING function [Transact-SQL]
ms.assetid: e736b43a-9457-4781-95a4-4bcf9d4fc46a
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 5eeb03620e210cebec1afece563c5e10b8101361
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="ceiling-transact-sql"></a>CEILING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o menor inteiro maior que ou igual a expressão numérica especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CEILING ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*numeric_expression*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de exato dados numéricos aproximados ou categoria de tipo, exceto para o **bit** tipo de dados.
  
## <a name="return-types"></a>Tipos de retorno
Retorna o mesmo tipo que *numeric_expression*.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra valores numéricos positivos, numéricos negativos e valores zero com a função CEILING.
  
```sql
SELECT CEILING($123.45), CEILING($-123.45), CEILING($0.0);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
--------- --------- -------------------------   
124.00    -123.00    0.00                       
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  

