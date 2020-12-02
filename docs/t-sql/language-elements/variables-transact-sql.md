---
description: Variáveis (Transact-SQL)
title: Variáveis (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f372ae86-a003-40af-92de-fa52e3eea13f
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 264a277c45ebd1f067318625f7b0f1fb986389d4
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92196140"
---
# <a name="variables-transact-sql"></a>Variáveis (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Uma variável local Transact-SQL é um objeto que pode conter um único valor de dados de um tipo específico. As variáveis em lotes e scripts são normalmente usadas: 

* Como um contador, para contar o número de vezes que um loop é executado ou controlar quantas vezes que o loop é executado.
* Para reter um valor de dados a ser testado por uma instrução de controle de fluxo.
* Para salvar um valor de dados a ser retornado por um código de retorno de procedimento armazenado ou valor de retorno de função.

> [!NOTE]
> - Os nomes de algumas funções do sistema Transact-SQL começam com dois sinais de *arroba* (\@\@). Embora nas versões anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as funções \@\@ sejam conhecidas como variáveis globais, as funções \@\@ não são variáveis e não têm os mesmos comportamentos de variáveis. As funções \@\@ são funções de sistema, e o uso de sua sintaxe segue as regras das funções.
> - Você não pode usar variáveis em uma exibição.
> - As alterações nas variáveis não são afetadas pela reversão de uma transação.

O script seguinte cria uma tabela de teste pequena e a popula com 26 linhas. O script usa uma variável para fazer três coisas: 

* Controlar quantas linhas são inseridas ao controlar quantas vezes o loop é executado.
* Fornecer o valor inserido na coluna de números inteiros.
* Funcionar como parte da expressão que gera letras a serem inseridas na coluna de caracteres.  

```sql
-- Create the table.
CREATE TABLE TestTable (cola INT, colb CHAR(3));
GO
SET NOCOUNT ON;
GO
-- Declare the variable to be used.
DECLARE @MyCounter INT;

-- Initialize the variable.
SET @MyCounter = 0;

-- Test the variable to see if the loop is finished.
WHILE (@MyCounter < 26)
BEGIN;
   -- Insert a row into the table.
   INSERT INTO TestTable VALUES
       -- Use the variable to provide the integer value
       -- for cola. Also use it to generate a unique letter
       -- for each row. Use the ASCII function to get the
       -- integer value of 'a'. Add @MyCounter. Use CHAR to
       -- convert the sum back to the character @MyCounter
       -- characters after 'a'.
       (@MyCounter,
        CHAR( ( @MyCounter + ASCII('a') ) )
       );
   -- Increment the variable to count this iteration
   -- of the loop.
   SET @MyCounter = @MyCounter + 1;
END;
GO
SET NOCOUNT OFF;
GO
-- View the data.
SELECT cola, colb
FROM TestTable;
GO
DROP TABLE TestTable;
GO
```

## <a name="declaring-a-transact-sql-variable"></a>Declarando uma variável Transact-SQL
A instrução DECLARE inicializa uma variável Transact-SQL por: 
* Atribuição de um nome. O nome deve ter uma única \@ como o primeiro caractere.
* Atribuição de um tipo de dados fornecido por sistema ou definido pelo usuário e um comprimento. Para variáveis numéricas, precisão e escala também são atribuídas. Para variáveis do tipo XML, uma coleção de esquema opcional pode ser atribuída.
* Definição do valor como NULL.

Por exemplo, a instrução **DECLARE** seguinte cria uma variável local nomeada **\@mycounter** com um tipo de dados int.  
```sql
DECLARE @MyCounter INT;
```
Para declarar mais de uma variável local, use uma vírgula depois da primeira variável local definida, e especifique o próximo nome de variável local e o tipo de dados.

Por exemplo, esta instrução **DECLARE** cria três variáveis locais chamadas **\@LastName**, **\@FirstName** e **\@StateProvince**, e inicializa cada uma como NULL:  
```sql
DECLARE @LastName NVARCHAR(30), @FirstName NVARCHAR(20), @StateProvince NCHAR(2);
```

O escopo de uma variável é a gama de instruções Transact-SQL que podem referenciar a variável. O escopo de uma variável dura do ponto em que é declarada até o término do lote ou procedimento armazenado no qual ela é declarada. Por exemplo, o seguinte script gera um erro de sintaxe porque a variável é declarada em um lote e referenciada em outro:  
```sql
USE AdventureWorks2014;
GO
DECLARE @MyVariable INT;
SET @MyVariable = 1;
-- Terminate the batch by using the GO keyword.
GO 
-- @MyVariable has gone out of scope and no longer exists.

-- This SELECT statement generates a syntax error because it is
-- no longer legal to reference @MyVariable.
SELECT BusinessEntityID, NationalIDNumber, JobTitle
FROM HumanResources.Employee
WHERE BusinessEntityID = @MyVariable;
```

As variáveis têm escopo local e são apenas visíveis dentro do lote ou procedimento, onde elas estão definidas. No exemplo a seguir, o escopo aninhado criado para execução de sp_executesql não tem acesso à variável declarada no escopo mais alto e retorna um erro.  

```sql
DECLARE @MyVariable INT;
SET @MyVariable = 1;
EXECUTE sp_executesql N'SELECT @MyVariable'; -- this produces an error
```

## <a name="setting-a-value-in-a-transact-sql-variable"></a>Definindo um valor em uma variável Transact-SQL

Quando uma variável é primeiramente declarada, seu valor é definido como NULL. Para atribuir um valor à uma variável, use a instrução SET. Este é o método preferido de atribuir um valor a uma variável. Uma variável também pode ter um valor atribuído sendo referenciado na lista selecionada de uma instrução SELECT.

Para atribuir um valor a uma variável usando a instrução SET, inclua o nome da variável e o valor a ser atribuído à variável. Este é o método preferido de atribuir um valor a uma variável. O seguinte lote, por exemplo, declara duas variáveis, atribui valores a elas e usa-as na cláusula `WHERE` de uma instrução `SELECT`:  

```sql
USE AdventureWorks2014;
GO
-- Declare two variables.
DECLARE @FirstNameVariable NVARCHAR(50),
   @PostalCodeVariable NVARCHAR(15);

-- Set their values.
SET @FirstNameVariable = N'Amy';
SET @PostalCodeVariable = N'BA5 3HX';

-- Use them in the WHERE clause of a SELECT statement.
SELECT LastName, FirstName, JobTitle, City, StateProvinceName, CountryRegionName
FROM HumanResources.vEmployee
WHERE FirstName = @FirstNameVariable
   OR PostalCode = @PostalCodeVariable;
GO
```

Uma variável também pode ter um valor atribuído ao ser referenciada na lista selecionada. Se uma variável for referenciada em uma lista selecionada, deve ser atribuído um valor escalar ou a instrução SELECT deve retornar só uma linha. Por exemplo:  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable INT;

SELECT @EmpIDVariable = MAX(EmployeeID)
FROM HumanResources.Employee;
GO
```

> [!WARNING]
> Se houver várias cláusulas de atribuições em uma única instrução SELECT, o SQL Server não garante a ordem de avaliação das expressões. Observe que os efeitos são visíveis apenas se houver referências entre as atribuições.

Se uma instrução SELECT retornar mais de uma linha e a variável referenciar uma expressão não escalar, a variável será definida com o valor retornado para a expressão na última linha do conjunto de resultados. Por exemplo, no seguinte lote, **\@EmpIDVariable** é definido com o valor de **BusinessEntityID** da última linha retornada, que é 1:  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable INT;

SELECT @EmpIDVariable = BusinessEntityID
FROM HumanResources.Employee
ORDER BY BusinessEntityID DESC;

SELECT @EmpIDVariable;
GO
```

## <a name="see-also"></a>Consulte Também  
 [Declarar @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
 [SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
 [SELECT @local_variable](../../t-sql/language-elements/select-local-variable-transact-sql.md)  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
  
