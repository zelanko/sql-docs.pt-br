---
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c52996b890529504c304aae2bf1dc41c3a3f4b4b
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947568"
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna dados de caractere convertidos de dados numéricos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 É uma expressão de tipo de dados numérico aproximado (**float**) com um separador decimal.  
  
 *length*  
 É o comprimento total. Isso inclui ponto decimal, sinal, dígitos e espaços. O padrão é 10.  
  
 *decimal*  
 É o número de dígitos à direita da vírgula decimal. *decimal* deve ser menor ou igual a 16. Se *decimal* for maior que 16, o resultado será truncado com dezesseis casas à direita do separador decimal.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 Se for fornecidos, os valores para os parâmetros *length* e *decimal* para STR devem ser positivos. O número é arredondado para um número inteiro por padrão ou se o parâmetro decimal for 0. O comprimento especificado deve ser maior ou igual à parte do número antes do ponto decimal mais o sinal do número (se houver). Uma *float_expression* breve é justificada à direita no comprimento especificado e uma *float_expression* longa é truncada para o número especificado de casas decimais. Por exemplo, STR(12 **,** 10) gera 12 como resultado. É justificado à direita no conjunto de resultados. Entretanto, STR (1223 **,** 2) trunca o conjunto de resultados com **. As funções de cadeia de caracteres podem ser aninhadas.  
  
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
  
  

