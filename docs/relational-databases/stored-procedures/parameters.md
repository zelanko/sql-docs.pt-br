---
title: Parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- user-defined functions [SQL Server], parameters
ms.assetid: c1f9bd93-3271-4098-a23b-7bd7a19ab65b
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9422e6c8b406258210e03262014d04abc1a4d3ba
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68136728"
---
# <a name="parameters"></a>parâmetros
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
São usados parâmetros para troca de dados entre procedimentos armazenados e funções e entre o aplicativo ou a ferramenta que chamam o procedimento armazenado ou a função: 

*  Os parâmetros de entrada permitem que o chamador transfira valores de dados para procedimentos armazenados ou funções.
*  Os parâmetros de entrada permitem que os procedimentos armazenados passem valores de dados ou variável de cursor de volta ao chamador. As funções definidas pelo usuário não podem especificar parâmetros de saída.
*  Todo procedimento armazenado retorna um código inteiro de retorno para o chamador. Se o procedimento armazenado não definir explicitamente um valor para o código de retorno, o código de retorno será 0.

O seguinte procedimento armazenado mostra o uso de um parâmetro de entrada, parâmetro de saída e código de retorno:
```
-- Create a procedure that takes one input parameter and returns one output parameter and a return code.
CREATE PROCEDURE SampleProcedure @EmployeeIDParm INT,
         @MaxTotal INT OUTPUT
AS
-- Declare and initialize a variable to hold @@ERROR.
DECLARE @ErrorSave INT
SET @ErrorSave = 0

-- Do a SELECT using the input parameter.
SELECT FirstName, LastName, JobTitle
FROM HumanResources.vEmployee
WHERE EmployeeID = @EmployeeIDParm

-- Save any nonzero @@ERROR value.
IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Set a value in the output parameter.
SELECT @MaxTotal = MAX(TotalDue)
FROM Sales.SalesOrderHeader;

IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Returns 0 if neither SELECT statement had an error; otherwise, returns the last error.
RETURN @ErrorSave
GO
```

Quando um procedimento armazenado ou uma função são executados, os parâmetros de entrada podem ter seus valores definidos como uma constante ou podem usar o valor de uma variável. Os parâmetros de saída e códigos de retorno devem retornar seus valores para uma variável. Parâmetros e códigos de retorno podem trocar valores de dados com variáveis Transact-SQL ou variáveis de aplicativo.

Se um procedimento armazenado for chamado por meio de um lote ou script, os parâmetros e valores de código de retorno poderão usar as variáveis Transact-SQL definidas no mesmo lote. O exemplo a seguir é um lote que executa o procedimento criado anteriormente. O parâmetro de entrada é especificado como uma constante e o parâmetro de saída e o código de retorno colocam seus valores em variáveis Transact-SQL:
```
-- Declare the variables for the return code and output parameter.
DECLARE @ReturnCode INT
DECLARE @MaxTotalVariable INT

-- Execute the stored procedure and specify which variables
-- are to receive the output parameter and return code values.
EXEC @ReturnCode = SampleProcedure @EmployeeIDParm = 19,
   @MaxTotal = @MaxTotalVariable OUTPUT

-- Show the values returned.
PRINT ' '
PRINT 'Return code = ' + CAST(@ReturnCode AS CHAR(10))
PRINT 'Maximum Quantity = ' + CAST(@MaxTotalVariable AS CHAR(10))
GO
```

Um aplicativo pode usar marcadores de parâmetro associados a variáveis de programa para trocar dados entre variáveis de aplicativo, parâmetros e códigos de retorno.

## <a name="see-also"></a>Consulte Também
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [Seção Reutilização de parâmetros e plano de execução](../../relational-databases/query-processing-architecture-guide.md)   
 [Variáveis (Transact-SQL)](../../t-sql/language-elements/variables-transact-sql.md)
