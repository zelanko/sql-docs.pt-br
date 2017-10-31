---
title: SQRT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQRT
- SQRT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SQRT function
- square root values
ms.assetid: 26e244e8-e82d-4664-a445-1226230ee1c5
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5287fca25554a29211a48ab9584bc893b097686a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sqrt-transact-sql"></a>SQRT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a raiz quadrada do valor flutuante especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQRT ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em float.  
  
## <a name="return-types"></a>Tipos de retorno  
 **float**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a raiz quadrada de números entre `1.00` e `10.00`.  
  
```  
DECLARE @myvalue float;  
SET @myvalue = 1.00;  
WHILE @myvalue < 10.00  
   BEGIN  
      SELECT SQRT(@myvalue);  
      SET @myvalue = @myvalue + 1  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------------------   
1.0                        
------------------------   
1.4142135623731            
------------------------   
1.73205080756888           
------------------------   
2.0                        
------------------------   
2.23606797749979           
------------------------   
2.44948974278318           
------------------------   
2.64575131106459           
------------------------   
2.82842712474619           
------------------------   
3.0  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna a raiz quadrada de números `1.00` e `10.00`.  
  
```  
SELECT SQRT(1.00), SQRT(10.00);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
----------  ------------  
1.00        3.16
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


