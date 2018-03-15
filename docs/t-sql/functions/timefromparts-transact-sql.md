---
title: TIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TIMEFROMPARTS_TSQL
- TIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- TIMEFROMPARTS function
ms.assetid: 786c65a1-2b3f-4e4b-82b6-4940d62f3801
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5e046e203e7ebd5243cdfc6f10948dfd353b2dd3
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Retorna um valor **time** para a hora especificada e com a precisão especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
 *hour*  
 Expressão de inteiro que especifica horas.  
  
 *minute*  
 Expressão de inteiro que especifica minutos.  
  
 *segundos*  
 Expressão de inteiro que especifica segundos.  
  
 *fractions*  
 Expressão de inteiro que especifica frações.  
  
 *precisão*  
 Literal de inteiro que especifica a precisão do valor **time** a ser retornado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **time(** *precision* **)**  
  
## <a name="remarks"></a>Remarks  
 TIMEROMPARTS retorna um valor de hora completamente inicializado. Se os argumentos forem inválidos, um erro será lançado. Se algum parâmetro for nulo, nulo será retornado. Porém, se o argumento *precision* for nulo, um erro será gerado.  
  
 O argumento *fractions* depende do argumento *precision*. Por exemplo, se *precision* for 7, cada fração representará 100 nanosegundos; se *precision* for 3, cada fração representará um milissegundo. Se o valor de *precision* for zero, o valor de *fractions* também deverá ser zero; caso contrário, um erro será gerado.  
  
 Essa função pode ser remota para servidores [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posteriores. Ela não pode ser remota para servidores com versão anterior à [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Exemplo simples sem frações de um segundo  
  
```  
SELECT TIMEFROMPARTS ( 23, 59, 59, 0, 0 ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------------------  
23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Exemplo simples com frações de um segundo  
 O seguinte exemplo demonstra o uso dos parâmetros *fractions* e *precision*:  
  
1.  Quando *fractions* tem um valor igual a 5 e *precision* tem um valor igual a 1, o valor de *fractions* representa 5/10 de um segundo.  
  
2.  Quando *fractions* tem um valor igual a 50 e *precision* tem um valor igual a 2, o valor de *fractions* representa 50/100 de um segundo.  
  
3.  Quando *fractions* tem um valor igual a 500 e *precision* tem um valor igual a 3, o valor de *fractions* representa 500/1.000 de um segundo.  
  
```sql  
SELECT TIMEFROMPARTS ( 14, 23, 44, 5, 1 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 50, 2 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 500, 3 );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------  
14:23:44.5  
  
(1 row(s) affected)  
  
----------------  
14:23:44.50  
  
(1 row(s) affected)  
  
----------------  
14:23:44.500  
  
(1 row(s) affected)  
```  
  

