---
description: STR (Transact-SQL)
title: STR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 365ef62b6b5437956e6dd2753b3f83de300d32b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467788"
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna dados de caractere convertidos de dados numéricos. Os dados de caractere são justificados à direita, com comprimento e precisão decimal especificados. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *float_expression*  
 É uma expressão de tipo de dados numérico aproximado (**float**) com um separador decimal.  
  
 *length*  
 É o comprimento total. Isso inclui ponto decimal, sinal, dígitos e espaços. O padrão é 10.  
  
 *decimal*  
 É o número de dígitos à direita da vírgula decimal. *decimal* deve ser menor ou igual a 16. Se *decimal* for maior que 16, o resultado será truncado com dezesseis casas à direita do separador decimal.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varchar**  
  
## <a name="remarks"></a>Comentários  
 Se for fornecidos, os valores para os parâmetros *length* e *decimal* para STR devem ser positivos. O número é arredondado para um número inteiro por padrão ou se o parâmetro decimal for 0. O comprimento especificado deve ser maior ou igual à parte do número antes do ponto decimal mais o sinal do número (se houver). Uma *float_expression* breve é justificada à direita no comprimento especificado e uma *float_expression* longa é truncada para o número especificado de casas decimais. Por exemplo, STR(12, 10) gera 12 como resultado. É justificado à direita no conjunto de resultados. Entretanto, STR (1223, 2) trunca o conjunto de resultados com \*\*. As funções de cadeia de caracteres podem ser aninhadas.  
  
> [!NOTE]  
>  Para converter para dados Unicode, use STR dentro de uma função de conversão CONVERT ou [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
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
SELECT STR (FLOOR (123.45), 8, 3);
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

