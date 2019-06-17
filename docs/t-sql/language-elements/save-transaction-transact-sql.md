---
title: SAVE TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SAVE
- SAVE_TSQL
- SAVE_TRANSACTION_TSQL
- SAVE TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- rolling back transactions, SAVE TRANSACTION
- SAVE TRANSACTION statement
- transactions [SQL Server], rolling back
- marking transactions [SQL Server]
- savepoints [SQL Server]
- marked transactions [SQL Server], SAVE TRANSACTION statement
- duplicate savepoints
ms.assetid: b953c3f1-f96d-42f1-95a2-30e314292b35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 873a02649eea5fb709f7c61b3c16c4a8141c08ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980286"
---
# <a name="save-transaction-transact-sql"></a>SAVE TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define um ponto de salvamento em uma transação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

 ## <a name="syntax"></a>Sintaxe  
  
```  
  
SAVE { TRAN | TRANSACTION } { savepoint_name | @savepoint_variable }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *savepoint_name*  
 É o nome atribuído ao ponto de salvamento. Os nomes de ponto de salvamento devem estar de acordo com as regras para identificadores, mas são limitados a 32 caracteres. *savepoint_name* sempre diferencia maiúsculas de minúsculas, mesmo quando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não diferencia maiúsculas de minúsculas.  
  
 @*savepoint_variable*  
 É o nome de uma variável definida pelo usuário que contém um nome de ponto de salvamento válido. A variável precisa ser declarada com o tipo de dados **char**, **varchar**, **nchar** ou **nvarchar**. Podem ser passados mais de 32 caracteres para a variável; porém, apenas os primeiros 32 caracteres são usados.  
  
## <a name="remarks"></a>Remarks  
 Um usuário pode definir um ponto de salvamento, ou marcador, em uma transação. O ponto de salvamento define um local para o qual a transação poderá retornar se parte da transação for cancelada condicionalmente. Se uma transação for revertida a um ponto de salvamento, ela deverá prosseguir para a conclusão com mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], se necessário, e uma instrução COMMIT TRANSACTION, ou deverá ser totalmente cancelada pela reversão da transação ao seu início. Para cancelar uma transação inteira, use o formato ROLLBACK TRANSACTION *transaction_name*. Todas as instruções ou procedimentos da transação são desfeitos.  
  
 Nomes de pontos de salvamento duplicados são permitidos em uma transação; porém, uma instrução ROLLBACK TRANSACTION que especifica o nome do ponto de salvamento só reverterá a transação para a SAVE TRANSACTION mais recente, usando esse nome.  
  
 Não há suporte para SAVE TRANSACTION em transações distribuídas iniciadas tanto explicitamente com BEGIN DISTRIBUTED TRANSACTION quanto escaladas de uma transação local.  
  
> [!IMPORTANT]  
>  Uma instrução ROLLBACK TRANSACTION que especifica um savepoint_name libera qualquer bloqueio adquirido além do ponto de salvamento, exceto escalonamentos e conversões. Esses bloqueios não são liberados e não são revertidos ao modo de bloqueio anterior.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar um ponto de salvamento de transação para reverter apenas as modificações feitas por um procedimento armazenado caso uma transação ativa seja iniciada antes de o procedimento armazenado ser executado.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
           WHERE name = N'SaveTranExample')  
    DROP PROCEDURE SaveTranExample;  
GO  
CREATE PROCEDURE SaveTranExample  
    @InputCandidateID INT  
AS  
    -- Detect whether the procedure was called  
    -- from an active transaction and save  
    -- that for later use.  
    -- In the procedure, @TranCounter = 0  
    -- means there was no active transaction  
    -- and the procedure started one.  
    -- @TranCounter > 0 means an active  
    -- transaction was started before the   
    -- procedure was called.  
    DECLARE @TranCounter INT;  
    SET @TranCounter = @@TRANCOUNT;  
    IF @TranCounter > 0  
        -- Procedure called when there is  
        -- an active transaction.  
        -- Create a savepoint to be able  
        -- to roll back only the work done  
        -- in the procedure if there is an  
        -- error.  
        SAVE TRANSACTION ProcedureSave;  
    ELSE  
        -- Procedure must start its own  
        -- transaction.  
        BEGIN TRANSACTION;  
    -- Modify database.  
    BEGIN TRY  
        DELETE HumanResources.JobCandidate  
            WHERE JobCandidateID = @InputCandidateID;  
        -- Get here if no errors; must commit  
        -- any transaction started in the  
        -- procedure, but not commit a transaction  
        -- started before the transaction was called.  
        IF @TranCounter = 0  
            -- @TranCounter = 0 means no transaction was  
            -- started before the procedure was called.  
            -- The procedure must commit the transaction  
            -- it started.  
            COMMIT TRANSACTION;  
    END TRY  
    BEGIN CATCH  
        -- An error occurred; must determine  
        -- which type of rollback will roll  
        -- back only the work done in the  
        -- procedure.  
        IF @TranCounter = 0  
            -- Transaction started in procedure.  
            -- Roll back complete transaction.  
            ROLLBACK TRANSACTION;  
        ELSE  
            -- Transaction started before procedure  
            -- called, do not roll back modifications  
            -- made before the procedure was called.  
            IF XACT_STATE() <> -1  
                -- If the transaction is still valid, just  
                -- roll back to the savepoint set at the  
                -- start of the stored procedure.  
                ROLLBACK TRANSACTION ProcedureSave;  
                -- If the transaction is uncommitable, a  
                -- rollback to the savepoint is not allowed  
                -- because the savepoint rollback writes to  
                -- the log. Just return to the caller, which  
                -- should roll back the outer transaction.  
  
        -- After the appropriate rollback, echo error  
        -- information to the caller.  
        DECLARE @ErrorMessage NVARCHAR(4000);  
        DECLARE @ErrorSeverity INT;  
        DECLARE @ErrorState INT;  
  
        SELECT @ErrorMessage = ERROR_MESSAGE();  
        SELECT @ErrorSeverity = ERROR_SEVERITY();  
        SELECT @ErrorState = ERROR_STATE();  
  
        RAISERROR (@ErrorMessage, -- Message text.  
                   @ErrorSeverity, -- Severity.  
                   @ErrorState -- State.  
                   );  
    END CATCH  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md)  
  
  
