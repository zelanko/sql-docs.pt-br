---
title: ERROR_NUMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_NUMBER_TSQL
- ERROR_NUMBER
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], numbers
- TRY...CATCH [SQL Server]
- ERROR_NUMBER function
- CATCH block
ms.assetid: 1de85fff-1ca2-4b31-841b-926e571cb150
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74e87d0cf31e866d21d2027e40513d0c0598ea7a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999016"
---
# <a name="error_number-transact-sql"></a>ERROR_NUMBER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna o número do erro que fez com que o bloco CATCH de um constructo TRY…CATCH fosse executado.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ERROR_NUMBER ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
Quando chamado em um bloco CATCH, `ERROR_NUMBER` retorna o número do erro que fez com que o bloco CATCH fosse executado.  

`ERROR_NUMBER` retorna NULL quando chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Comentários  
`ERROR_NUMBER` dá suporte a chamadas em qualquer lugar dentro do escopo de um bloco CATCH.  
  
`ERROR_NUMBER` retorna um número de erro relevante, independentemente de quantas vezes ou de em que local ele é executado dentro do escopo do bloco `CATCH`. É diferente de uma função como @@ERROR, que retorna apenas um número de erro na instrução imediatamente após àquela que causa um erro.  

Em um bloco `CATCH` aninhado, `ERROR_NUMBER` retorna o número do erro específico do escopo do bloco `CATCH` que referenciou esse bloco `CATCH`. Por exemplo, o bloco `CATCH` de um constructo TRY...CATCH externo poderia ter um constructo `TRY...CATCH` interno. Dentro desse bloco `CATCH` interno, `ERROR_NUMBER` retorna o número do erro que invocou o bloco `CATCH` interno. Se `ERROR_NUMBER` é executado no bloco `CATCH` externo, ele retorna o número do erro que invocou esse bloco `CATCH` externo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-error_number-in-a-catch-block"></a>a. Usando ERROR_NUMBER em um bloco CATCH  
Este exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. O bloco `CATCH` retorna o número do erro.  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_NUMBER() AS ErrorNumber;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```
-----------

(0 row(s) affected)

ErrorNumber
-----------
8134

(1 row(s) affected)

```  
  
### <a name="b-using-error_number-in-a-catch-block-with-other-error-handling-tools"></a>B. Usando ERROR_NUMBER em um bloco CATCH com outras ferramentas de tratamento de erros  
Este exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. Juntamente com o número do erro, o bloco `CATCH` retorna informações sobre esse erro.  

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

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure   ErrorLine  ErrorMessage
----------- ------------- ----------- ---------------  ---------- ----------------------------------
8134        16            1           NULL             4          Divide by zero error encountered.

(1 row(s) affected)

```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)     
 [Referência de Erros e Eventos &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/errors-events/errors-and-events-reference-database-engine.md)     
  
  

