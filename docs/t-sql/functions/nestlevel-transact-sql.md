---
description: '&#x40;&#x40;NESTLEVEL (Transact-SQL)'
title: '@@NESTLEVEL (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@NESTLEVEL'
- '@@NESTLEVEL_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@NESTLEVEL function'
- nesting stored procedures
- stored procedure nesting levels [SQL Server]
ms.assetid: 8c0b2134-8616-44f6-addc-6583c432fb62
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a6c28eca6f0496e8e66deef9a26aa4e7ef45ea81
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445725"
---
# <a name="x40x40nestlevel-transact-sql"></a>&#x40;&#x40;NESTLEVEL (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o nível aninhando da execução de procedimento armazenado atual (inicialmente 0) no servidor local.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@NESTLEVEL  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários  
 O nível é incrementado sempre que um procedimento armazenado chama outro procedimento armazenado ou executa código gerenciado fazendo referência a uma rotina, um tipo ou uma agregação CLR (Common Language Runtime). Quando o máximo de 32 for excedido, a transação será terminada.  
  
 Quando @@NESTLEVEL é executado em uma cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)], o valor retornado é 1 + o nível de aninhamento atual. Quando @@NESTLEVEL é executado dinamicamente usando sp_executesql, o valor retornado é 2 + o nível de aninhamento atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-nestlevel-in-a-procedure"></a>a. Usando @@NESTLEVEL em um procedimento  
 O exemplo a seguir cria dois procedimentos: um que chama o outro e um que exibe a configuração `@@NESTLEVEL` de cada um deles.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'usp_OuterProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_OuterProc;  
GO  
IF OBJECT_ID (N'usp_InnerProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_InnerProc;  
GO  
CREATE PROCEDURE usp_InnerProc AS   
    SELECT @@NESTLEVEL AS 'Inner Level';  
GO  
CREATE PROCEDURE usp_OuterProc AS   
    SELECT @@NESTLEVEL AS 'Outer Level';  
    EXEC usp_InnerProc;  
GO  
EXECUTE usp_OuterProc;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Outer Level  
-----------  
1  
  
Inner Level  
-----------  
2
```  
  
### <a name="b-calling-nestlevel"></a>B. Chamando @@NESTLEVEL  
 O exemplo a seguir mostra a diferença nos valores retornados por `SELECT`, `EXEC` e `sp_executesql` quando cada um deles chama `@@NESTLEVEL`.  
  
```  
CREATE PROC usp_NestLevelValues AS  
    SELECT @@NESTLEVEL AS 'Current Nest Level';  
EXEC ('SELECT @@NESTLEVEL AS OneGreater');   
EXEC sp_executesql N'SELECT @@NESTLEVEL as TwoGreater' ;  
GO  
EXEC usp_NestLevelValues;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Current Nest Level  
------------------  
1  
  
(1 row(s) affected)  
  
OneGreater  
-----------  
2  
  
(1 row(s) affected)  
  
TwoGreater  
-----------  
3  
  
(1 row(s) affected)
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
