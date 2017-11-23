---
title: ERROR_NUMBER (Transact-SQL) | Microsoft Docs
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
- ERROR_NUMBER_TSQL
- ERROR_NUMBER
dev_langs: TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], numbers
- TRY...CATCH [SQL Server]
- ERROR_NUMBER function
- CATCH block
ms.assetid: 1de85fff-1ca2-4b31-841b-926e571cb150
caps.latest.revision: "50"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 88a6b73698c38e88905ea5efe3883a5d0d73d85e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="errornumber-transact-sql"></a>ERROR_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o número do erro que fez com que o bloco CATCH de uma construção TRY…CATCH fosse executado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ERROR_NUMBER ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="return-value"></a>Valor de retorno  
 Quando chamado em um bloco CATCH, retorna o número do erro da mensagem de erro que fez o bloco ser executado.  
  
 Retorna NULL se for chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Comentários  
 Esta função pode ser chamada em qualquer lugar dentro do escopo de um bloco CATCH.  
  
 ERROR_NUMBER retorna o número do erro, independentemente do número de vezes que ele é executado ou se é executado dentro do escopo do bloco CATCH. Isso é em comparação com@ERROR, que retorna somente o número do erro na instrução imediatamente posterior àquela que causa um erro ou bloquear a primeira instrução de um problema.  
  
 Em blocos CATCH aninhados, ERROR_NUMBER retorna o número do erro específico do escopo do bloco CATCH no qual é referenciado. Por exemplo, o bloco CATCH de uma construção TRY...CATCH externa poderia ter uma construção TRY...CATCH aninhada. Dentro do bloco CATCH aninhado, ERROR_NUMBER retorna o número do erro que invocou o bloco CATCH aninhado. Se ERROR_NUMBER for executado em um bloco CATCH externo, retornará o número do erro que invocou aquele bloco CATCH.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-errornumber-in-a-catch-block"></a>A. Usando ERROR_NUMBER em um bloco CATCH  
 O exemplo de código a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. O número do erro é retornado.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_NUMBER() AS ErrorNumber;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errornumber-in-a-catch-block-with-other-error-handling-tools"></a>B. Usando ERROR_NUMBER em um bloco CATCH com outras ferramentas de tratamento de erros  
 O exemplo de código a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. Juntamente com o número do erro, são retornadas as informações relacionadas ao erro.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errornumber-in-a-catch-block-with-other-error-handling-tools"></a>C. Usando ERROR_NUMBER em um bloco CATCH com outras ferramentas de tratamento de erros  
 O exemplo de código a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. Juntamente com o número do erro, são retornadas as informações relacionadas ao erro.  
  
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
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

