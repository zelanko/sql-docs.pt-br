---
title: ACOS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ACOS
- ACOS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- ACOS function
- arccosine
ms.assetid: 4ec6b46e-9438-4f0f-8b96-461edd84280a
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 165cd76209927d223e90be73bad6fd0b383e5404
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33049353"
---
# <a name="acos-transact-sql"></a>ACOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma função que retorna o ângulo, em radianos, cujo cosseno é a expressão float especificada. Isso também é chamado de arco cosseno.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ACOS ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em float. Somente um valor que varia de -1,00 a 1,00 é válido. Valores fora deste intervalo retornarão NULL e ASIN relatará um erro de domínio.
  
## <a name="return-types"></a>Tipos de retorno  
**float**
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna o valor `ACOS` do número especificado.
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funções](../../t-sql/functions/functions.md)
  
  

