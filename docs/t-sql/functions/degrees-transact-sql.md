---
title: GRAUS (Transact-SQL) | Microsoft Docs
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
- DEGREES
- DEGREES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DEGREES function
- number of degrees
ms.assetid: 5208de3c-90a3-4f59-a7e3-10b01bf285bb
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: b9c361e304bac38b51b31c65c029d5719aa8f006
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="degrees-transact-sql"></a>DEGREES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o ângulo correspondente em graus para um ângulo especificado em radiano.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DEGREES ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de exato dados numéricos aproximados ou categoria de tipo, exceto para o **bit** tipo de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Retorna o mesmo tipo que *numeric_expression*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o número de graus em um ângulo de radiano PI/2.  
  
```  
SELECT 'The number of degrees in PI/2 radians is: ' +   
CONVERT(varchar, DEGREES((PI()/2)));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The number of degrees in PI/2 radians is 90         
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


