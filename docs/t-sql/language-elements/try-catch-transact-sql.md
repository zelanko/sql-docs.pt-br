---
title: TRY...CATCH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BEGIN_TRY_TSQL
- BEGIN_CATCH_TSQL
- TRY
- BEGIN TRY
- TRY_TSQL
- BEGIN CATCH
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN CATCH statement
- uncommittable transactions
- errors [SQL Server], TRY...CATCH
- TRY block [SQL Server]
- XACT_STATE function
- TRY...CATCH [SQL Server]
- BEGIN TRY statement
- CATCH block
ms.assetid: 248df62a-7334-4bca-8262-235a28f4b07f
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1487803dbbcb2ef09dd182dea2eaffa6a967badf
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54298923"
---
# <a name="trycatch-transact-sql"></a>TRY...CATCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  > [!div class="nextstepaction"]
  > [Compartilhe seus comentários sobre o Índice do SQL Docs!](https://aka.ms/sqldocsurvey)

  Implementa tratamento de erros para [!INCLUDE[tsql](../../includes/tsql-md.md)] semelhante ao tratamento de exceções nas linguagens [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Um grupo de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser incluído em um bloco TRY. Se ocorrer um erro no bloco TRY, o controle passará para outro grupo de instruções que está incluído em um bloco CATCH.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
BEGIN TRY  
     { sql_statement | statement_block }  
END TRY  
BEGIN CATCH  
     [ { sql_statement | statement_block } ]  
END CATCH  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *sql_statement*  
 É qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 *statement_block*  
 Qualquer grupo de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um lote ou incluso em um bloco BEGIN...END.  
  
## <a name="remarks"></a>Remarks  
 Um constructo TRY...CATCH captura todos os erros de execução com gravidade maior que 10 que não fecham a conexão de banco de dados.  
  
 Um bloco TRY deve ser seguido imediatamente por um bloco CATCH associado. A inclusão de qualquer outra instrução entre as instruções END TRY e BEGIN CATCH gera um erro de sintaxe.  
  
 Um constructo TRY...CATCH não pode abranger vários lotes. Um constructo TRY...CATCH não pode abranger vários blocos de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por exemplo, um constructo TRY...CATCH não pode abranger dois blocos BEGIN...END de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e não pode abranger um constructo IF...ELSE.  
  
 Se não houver erros no código incluído em um bloco TRY, quando a execução da última instrução no bloco TRY for concluída, o controle passará para a instrução imediatamente posterior à instrução END CATCH associada. Se houver um erro no código incluído em um bloco TRY, o controle passará para a primeira instrução do bloco CATCH associado. Se a instrução END CATCH for a última instrução de um procedimento armazenado ou gatilho, o controle voltará para a instrução que chamou o procedimento armazenado ou acionou o gatilho.  
  
 Quando o código no bloco CATCH for concluído, o controle passará para a instrução imediatamente posterior à instrução END CATCH. Os erros interceptados por um bloco CATCH não são retornados ao aplicativo que o chamou. Se qualquer parte das informações de erro precisar ser retornada ao aplicativo, o código no bloco CATCH deverá fazê-lo usando mecanismos como conjuntos de resultados SELECT ou as instruções RAISERROR e PRINT.  
  
 Os constructos TRY...CATCH podem ser aninhados. Um bloco TRY ou um bloco CATCH pode conter constructos TRY...CATCH aninhados. Por exemplo, um bloco CATCH pode conter um constructo TRY...CATCH inserido para tratar erros encontrados pelo código CATCH.  
  
 Os erros encontrados em um bloco CATCH são tratados como erros gerados em qualquer outro lugar. Se o bloco CATCH contiver um constructo TRY...CATCH aninhado, qualquer erro no bloco TRY aninhado passará o controle para o bloco CATCH aninhado. Se não houver nenhum constructo TRY...CATCH aninhado, o erro voltará para o chamador.  
  
 Os constructos TRY...CATCH capturam erros não tratados de procedimentos armazenados nem gatilhos executados pelo código do bloco TRY. Como alternativa, os procedimentos armazenados ou os gatilhos podem conter os próprios constructos TRY...CATCH para tratar os erros gerados por seu código. Por exemplo, quando um bloco TRY executa um procedimento armazenado e ocorre um erro no procedimento, o erro pode ser tratado das seguintes maneiras:  
  
-   Se o procedimento armazenado não contiver seu próprio constructo TRY...CATCH, o erro retornará o controle para o bloco CATCH associado ao bloco TRY que contém a instrução EXECUTE.  
  
-   Se o procedimento armazenado contiver um constructo TRY...CATCH, o erro transferirá o controle para o bloco CATCH do procedimento armazenado. Quando o código do bloco CATCH for concluído, o controle voltará para a instrução imediatamente posterior à instrução EXECUTE que chamou o procedimento armazenado.  
  
 As instruções GOTO não podem ser usadas para inserir um bloco TRY ou CATCH. As instruções GOTO podem ser usadas para saltar para um rótulo dentro do mesmo bloco TRY ou CATCH ou para sair de um bloco TRY ou CATCH.  
  
 O constructo TRY...CATCH não pode ser usado em uma função definida pelo usuário.  
  
## <a name="retrieving-error-information"></a>Recuperando informações de erro  
 No escopo de um bloco CATCH, as seguintes funções de sistema podem ser usadas para obter informações sobre o erro que causou a execução do bloco CATCH.  
  
-   [ERROR_NUMBER()](../../t-sql/functions/error-number-transact-sql.md) retorna o número do erro.  
  
-   [ERROR_SEVERITY()](../../t-sql/functions/error-severity-transact-sql.md) retorna a severidade.  
  
-   [ERROR_STATE()](../../t-sql/functions/error-state-transact-sql.md) retorna o número do estado do erro.  
  
-   [ERROR_PROCEDURE()](../../t-sql/functions/error-procedure-transact-sql.md) retorna o nome do procedimento armazenado ou do gatilho no qual ocorreu o erro.  
  
-   [ERROR_LINE()](../../t-sql/functions/error-line-transact-sql.md) retorna o número de linha dentro da rotina que causou o erro.  
  
-   [ERROR_MESSAGE()](../../t-sql/functions/error-message-transact-sql.md) retorna o texto completo da mensagem de erro. O texto inclui os valores fornecidos para qualquer parâmetro substituível, como comprimentos, nomes de objeto ou horas.  
  
Essas funções retornarão NULL se forem chamadas fora do escopo do bloco CATCH. As informações de erro podem ser recuperadas com o uso dessas funções em qualquer lugar no escopo do bloco CATCH. Por exemplo, o script a seguir mostra um procedimento armazenado que contém funções de tratamento de erros. No bloco `CATCH` de uma construção `TRY...CATCH`, o procedimento armazenado é chamado e as informações sobre o erro são retornadas.  
  
```sql  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_GetErrorInfo', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_GetErrorInfo;  
GO  
  
-- Create procedure to retrieve error information.  
CREATE PROCEDURE usp_GetErrorInfo  
AS  
SELECT  
    ERROR_NUMBER() AS ErrorNumber  
    ,ERROR_SEVERITY() AS ErrorSeverity  
    ,ERROR_STATE() AS ErrorState  
    ,ERROR_PROCEDURE() AS ErrorProcedure  
    ,ERROR_LINE() AS ErrorLine  
    ,ERROR_MESSAGE() AS ErrorMessage;  
GO  
  
BEGIN TRY  
    -- Generate divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    -- Execute error retrieval routine.  
    EXECUTE usp_GetErrorInfo;  
END CATCH;   
```  
  
 As funções ERROR\_\* também funcionam em um bloco `CATCH` dentro de um [procedimento armazenado compilado nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="errors-unaffected-by-a-trycatch-construct"></a>Erros não afetados por um constructo TRY...CATCH  
 Os constructos TRY...CATCH não interceptam as seguintes condições:  
  
-   Avisos ou mensagens informativas que têm uma severidade 10 ou menor.  
  
-   Erros que têm uma severidade 20 ou maior, que param o processamento de tarefa do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para a sessão. Se ocorrer um erro com gravidade 20 ou maior e a conexão de banco de dados não for interrompida, TRY...CATCH tratará o erro.  
  
-   Atenções, como solicitações da interrupção de cliente ou conexões de cliente desfeitas.  
  
-   Quando a sessão for finalizada por um administrador de sistema com o uso da instrução KILL.  
  
Os seguintes tipos de erros não são tratados por um bloco CATCH quando ocorrerem no mesmo nível de execução que o constructo TRY...CATCH:  
  
-   Erros de compilação, como erros de sintaxe, que impeçam a execução de um lote.  
  
-   Erros que ocorrem durante a recompilação em nível de instrução, como os erros de resolução do nome de objeto que ocorrem após a compilação, devido à resolução adiada do nome.  
-   Erros de resolução de nome de objeto   

  
Esses erros são retornados ao nível que executou o lote, o procedimento armazenado ou o gatilho.  
  
Se ocorrer um erro durante a compilação ou a recompilação no nível da instrução em um nível de execução inferior (por exemplo, ao executar sp_executesql ou um procedimento armazenado definido pelo usuário) dentro do bloco TRY, o erro ocorrerá em um nível inferior ao do constructo TRY...CATCH e será tratado pelo bloco CATCH associado.  
  
O exemplo a seguir mostra como um erro de resolução de nome de objeto gerado por uma instrução `SELECT` não é capturado pela construção `TRY...CATCH`, mas é capturado pelo bloco `CATCH` quando a mesma instrução `SELECT` é executada dentro de um procedimento armazenado.  
  
```sql  
BEGIN TRY  
    -- Table does not exist; object name resolution  
    -- error not caught.  
    SELECT * FROM NonexistentTable;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
       ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH  
```  
  
 O erro não é capturado e o controle é transmitido para fora da construção `TRY...CATCH` para o próximo nível mais alto.  
  
 A execução da instrução `SELECT` dentro de um procedimento armazenado fará com que o erro ocorra em um nível inferior ao do bloco `TRY`. O erro será tratado pela construção `TRY...CATCH`.  
  
```sql  
-- Verify that the stored procedure does not exist.  
IF OBJECT_ID ( N'usp_ExampleProc', N'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that will cause an   
-- object resolution error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT * FROM NonexistentTable;  
GO  
  
BEGIN TRY  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
```  
  
## <a name="uncommittable-transactions-and-xactstate"></a>Transações não confirmáveis e XACT_STATE  
 Se um erro gerado em um bloco TRY fizer com que o estado da transação atual seja invalidado, a transação será classificada como não confirmável. Um erro que normalmente finaliza uma transação fora de um bloco TRY faz com que uma transação entre em um estado não confirmável quando o erro ocorre dentro de um bloco TRY. Uma transação não confirmável só pode executar operações de leitura ou uma ROLLBACK TRANSACTION. A transação não pode executar nenhuma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que geraria uma operação de gravação ou uma COMMIT TRANSACTION. A função XACT_STATE retornará o valor -1 se uma transação foi classificada como não confirmável. Quando um lote é concluído, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reverte quaisquer transações ativas não confirmáveis. Se nenhuma mensagem de erro foi enviada quando a transação entrou em um estado não confirmável, quando o lote terminar, uma mensagem de erro será enviada ao aplicativo cliente. Isso indica que uma transação não confirmável foi detectada e revertida.  
  
 Para obter mais informações sobre transações não confirmáveis e a função XACT_STATE, consulte [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-trycatch"></a>A. Usando TRY...CATCH  
 O exemplo a seguir mostra uma instrução `SELECT` que gerará um erro de divisão por zero. O erro faz com que a execução salte para o bloco `CATCH` associado.  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-trycatch-in-a-transaction"></a>b. Usando TRY...CATCH em uma transação  
 O exemplo a seguir mostra como um bloco `TRY...CATCH` funciona dentro de uma transação. A instrução dentro do bloco `TRY` gera um erro de violação de restrição.  
  
```sql  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Generate a constraint violation error.  
    DELETE FROM Production.Product  
    WHERE ProductID = 980;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
### <a name="c-using-trycatch-with-xactstate"></a>C. Usando TRY...CATCH com XACT_STATE  
 O exemplo a seguir mostra como usar a construção `TRY...CATCH` para tratar erros que ocorrem dentro de uma transação. A função `XACT_STATE` determina se a transação deve ser confirmada ou revertida. Neste exemplo, `SET XACT_ABORT` é `ON`. Isso torna a transação não confirmável quando o erro de violação de restrição ocorrer.  
  
```sql  
-- Check to see whether this stored procedure exists.  
IF OBJECT_ID (N'usp_GetErrorInfo', N'P') IS NOT NULL  
    DROP PROCEDURE usp_GetErrorInfo;  
GO  
  
-- Create procedure to retrieve error information.  
CREATE PROCEDURE usp_GetErrorInfo  
AS  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_LINE () AS ErrorLine  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
GO  
  
-- SET XACT_ABORT ON will cause the transaction to be uncommittable  
-- when the constraint violation occurs.   
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the DELETE statement succeeds, commit the transaction.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Execute error retrieval routine.  
    EXECUTE usp_GetErrorInfo;  
  
    -- Test XACT_STATE:  
        -- If 1, the transaction is committable.  
        -- If -1, the transaction is uncommittable and should   
        --     be rolled back.  
        -- XACT_STATE = 0 means that there is no transaction and  
        --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT  
            N'The transaction is in an uncommittable state.' +  
            'Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is committable.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT  
            N'The transaction is committable.' +  
            'Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-trycatch"></a>D. Usando TRY...CATCH  
 O exemplo a seguir mostra uma instrução `SELECT` que gerará um erro de divisão por zero. O erro faz com que a execução salte para o bloco `CATCH` associado.  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Gravidades de erros do mecanismo de banco de dados](../../relational-databases/errors-events/database-engine-error-severities.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [GOTO &#40;Transact-SQL&#41;](../../t-sql/language-elements/goto-transact-sql.md)   
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md)   
 [SET XACT_ABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-xact-abort-transact-sql.md)  
  
  

