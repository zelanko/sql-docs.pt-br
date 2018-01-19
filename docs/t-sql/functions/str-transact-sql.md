---
title: STR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs: TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 04386cd8dafb69d08c72b460f3794963c8b6da36
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna dados de caractere convertidos de dados numéricos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 É uma expressão de numérico aproximado (**float**) tipo de dados com um ponto decimal.  
  
 *comprimento*  
 É o comprimento total. Isso inclui ponto decimal, sinal, dígitos e espaços. O padrão é 10.  
  
 *decimal*  
 É o número de dígitos à direita da vírgula decimal. *decimal* deve ser menor ou igual a 16. Se *decimal* for maior que 16, o resultado será truncado com dezesseis casas à direita da vírgula decimal.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 Se for fornecido, os valores para *comprimento* e *decimal* parâmetros para STR devem ser positivos. O número é arredondado para um número inteiro por padrão ou se o parâmetro decimal for 0. O comprimento especificado deve ser maior ou igual à parte do número antes do ponto decimal mais o sinal do número (se houver). Uma breve *float_expression* é justificado à direita no comprimento especificado e um longo *float_expression* são truncados para o número especificado de casas decimais. Por exemplo, STR (12**,**10), o resultado de 12. É justificado à direita no conjunto de resultados. No entanto, STR (1223**,**2) trunca o conjunto de resultados para * *. As funções de cadeia de caracteres podem ser aninhadas.  
  
> [!NOTE]  
>  Para converter para dados Unicode, use STR dentro de uma CONVERSÃO ou [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) função de conversão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir converte uma expressão composta de cinco dígitos e um ponto decimal em uma cadeia de caracteres de seis posições. A parte fracionária do número é arredondada para uma casa decimal.  
  
```  
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 Quando a expressão excede o comprimento especificado, a cadeia de caracteres retorna `**` para o comprimento especificado.  
  
```  
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 Até mesmo quando dados numéricos são aninhados em `STR`, o resultado são dados de caractere com o formato especificado.  
  
```  
SELECT STR (FLOOR (123.45), 8, 3;)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

