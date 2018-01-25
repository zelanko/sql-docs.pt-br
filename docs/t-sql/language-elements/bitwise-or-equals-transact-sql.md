---
title: "| = (Bit a bit ou atribuição) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '|='
- '|=_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- compound operators, |=
- assignment operators, |=
- augmented operators, |=
- '|= (bitwise OR equals)'
ms.assetid: bd746a4f-6498-4196-bf2e-b6f457a15d44
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51157a82824e9445860a8cf8d3b6d49de1781b6d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="-bitwise-or-assignment-transact-sql"></a>| = (Bit a bit ou atribuição) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma operação OR lógica bit a bit entre dois valores inteiros especificados, conforme convertidos em expressões binárias dentro de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e define um valor como o resultado da operação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression |= expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos dados de tipos da categoria numérica, exceto o **bit** tipo de dados.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações, consulte [&#124; &#40; OR bit a bit &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Composta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
