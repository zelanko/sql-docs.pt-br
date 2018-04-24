---
title: ERROR_SEVERITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f6b3f8051243e2f2afc2204f190320cf4af23a85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="errorseverity-transact-sql"></a>ERROR_SEVERITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a severidade do erro que fez o bloco CATCH de uma construção TRY…CATCH ser executado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ERROR_SEVERITY ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
 Quando chamado em um bloco CATCH, retorna a severidade da mensagem de erro que fez esse bloco ser executado.  
  
 Retorna NULL se for chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Remarks  
 ERROR_SEVERITY pode ser chamado em qualquer lugar dentro do escopo de um bloco CATCH.  
  
 ERROR_SEVERITY retorna a severidade de erro, independentemente do número de vezes que é executado ou se é executado dentro do escopo do bloco CATCH. Isso é diferente de funções como @@ERROR, que retornam apenas o número de erro na instrução imediatamente posterior àquela que causa um erro, ou na primeira instrução de um bloco CATCH.  
  
 Em blocos CATCH aninhados, ERROR_SEVERITY retorna a severidade de erro específica do escopo do bloco CATCH no qual é referenciado. Por exemplo, o bloco CATCH de uma construção TRY...CATCH externa poderia ter uma construção TRY...CATCH aninhada. Dentro do bloco CATCH aninhado, ERROR_SEVERITY retorna a severidade de erro que invocou o bloco CATCH aninhado. Se ERROR_SEVERITY for executado em um bloco CATCH externo, retornará a severidade de erro que invocou esse bloco CATCH.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-errorseverity-in-a-catch-block"></a>A. Usando ERROR_SEVERIRTY em um bloco CATCH  
 O exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. A severidade do erro é retornada.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>B. Usando ERROR_SEVERITY em um bloco CATCH com outras ferramentas de tratamento de erros  
 O exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. Junto com a severidade, são retornadas as informações relacionadas ao erro.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>C. Usando ERROR_SEVERITY em um bloco CATCH com outras ferramentas de tratamento de erros  
 O exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. Junto com a severidade, são retornadas as informações relacionadas ao erro.  
  
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
  
  

