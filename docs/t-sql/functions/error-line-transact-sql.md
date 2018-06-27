---
title: ERROR_LINE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 347233585a00c73d006fa0115fb703d57fc16ca2
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249659"
---
# <a name="errorline-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna o número de linha da ocorrência de um erro que fez com que o bloco CATCH de um constructo TRY…CATCH fosse executado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>Tipo de retorno  
**int**  
  
## <a name="return-value"></a>Valor retornado  
Quando chamado em um bloco CATCH, `ERROR_LINE` retorna  
  
-   o número de linha em que o erro ocorreu    
-   o número de linha em uma rotina se o erro ocorreu dentro de um procedimento armazenado ou gatilho  
-   NULL, se chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Remarks  
Uma chamada a `ERROR_LINE` pode ocorrer em qualquer lugar dentro do escopo de um bloco CATCH.  
  
`ERROR_LINE` retorna o número de linha em que o erro ocorreu. Isso acontece independentemente da localização da chamada `ERROR_LINE` dentro do escopo do bloco CATCH e independentemente do número de chamadas para `ERROR_LINE`. Isso contrasta com funções como @@ERROR. @@ERROR retorna um número de erro na instrução imediatamente após aquela que causa um erro ou na primeira instrução de um bloco CATCH.  
  
Em blocos CATCH aninhados, `ERROR_LINE` retorna o número de linha do erro específico ao escopo do bloco CATCH no qual ele é referenciado. Por exemplo, o bloco CATCH de uma construção TRY...CATCH poderia ter uma construção TRY...CATCH aninhada. Dentro do bloco CATCH aninhado, `ERROR_LINE` retorna o número de linha do erro que invocou o bloco CATCH aninhado. Se `ERROR_LINE` for executado em um bloco CATCH externo, ele retornará o número de linha do erro que invocou aquele bloco CATCH específico.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-errorline-in-a-catch-block"></a>A. Usando ERROR_LINE em um bloco CATCH  
Este exemplo de código a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. `ERROR_LINE` retorna o número de linha em que ocorreu o erro.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
Result 
-----------

(0 row(s) affected)

ErrorLine
-----------
4

(1 row(s) affected)
```  
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>B. Usando ERROR_LINE em um bloco CATCH com um procedimento armazenado  
Este exemplo mostra um procedimento armazenado que gera um erro de divisão por zero. `ERROR_LINE` retorna o número de linha em que ocorreu o erro.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that  
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
``` 
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorLine
-----------
7

(1 row(s) affected)  
   
```

### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>C. Usando ERROR_LINE em um bloco CATCH com outras ferramentas de tratamento de erros  
Este exemplo de código a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. `ERROR_LINE` retorna o número de linha em que ocorreu o erro e informações sobre o erro propriamente dito.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
``` 
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState ErrorProcedure ErrorLine ErrorMessage
----------- ------------- ---------- -------------- --------- ---------------------------------
8134        16            1          NULL           3         Divide by zero error encountered.

(1 row(s) affected)
  
```
  
## <a name="see-also"></a>Consulte Também  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
