---
title: "Especificar parâmetros | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 029b4f8eab1af6ebbd26c1d8fe877d38420e7f5c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="specify-parameters"></a>Especificar parâmetros
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Ao especificar parâmetros de procedimento, programas de chamada podem passar valores para o corpo do procedimento. Esses valores podem ser usados com vários propósitos durante a execução do procedimento. Parâmetros de procedimento também retornam valores ao programa de chamada quando o parâmetro é marcado como um parâmetro OUTPUT.  
  
 Um procedimento pode ter no máximo 2100 parâmetros; a cada um é atribuído um nome, um tipo de dados e uma direção. Outra opção é atribuir valores padrão aos parâmetros.  
  
 A seção a seguir fornece informações sobre como passar valores para parâmetros e como cada atributo de parâmetro é usado durante uma chamada de procedimento.  
  
## <a name="passing-values-into-parameters"></a>Passando valores para parâmetros  
 Os valores de parâmetros fornecidos com uma chamada de procedimento devem ser constantes ou uma variável; um nome de função não pode ser usado como um valor de parâmetro. As variáveis podem ser definidas pelo usuário ou pelas variáveis de sistema como @@spid.  
  
 Os exemplos a seguir demonstram a passagem de valores de parâmetro para o procedimento `uspGetWhereUsedProductID`. Eles ilustram como passar parâmetros como constantes e variáveis e também como usar uma variável para passar o valor de uma função.  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>Especificando nomes de parâmetro  
 Na criação de um procedimento e declaração de um nome de parâmetro, o nome de parâmetro deve começar com um único caractere @ e deve ser exclusivo no escopo do procedimento.  
  
 A nomeação explícita dos parâmetros e a atribuição dos valores apropriados a cada parâmetro em uma chamada de procedimento permitem o fornecimento dos parâmetros em qualquer ordem. Por exemplo, se o procedimento **my_proc** espera três parâmetros com os nomes **@first**, **@second**e **@third**, os valores passados ao procedimento podem ser atribuídos aos nomes de parâmetros, como: `EXECUTE my_proc @second = 2, @first = 1, @third = 3;`  
  
> [!NOTE]  
>  Se o valor de um parâmetro for fornecido no formato **@parameter =***valor*, forneça todos os parâmetros posteriores dessa maneira. Se os valores dos parâmetros não forem passados no formato **@parameter =***valor*, os valores deverão ser fornecidos na mesma ordem (da esquerda para a direita) em que os parâmetros são listados na instrução CREATE PROCEDURE.  
  
> [!WARNING]  
>  Qualquer parâmetro passado no formato **@parameter =***valor*, com o parâmetro digitado incorretamente, fará com que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gere um erro e impeça a execução do procedimento.  
  
## <a name="specifying-parameter-data-types"></a>Especificando tipos de dados de parâmetros  
 Parâmetros devem ser definidos com um tipo de dados quando são declarados em uma instrução CREATE PROCEDURE. O tipo de dados de um parâmetro determina o tipo e o intervalo dos valores aceitos pelo parâmetro quando o procedimento é chamado. Por exemplo, se você definir um parâmetro com um tipo de dados **tinyint** , somente valores numéricos no intervalo entre 0 e 255 serão aceitos quando passados para esse parâmetro. Um erro será retornado se um procedimento for executado com um valor incompatível com o tipo de dados.  
  
## <a name="specifying-parameter-default-values"></a>Especificando valores padrão de parâmetro  
 Um parâmetro é considerado opcional se o parâmetro tem um valor padrão especificado quando é declarado. Não é necessário fornecer um valor para um parâmetro opcional em uma chamada de procedimento.  
  
 O valor padrão de um parâmetro é usado quando:  
  
-   Nenhum valor é especificado para o parâmetro na chamada do procedimento.  
  
-   A palavra-chave DEFAULT é especificada como o valor na chamada do procedimento.  
  
> [!NOTE]  
>  Se o valor padrão for uma cadeia de caracteres contendo pontuação ou espaços em branco inseridos, ou caso ela comece com um número (por exemplo, 6xxx), ela deverá ser colocada entre aspas simples.  
  
 Se nenhum valor puder ser especificado adequadamente como um padrão para o parâmetro, especifique NULL como o padrão. Convém levar o procedimento a retornar uma mensagem personalizada se ele for executado sem um valor para o parâmetro.  
  
 O exemplo a seguir cria o procedimento armazenado `uspGetSalesYTD` com um parâmetro de entrada, `@SalesPerson`. NULL será atribuído como valor padrão para o parâmetro e será utilizado em instruções de tratamento de erros para retornar uma mensagem de erro personalizada nos casos de execução do procedimento sem um valor para o parâmetro `@SalesPerson` .  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 O exemplo a seguir executa o procedimento. A primeira instrução executa o procedimento sem especificar um valor de entrada. Isso leva as instruções de tratamento de erros no procedimento a retornarem a mensagem de erro personalizada. A segunda instrução fornece um valor de entrada e retorna o conjunto de resultados esperado.  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.uspGetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.uspGetSalesYTD N'Blythe';  
GO  
```  
  
 Embora seja possível omitir os parâmetros para os quais foram fornecidos padrões, a lista de parâmetros só poderá ser truncada. Por exemplo, se um procedimento tiver cinco parâmetros, o quarto e o quinto parâmetros poderão ser omitidos. Entretanto, o quarto parâmetro não pode ser ignorado, desde que o quinto parâmetro seja incluído, a menos que os parâmetros sejam fornecidos no formato **@parameter =***valor*.  
  
## <a name="specifying-parameter-direction"></a>Especificando a direção do parâmetro  
 A direção de um parâmetro é de entrada, em que um valor é passado para o corpo do procedimento armazenado, ou de saída, em que o procedimento retorna um valor ao programa de chamada. O padrão é um parâmetro de entrada.  
  
 Para especificar um parâmetro de saída, especifique a palavra-chave OUTPUT na definição do parâmetro na instrução CREATE PROCEDURE. O procedimento retorna o valor atual do parâmetro de saída ao programa de chamada quando o procedimento existe. O programa de chamada também deve usar a palavra-chave OUTPUT ao executar o procedimento a fim de salvar o valor do parâmetro em uma variável que pode ser usada no programa de chamada.  
  
 O exemplo a seguir cria o procedimento `Production.usp_GetList`, que retorna uma lista de produtos com preços que não excedem uma quantia especificada. O exemplo mostra o uso de várias instruções SELECT e vários parâmetros OUTPUT. Os parâmetros OUTPUT permitem que um procedimento externo, um lote ou mais de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] acessem um valor definido durante a execução do procedimento.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 Execute `usp_GetList` para retornar uma lista de produtos (bicicletas) da [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] que custam menos que $ 700. Os parâmetros OUTPUT **@cost** e **@compareprices** são usados com linguagem de controle de fluxo para retornar uma mensagem na janela **Mensagens** .  
  
> [!NOTE]  
>  A variável OUTPUT deve ser definida durante a criação do procedimento e também durante o uso da variável. O nome de parâmetro e o nome de variável não precisam coincidir. Contudo, o tipo de dados e o posicionamento do parâmetro devem corresponder (a menos que **@listprice=** *variável* seja usado).  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 Este é o conjunto de resultados parcial:  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  
