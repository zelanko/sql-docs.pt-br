---
title: Retornar dados de um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 950e1d3ecf6283cd8d49c606412d351d1b554fae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="return-data-from-a-stored-procedure"></a>Retornar dados de um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 > Para ver o conteúdo relacionado a versões anteriores do SQL Server, consulte [Retornar dados de um procedimento armazenado](https://msdn.microsoft.com/en-US/library/ms188655(SQL.120).aspx).

  Há três formas de retornar dados de um procedimento para um programa de chamada: conjuntos de resultados, parâmetros de saída e códigos de retorno. Este tópico fornece informações sobre as três abordagens.  
  
  ## <a name="returning-data-using-result-sets"></a>Retorno de dados usando conjuntos de resultados
 Se você incluir uma instrução SELECT no corpo de um procedimento armazenado (mas não uma SELECT... INTO ou INSERT... SELECT), as linhas especificadas pela instrução SELECT serão enviadas diretamente ao cliente.  Para grandes conjuntos de resultados a execução do procedimento armazenado não continuará na próxima instrução até que o conjunto de resultados seja completamente enviado ao cliente.  Para pequenos conjuntos de resultados, os resultados serão colocados em spool para retornar ao cliente e a execução continuará.  Se várias dessas instruções SELECT forem executadas durante a execução do procedimento armazenado, vários conjuntos de resultados serão enviados ao cliente.  Esse comportamento também se aplica a lotes de TSQL aninhados, procedimentos armazenados aninhados e lotes de TSQL de nível superior.
 
 
 ### <a name="examples-of-returning-data-using-a-result-set"></a>Exemplos de dados de retorno usando um conjunto de resultados 
  O exemplo a seguir mostra um procedimento armazenado que retorna os valores LastName e SalesYTD para todas as linhas SalesPerson que também aparecem na exibição vEmployee.
  
 ```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
AS    
  
    SET NOCOUNT ON;  
    SELECT LastName, SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    
RETURN  
GO  
  
```  

  
## <a name="returning-data-using-an-output-parameter"></a>Retornando dados por meio de um parâmetro de saída  
 Caso a palavra-chave OUTPUT seja especificada para um parâmetro na definição do procedimento, o procedimento poderá retornar o valor atual do parâmetro para o programa de chamada na saída do procedimento. Para salvar o valor do parâmetro na variável que poderá ser usada no programa de chamada, o programa de chamada precisará usar a palavra-chave OUTPUT ao executar o procedimento. Para obter mais informações quais tipos de dados podem ser usados como parâmetros de saída, veja [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
### <a name="examples-of-output-parameter"></a>Exemplos de parâmetro de saída  
 O exemplo a seguir mostra um procedimento com parâmetros de entrada e de saída. O parâmetro `@SalesPerson` receberia um valor de entrada especificado pelo programa de chamada. A instrução SELECT usa o valor passado para o parâmetro de entrada para obter o valor `SalesYTD` correto. A instrução SELECT também atribui o valor ao parâmetro de saída `@SalesYTD` , que retorna o valor ao programa de chamada quando o procedimento sai.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 O exemplo a seguir chama o procedimento criado no primeiro exemplo e salva o valor de saída retornado do procedimento chamado na variável `@SalesYTD` , que é local para o programa de chamada.  
  
```  
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 Valores de entrada também podem ser especificados para parâmetros OUTPUT quando o procedimento é executado. Isso permite que o procedimento receba um valor do programa de chamada, altere-o ou realize operações com o valor e, em seguida, retorne o novo valor para o programa de chamada. No exemplo anterior, um valor pode ser atribuído à variável `@SalesYTDBySalesPerson` antes de o programa chamar o procedimento `Sales.uspGetEmployeeSalesYTD` . A instrução execute passaria o valor de variável `@SalesYTDBySalesPerson` para o parâmetro OUTPUT `@SalesYTD` . Depois, no corpo do procedimento, o valor poderia ser usado em cálculos que geram um novo valor. O novo valor seria devolvido do procedimento pelo parâmetro OUTPUT, atualizando o valor na variável `@SalesYTDBySalesPerson` , quando o procedimento saísse. Isto é denominado frequentemente como "capacidade de passagem-por-referência".  
  
 Quando você especifica OUTPUT para um parâmetro ao chamar um procedimento e esse parâmetro não é definido com OUTPUT na definição de procedimento, uma mensagem de erro é exibida. Entretanto, é possível executar um procedimento com parâmetros de saída e não especificar OUTPUT ao executar o procedimento. Uma mensagem de erro é exibida, mas não se pode usar valor de saída no programa de chamada.  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>Usando o tipo de dados de cursor em parâmetros OUTPUT  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] os procedimentos podem usar o tipo de dados **cursor** apenas para parâmetros OUTPUT. Se o tipo de dados **cursor** for especificado para um parâmetro, as palavras-chaves VARYING e OUTPUT deverão ser especificadas para esse parâmetro na definição do procedimento. Um parâmetro pode ser especificado como apenas OUTPUT, mas, se a palavra-chave VARYING for especificada na declaração do parâmetro, o tipo de dados deverá ser **cursor** e a palavra-chave OUTPUT também deverá ser especificada.  
  
> [!NOTE]  
>  O tipo de dados **cursor** não pode ser associado a variáveis de aplicativos por meio de APIs de banco de dados, como OLE DB, ODBC, ADO e DB-Library. Como os parâmetros OUTPUT devem ser associados antes de um aplicativo executar um procedimento, os procedimentos com parâmetros OUTPUT **cursor** não podem ser chamados das APIs do banco de dados. Esses procedimentos podem ser chamados de lotes, procedimentos ou gatilhos do [!INCLUDE[tsql](../../includes/tsql-md.md)] apenas quando a variável OUTPUT de **cursor** é atribuída a uma variável [!INCLUDE[tsql](../../includes/tsql-md.md)] cursor **local do** .  
  
### <a name="rules-for-cursor-output-parameters"></a>Regras para parâmetros de saída de cursor  
 As regras seguintes pertencem aos parâmetros de saída de **cursor** quando o procedimento é executado:  
  
-   Para um cursor de somente avanço, as linhas retornadas no conjunto de resultados do cursor são apenas as que estão na posição do cursor na conclusão da execução do procedimento, por exemplo:  
  
    -   Um cursor não rolável é aberto em um procedimento em um conjunto de resultados nomeado RS de 100 linhas.  
  
    -   O procedimento busca as primeiras 5 linhas de conjunto de resultados RS.  
  
    -   O procedimento retorna ao chamador.  
  
    -   O conjunto de resultados RS retornado ao chamador consiste de linhas de 6 a 100 do RS, e o cursor no chamador está posicionado antes da primeira linha do RS.  
  
-   No caso de um cursor de somente avanço, se o cursor estiver posicionado antes da primeira linha quando o procedimento sair, o conjunto de resultados inteiro será retornado ao lote, procedimento ou gatilho de chamada. No retorno, a posição do cursor é estabelecida antes da primeira linha.  
  
-   No caso de um cursor de somente avanço, se o cursor estiver posicionado depois do fim da última linha quando o procedimento sair, um conjunto de resultados vazio será retornado ao lote, procedimento ou gatilho de chamada.  
  
    > [!NOTE]  
    >  Um conjunto de resultados vazio não é igual a um valor nulo.  
  
-   No caso de um cursor rolável, todas as linhas no conjunto de resultados são retornadas ao lote, procedimento ou gatilho de chamada quando o procedimento sai. No retorno, a posição de cursor é mantida na posição da última busca executada no procedimento.  
  
-   Para qualquer tipo de cursor, se o cursor for fechado, um valor nulo será retornado ao lote, procedimento ou gatilho de chamada. Isso também acontecerá se o cursor for atribuído a um parâmetro, mas nunca for aberto.  
  
    > [!NOTE]  
    >  O estado fechado só tem importância no momento do retorno. Por exemplo, é válido fechar um cursor durante o procedimento, reabrindo-o no procedimento posteriormente, e retornar o conjunto de resultados desse cursor para o lote, procedimento ou gatilho de chamada.  
  
### <a name="examples-of-cursor-output-parameters"></a>Exemplos de parâmetros de saída de cursor  
 No exemplo a seguir, é criado um procedimento que especifica um parâmetro de saída, `@currency_cursor`, usando o tipo de dados **cursor**. O procedimento é chamado em um lote.  
 
 Primeiro, crie o procedimento que declara e, então, abra um cursor na tabela Moeda.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 A seguir, execute um lote que declare uma variável de cursor local, execute o procedimento para atribuir o cursor à variável local e depois busque as linhas do cursor.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>Retornando dados usando um código de retorno  
 Um procedimento pode retornar um valor inteiro chamado de código de retorno para indicar o status de execução de um procedimento. Especifique o código de retorno de um procedimento usando a instrução RETURN. Assim como em parâmetros OUTPUT, você deve salvar o código de retorno em uma variável quando o procedimento é executado para usar o valor de código de retorno no programa de chamada. Por exemplo, a variável de atribuição `@result` do tipo de dados **int** é usada para armazenar o código de retorno do procedimento `my_proc`, como:  
  
```  
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 Os códigos de retorno são geralmente usados em blocos de controle de fluxo em procedimentos para definir o valor de código de retorno para cada situação de erro possível. Você pode usar a função @@ERROR após uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] para detectar se ocorreu um erro durante a execução da instrução.  Antes da introdução do tratamento de erro TRY/CATCH/THROW no TSQL, era necessário que, às vezes, os códigos de retorno determinassem o êxito ou a falha dos procedimentos armazenados.  Os procedimentos armazenados devem sempre indicar falha com um erro (gerado com THROW/RAISERROR, se necessário) e não contar com um código de retorno para indicar a falha.  Além disso, você também deve evitar o uso de código de retorno para retornar dados de aplicativo.
  
### <a name="examples-of-return-codes"></a>Exemplos de códigos de retorno  
 O exemplo a seguir mostra o procedimento `usp_GetSalesYTD` com tratamento de erros que define valores de código de retorno especiais para vários erros. A tabela a seguir mostra o valor de inteiro atribuído pelo procedimento a cada erro possível, e o significado correspondente de cada valor.  
  
|Valor de código de retorno|Significado|  
|-----------------------|-------------|  
|0|Execução bem-sucedida.|  
|1|O valor de parâmetro necessário não foi especificado.|  
|2|O valor de parâmetro especificado não é válido.|  
|3|Erro ocorrido ao obter o valor de vendas.|  
|4|Valor de vendas NULL encontrado para o vendedor.|  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 O exemplo a seguir cria um programa para controlar os códigos de retorno retornados do procedimento `usp_GetSalesYTD` .  
  
```  
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'EERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
