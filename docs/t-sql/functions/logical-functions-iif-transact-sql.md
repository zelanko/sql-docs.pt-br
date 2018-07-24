---
title: IIF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IIF_TSQL
- IIF
dev_langs:
- TSQL
helpviewer_keywords:
- IIF function
ms.assetid: e3ccf8ed-1cec-43ac-90b7-d8597c24b050
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4234d8df62c024e68a83497c763253044011b5b8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38022780"
---
# <a name="logical-functions---iif-transact-sql"></a>Funções lógicas – IIF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna um de dois valores, dependendo de a expressão booliana ser avaliada como true ou false no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IIF ( boolean_expression, true_value, false_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Uma expressão Booliana válida.  
  
 Se esse argumento não for uma expressão Booliana, será gerado um erro de sintaxe.  
  
 *true_value*  
 Valor a ser retornado se *boolean_expression* for avaliada como verdadeira.  
  
 *false_value*  
 Valor a ser retornado se *boolean_expression* for avaliada como falsa.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o tipo de dados com a precedência mais alta dos tipos em *true_value* e *false_value*. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 IIF é uma forma abreviada de gravar uma expressão CASE. Avalia a expressão Booliana passada pelo primeiro argumento e retorna qualquer um dos outros dois argumentos com base no resultado da avaliação. Ou seja, o *true_value* será retornado se a expressão booliana for verdadeira e o *false_value* será retornado se a expressão booliana for falsa ou desconhecida. *true_value* e *false_value* podem ser de qualquer tipo. As mesmas regras que se aplicam à expressão CASE para expressões boolianas, manipulação de nulos e tipos de retorno também se aplicam a IIF. Para obter mais informações, consulte [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md).  
  
 O fato de IIF ser convertido em CASE também tem um impacto sobre outros aspectos do comportamento dessa função. Como as expressões CASE podem ser aninhadas apenas até o nível de 10, as instruções IIF também podem ser aninhadas apenas até o nível máximo de 10. Além disso, IIF é remota para outros servidores como uma expressão CASE semanticamente equivalente, com todos os comportamentos de uma expressão CASE remota.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-iif-example"></a>A. Exemplo de IIF simples  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
TRUE  
  
(1 row(s) affected)  
```  
  
### <a name="b-iif-with-null-constants"></a>B. IIF com constantes NULL  
  
```  
SELECT IIF ( 45 > 30, NULL, NULL ) AS Result;  
```  
  
 O resultado dessa instrução é um erro.  
  
### <a name="c-iif-with-null-parameters"></a>C. IIF com parâmetros NULL  
  
```  
DECLARE @P INT = NULL, @S INT = NULL;  
SELECT IIF ( 45 > 30, @p, @s ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CHOOSE &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  
