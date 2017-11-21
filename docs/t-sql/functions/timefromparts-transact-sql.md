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
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: e7cb7497251a0a61cff9f71c07d3c5d9e9028d5d
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Retorna um **tempo** valor para o tempo especificado e com a precisão especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
 *hora*  
 Expressão de inteiro que especifica horas.  
  
 *minuto*  
 Expressão de inteiro que especifica minutos.  
  
 *segundos*  
 Expressão de inteiro que especifica segundos.  
  
 *frações*  
 Expressão de inteiro que especifica frações.  
  
 *precisão*  
 Literal de inteiro que especifica a precisão do **tempo** valor a ser retornado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **tempo (** *precisão* **)**  
  
## <a name="remarks"></a>Comentários  
 TIMEROMPARTS retorna um valor de hora completamente inicializado. Se os argumentos forem inválidos, um erro será lançado. Se algum parâmetro for nulo, nulo será retornado. No entanto, se o *precisão* argumento for nulo, será gerado um erro.  
  
 O *frações* depende do argumento de *precisão* argumento. Por exemplo, se *precisão* for 7, cada fração representará 100 nanosegundos; se *precisão* é 3 e, em seguida, cada fração representará um milissegundo. Se o valor de *precisão* for zero, o valor de *frações* também deve ser zero; caso contrário, ocorrerá um erro.  
  
 Essa função pode ser remota para servidores [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posteriores. Ele não pode ser remoto para servidores que têm uma versão inferior a[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
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
 O exemplo a seguir demonstra o uso do *frações* e *precisão* parâmetros:  
  
1.  Quando *frações* tem um valor de 5 e *precisão* tem um valor de 1, em seguida, o valor de *frações* representa 5 a 10 de segundo.  
  
2.  Quando *frações* tem um valor de 50 e *precisão* tem um valor de 2, em seguida, o valor de *frações* representa 50/100 de um segundo.  
  
3.  Quando *frações* tem um valor de 500 e *precisão* tem um valor de 3, em seguida, o valor de *frações* representará 500/1000 de um segundo.  
  
```tsql  
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
  


