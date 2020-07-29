---
title: ERROR_SEVERITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_SEVERITY_TSQL
- ERROR_SEVERITY
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], severity
- messages [SQL Server], severity
- TRY...CATCH [SQL Server]
- CATCH block
- ERROR_SEVERITY function
ms.assetid: 50228f2f-6949-4d2e-8e43-fad11bf973ab
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 72d48e01cf44a0c8e3d03bcd665ca35dc876147f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111594"
---
# <a name="error_severity-transact-sql"></a>ERROR_SEVERITY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna o valor da gravidade do erro em que um erro ocorre se esse erro que fez com que o bloco CATCH de um constructo TRY...CATCH fosse executado.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
ERROR_SEVERITY ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="return-value"></a>Valor retornado  
Quando chamado em um bloco CATCH em que um erro ocorre, `ERROR_SEVERITY` retorna o valor da gravidade do erro que fez esse bloco `CATCH` ser executado.  

`ERROR_SEVERITY` retorna NULL se chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Comentários  
`ERROR_SEVERITY` dá suporte a chamadas em qualquer lugar dentro do escopo de um bloco CATCH.  
  
`ERROR_SEVERITY` retorna o valor da gravidade de um erro, independentemente de quantas vezes ou de em que local ele é executado dentro do escopo do bloco `CATCH`. É diferente de uma função como @@ERROR, que retorna apenas um número de erro na instrução imediatamente após àquela que causa um erro.  
  
`ERROR_SEVERITY` normalmente opera em um bloco `CATCH` aninhado. `ERROR_SEVERITY` retorna o valor da gravidade do erro específico do escopo do bloco `CATCH` que referenciou esse bloco `CATCH`. Por exemplo, o bloco `CATCH` de um constructo TRY...CATCH externo poderia ter um constructo `TRY...CATCH` interno. Dentro desse bloco `CATCH` interno, `ERROR_SEVERITY` retorna o valor da gravidade do erro que invocou o bloco `CATCH` interno. Se `ERROR_SEVERITY` executa no bloco `CATCH` externo, ele retorna o valor da gravidade do erro que invocou esse bloco `CATCH` externo.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-error_severity-in-a-catch-block"></a>a. Usando ERROR_SEVERIRTY em um bloco CATCH  
Este exemplo mostra um procedimento armazenado que gera um erro de divisão por zero. `ERROR_SEVERITY` retorna o valor da gravidade desse erro.  

```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```
-----------

(0 row(s) affected)

ErrorSeverity
-------------
16

(1 row(s) affected)

```  
  
### <a name="b-using-error_severity-in-a-catch-block-with-other-error-handling-tools"></a>B. Usando ERROR_SEVERITY em um bloco CATCH com outras ferramentas de tratamento de erros  
Este exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. O procedimento armazenado retorna informações sobre o erro.  

```sql  
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

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine   ErrorMessage
----------- ------------- ----------- --------------- ----------- ----------------------------------
8134        16            1           NULL            4           Divide by zero error encountered.

(1 row(s) affected)

```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
 [Referência de Erros e Eventos &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/errors-events/errors-and-events-reference-database-engine.md)     
  
    

