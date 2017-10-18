---
title: '@@ERROR (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ERROR'
- '@@ERROR_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ERROR function'
- errors [SQL Server], Transact-SQL
- error numbers [SQL Server]
ms.assetid: c8b43477-b6c0-49bf-a608-394a0b6cc7a2
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ef3f7b2f0b051fd79dd59325af7900aefff95a9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40error-transact-sql"></a>&#x40;&#x40; Erro (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o número do erro da última instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] executada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@ERROR  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 inteiro  
  
## <a name="remarks"></a>Comentários  
 Retornará 0 se a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] anterior não tiver encontrado nenhum erro.  
  
 Retornará um número de erro se a instrução anterior encontrar um erro. Se o erro foi um dos erros na exibição do catálogo sys. messages, em seguida,@ERROR contém o valor da coluna message_id para esse erro. Você pode exibir o texto associado com um @@ERROR número do erro em sys. messages.  
  
 Como @@ERROR está desmarcada e redefinir em cada instrução executada, verifique-o imediatamente após a instrução que está sendo verificada ou salvá-lo em uma variável local que pode ser verificada mais tarde.  
  
 Use a construção TRY...CATCH para manipular erros. O bloco TRY... CATCH construir também dá suporte a mais funções do sistema (ERROR_LINE, ERROR_MESSAGE, ERROR_PROCEDURE, ERROR_SEVERITY e ERROR_STATE) que retornam mais informações de erro @@ERROR. TRY...CATCH também oferece suporte a uma função ERROR_NUMBER não limitada a retornar o número de erro na instrução imediatamente após a instrução que gerou um erro. Para obter mais informações, consulte [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-error-to-detect-a-specific-error"></a>A. Usando @@ERROR para detectar um erro específico  
 O exemplo a seguir usa `@@ERROR` para verificar se existe violação de restrição (erro #547) em uma instrução `UPDATE`.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.EmployeePayHistory  
    SET PayFrequency = 4  
    WHERE BusinessEntityID = 1;  
IF @@ERROR = 547  
    PRINT N'A check constraint violation occurred.';  
GO  
```  
  
### <a name="b-using-error-to-conditionally-exit-a-procedure"></a>B. Usando @@ERROR para sair de um procedimento condicionalmente  
 O exemplo a seguir usa `IF...ELSE` instruções para testar `@@ERROR` após um `INSERT` instrução em um procedimento armazenado. O valor da variável `@@ERROR` determina o código de retorno enviado ao programa que está chamando, indicando o sucesso ou a falha do procedimento.  
  
```  
USE AdventureWorks2012;  
GO  
-- Drop the procedure if it already exists.  
IF OBJECT_ID(N'HumanResources.usp_DeleteCandidate', N'P') IS NOT NULL  
    DROP PROCEDURE HumanResources.usp_DeleteCandidate;  
GO  
-- Create the procedure.  
CREATE PROCEDURE HumanResources.usp_DeleteCandidate   
    (  
    @CandidateID INT  
    )  
AS  
-- Execute the DELETE statement.  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = @CandidateID;  
-- Test the error value.  
IF @@ERROR <> 0   
    BEGIN  
        -- Return 99 to the calling program to indicate failure.  
        PRINT N'An error occurred deleting the candidate information.';  
        RETURN 99;  
    END  
ELSE  
    BEGIN  
        -- Return 0 to the calling program to indicate success.  
        PRINT N'The job candidate has been deleted.';  
        RETURN 0;  
    END;  
GO  
```  
  
### <a name="c-using-error-with-rowcount"></a>C. Usando @@ERROR com @@ROWCOUNT   
 O exemplo a seguir usa `@@ERROR` com `@@ROWCOUNT` para validar a operação de uma instrução `UPDATE`. O valor de `@@ERROR` é verificado para não haver indicação de erro, e `@@ROWCOUNT` é usado para garantir que a atualização foi aplicada com sucesso na linha da tabela.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Purchasing.usp_ChangePurchaseOrderHeader',N'P')IS NOT NULL  
    DROP PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader;  
GO  
CREATE PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader  
    (  
    @PurchaseOrderID INT  
    ,@BusinessEntityID INT  
   )  
AS  
-- Declare variables used in error checking.  
DECLARE @ErrorVar INT;  
DECLARE @RowCountVar INT;  
  
-- Execute the UPDATE statement.  
UPDATE PurchaseOrderHeader   
    SET BusinessEntityID = @BusinessEntityID   
    WHERE PurchaseOrderID = @PurchaseOrderID;  
  
-- Save the @@ERROR and @@ROWCOUNT values in local   
-- variables before they are cleared.  
SELECT @ErrorVar = @@ERROR  
    ,@RowCountVar = @@ROWCOUNT;  
  
-- Check for errors. If an invalid @BusinessEntityID was specified,  
-- the UPDATE statement returns a foreign key violation error #547.  
IF @ErrorVar <> 0  
    BEGIN  
        IF @ErrorVar = 547  
            BEGIN  
                PRINT N'ERROR: Invalid ID specified for new employee.';  
                 RETURN 1;  
            END  
        ELSE  
            BEGIN  
                PRINT N'ERROR: error '  
                    + RTRIM(CAST(@ErrorVar AS NVARCHAR(10)))  
                    + N' occurred.';  
                RETURN 2;  
            END  
    END  
  
-- Check the row count. @RowCountVar is set to 0   
-- if an invalid @PurchaseOrderID was specified.  
IF @RowCountVar = 0  
    BEGIN  
        PRINT 'Warning: The BusinessEntityID specified is not valid';  
        RETURN 1;  
    END  
ELSE  
    BEGIN  
        PRINT 'Purchase order updated with the new employee';  
        RETURN 0;  
    END;  
GO  
```  

  
## <a name="see-also"></a>Consulte também  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sys. messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  


