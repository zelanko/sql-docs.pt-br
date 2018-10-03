---
title: sp_executesql (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_executesql
- sp_executesql_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_executesql
- dynamic SQL
ms.assetid: a8d68d72-0f4d-4ecb-ae86-1235b962f646
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20ddff9570c3d7bd092b9dbd757fb0541234b4af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647054"
---
# <a name="spexecutesql-transact-sql"></a>sp_executesql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma instrução ou lote [!INCLUDE[tsql](../../includes/tsql-md.md)] que pode ser reutilizado muitas vezes ou que foi criado dinamicamente. A instrução ou lote do [!INCLUDE[tsql](../../includes/tsql-md.md)] pode conter parâmetros inseridos.  
  
> [!IMPORTANT]  
>  Executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em tempo de compilação pode expor os aplicativos a ataques maliciosos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_executesql [ @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [ OUT | OUTPUT ][ ,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ \@stmt =] *instrução*  
 É uma cadeia de caracteres Unicode que contém um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote. \@stmt deve ser uma constante Unicode ou uma variável Unicode. Mais expressões Unicode complexas, como concatenar duas cadeias de caracteres com o operador +, não são permitidas. Constantes de caracteres não são permitidas. Se uma constante Unicode for especificada, ele deve ser prefixado com um **N**. Por exemplo, a constante Unicode **n' sp_who'** for válido, mas a constante de caractere **'sp_who'** não é. O tamanho da cadeia de caracteres é limitado apenas pela memória disponível do servidor de banco de dados. Em servidores de 64 bits, o tamanho da cadeia de caracteres é limitado a 2 GB, o tamanho máximo de **nvarchar (max)**.  
  
> [!NOTE]  
>  \@stmt pode conter parâmetros com a mesma forma que um nome de variável, por exemplo: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Cada parâmetro incluído em \@stmt deve ter uma entrada correspondente em ambos os \@lista de valores de lista de definições de parâmetro params e o parâmetro.  
  
 [ \@params =] N'\@*parameter_name * * data_type* [,... *n* ] '  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros que foram inseridos em \@stmt. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. *n* é um espaço reservado que indica definições de parâmetro adicionais. Todo parâmetro especificado em \@stmtmust ser definido em \@params. Se o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote na \@stmt não contiverem parâmetros, \@params não é necessária. O valor padrão para este parâmetro é NULL.  
  
 [ \@param1 =] '*value1*'  
 É um valor para o primeiro parâmetro definido na cadeia de caracteres de parâmetro. O valor pode ser uma constante Unicode ou uma variável Unicode. Deve haver um valor de parâmetro fornecido para cada parâmetro incluído em \@stmt. Os valores não são necessários quando o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote em \@stmt não tem nenhum parâmetro.  
  
 [ OUT | OUTPUT ]  
 Indica que o parâmetro é um parâmetro de saída. **texto**, **ntext**, e **imagem** parâmetros podem ser usados como parâmetros de saída, a menos que o procedimento é um procedimento do common language runtime (CLR). Um parâmetro de saída que usa a palavra-chave OUTPUT pode ser um espaço reservado de cursor, a menos que o procedimento seja CLR.  
  
 *n*  
 É um espaço reservado aos valores de parâmetros adicionais. Os valores só podem ser constantes ou variáveis. Os valores não podem ser expressões mais complexas, como funções ou expressões construídas usando os operadores.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou não zero (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna os conjuntos de resultados de todas as instruções SQL construídas na cadeia de caracteres SQL.  
  
## <a name="remarks"></a>Comentários  
 parâmetros de sp_executesql devem ser inseridos na ordem específica, conforme descrito na seção "Sintaxe" neste tópico. Se os parâmetros forem inseridos na ordem incorreta, uma mensagem de erro será exibida.  
  
 sp_executesql tem o mesmo comportamento que EXECUTE em relação a lotes, ao escopo de nomes e ao contexto de banco de dados. O [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote em sp_executesql \@stmt parâmetro não é compilado até que a instrução sp_executesql seja executada. O conteúdo de \@stmt são então compilados e executados como um plano de execução separado do plano de execução de lote que chamou sp_executesql. O lote sp_executesql não pode referenciar variáveis declaradas no lote que chama sp_executesql. Cursores locais ou variáveis no lote de sp_executesql não são visíveis para o lote que chama sp_executesql. As alterações no contexto de banco de dados duram apenas até o fim da instrução sp_executesql.  
  
 sp_executesql poderá ser usado no lugar de procedimentos armazenados para executar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] muitas vezes quando a alteração nos valores de parâmetro para a instrução for a única variação. Como a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] em si permanece constante e somente os valores de parâmetro são alterados, é provável que o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reutilize o plano de execução gerado para a primeira execução.  
  
> [!NOTE]  
>  Para melhorar o desempenho, use nomes de objeto totalmente qualificados na cadeia de caracteres de instrução.  
  
 sp_executesql oferece suporte à configuração de valores de parâmetro separadamente da cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)], conforme mostrado no exemplo a seguir.  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
  
/* Build the SQL string one time.*/  
SET @SQLString =  
     N'SELECT BusinessEntityID, NationalIDNumber, JobTitle, LoginID  
       FROM AdventureWorks2012.HumanResources.Employee   
       WHERE BusinessEntityID = @BusinessEntityID';  
SET @ParmDefinition = N'@BusinessEntityID tinyint';  
/* Execute the string with the first parameter value. */  
SET @IntVariable = 197;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
/* Execute the same string with the second parameter value. */  
SET @IntVariable = 109;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
```  
  
 Parâmetros de saída também podem ser usados com sp_executesql. O exemplo a seguir recupera um cargo da tabela `AdventureWorks2012.HumanResources.Employee` e o retorna no parâmetro de saída `@max_title`.  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @max_title varchar(30);  
  
SET @IntVariable = 197;  
SET @SQLString = N'SELECT @max_titleOUT = max(JobTitle)   
   FROM AdventureWorks2012.HumanResources.Employee  
   WHERE BusinessEntityID = @level';  
SET @ParmDefinition = N'@level tinyint, @max_titleOUT varchar(30) OUTPUT';  
  
EXECUTE sp_executesql @SQLString, @ParmDefinition, @level = @IntVariable, @max_titleOUT=@max_title OUTPUT;  
SELECT @max_title;  
```  
  
 A capacidade de substituir parâmetros em sp_executesql oferece as vantagens a seguir usando a instrução EXECUTE para executar uma cadeia de caracteres:  
  
-   Como o texto real da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] na cadeia de caracteres sp_executesql não é alterado entre as execuções, o otimizador de consulta provavelmente fará a correspondência da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] na segunda execução com o plano de execução gerado para a primeira execução. Portanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não precisa compilar a segunda instrução.  
  
-   A cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)] é criada apenas uma vez.  
  
-   O parâmetro numérico inteiro é especificado em seu formato nativo. A conversão para Unicode não é necessária.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-executing-a-simple-select-statement"></a>A. Executando uma instrução SELECT simples  
 O exemplo a seguir cria e executa uma instrução `SELECT` simples que contém um parâmetro inserido chamado `@level`.  
  
```  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
          WHERE BusinessEntityID = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
### <a name="b-executing-a-dynamically-built-string"></a>B. Executando uma cadeia de caracteres dinamicamente construída  
 O exemplo a seguir mostra o uso de `sp_executesql` para executar uma cadeia de caracteres dinamicamente construída. O exemplo de procedimento armazenado é usado para inserir dados em um conjunto de tabelas que são usadas para particionar dados de vendas em um ano. Há uma tabela para cada mês do ano com o seguinte formato:  
  
```  
CREATE TABLE May1998Sales  
    (OrderID int PRIMARY KEY,  
    CustomerID int NOT NULL,  
    OrderDate  datetime NULL  
        CHECK (DATEPART(yy, OrderDate) = 1998),  
    OrderMonth int  
        CHECK (OrderMonth = 5),  
    DeliveryDate datetime  NULL,  
        CHECK (DATEPART(mm, OrderDate) = OrderMonth)  
    )  
```  
  
 Este procedimento armazenado de amostra constrói e executa dinamicamente uma instrução `INSERT` para inserir novas ordens na tabela correta. O exemplo usa a data do pedido para criar o nome da tabela que deve conter os dados e, em seguida, incorpora o nome em uma instrução `INSERT`.  
  
> [!NOTE]  
>  Este é um exemplo simples para sp_executesql. O exemplo não contém verificação de erros e não inclui verificações para regras de negócios, como garantir que os números do pedido não sejam duplicados nas tabelas.  
  
```  
CREATE PROCEDURE InsertSales @PrmOrderID INT, @PrmCustomerID INT,  
                 @PrmOrderDate DATETIME, @PrmDeliveryDate DATETIME  
AS  
DECLARE @InsertString NVARCHAR(500)  
DECLARE @OrderMonth INT  
  
-- Build the INSERT statement.  
SET @InsertString = 'INSERT INTO ' +  
       /* Build the name of the table. */  
       SUBSTRING( DATENAME(mm, @PrmOrderDate), 1, 3) +  
       CAST(DATEPART(yy, @PrmOrderDate) AS CHAR(4) ) +  
       'Sales' +  
       /* Build a VALUES clause. */  
       ' VALUES (@InsOrderID, @InsCustID, @InsOrdDate,' +  
       ' @InsOrdMonth, @InsDelDate)'  
  
/* Set the value to use for the order month because  
   functions are not allowed in the sp_executesql parameter  
   list. */  
SET @OrderMonth = DATEPART(mm, @PrmOrderDate)  
  
EXEC sp_executesql @InsertString,  
     N'@InsOrderID INT, @InsCustID INT, @InsOrdDate DATETIME,  
       @InsOrdMonth INT, @InsDelDate DATETIME',  
     @PrmOrderID, @PrmCustomerID, @PrmOrderDate,  
     @OrderMonth, @PrmDeliveryDate  
  
GO  
```  
  
 Usar sp_executesql neste procedimento é mais eficiente que usar EXECUTE para executar uma cadeia de caracteres. Quando sp_executesql é usado, há somente 12 versões da cadeia de caracteres INSERT que são geradas, uma para cada tabela mensal. Com EXECUTE, cada cadeia de caracteres INSERT é exclusiva porque os valores de parâmetro são diferentes. Embora os dois métodos gerem o mesmo número de lotes, a similaridade das cadeias de caracteres INSERT geradas por sp_executesql torna mais provável que o otimizador de consultas reutilize os planos de execução.  
  
### <a name="c-using-the-output-parameter"></a>C. Usando o parâmetro OUTPUT  
 O exemplo a seguir usa uma `OUTPUT` parâmetro para armazenar o conjunto de resultados gerado pela `SELECT` instrução no `@SQLString` parâmetro. Duas `SELECT` instruções são executadas que usam o valor da `OUTPUT` parâmetro.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @SalesOrderNumber nvarchar(25);  
DECLARE @IntVariable int;  
SET @SQLString = N'SELECT @SalesOrderOUT = MAX(SalesOrderNumber)  
    FROM Sales.SalesOrderHeader  
    WHERE CustomerID = @CustomerID';  
SET @ParmDefinition = N'@CustomerID int,  
    @SalesOrderOUT nvarchar(25) OUTPUT';  
SET @IntVariable = 22276;  
EXECUTE sp_executesql  
    @SQLString  
    ,@ParmDefinition  
    ,@CustomerID = @IntVariable  
    ,@SalesOrderOUT = @SalesOrderNumber OUTPUT;  
-- This SELECT statement returns the value of the OUTPUT parameter.  
SELECT @SalesOrderNumber;  
-- This SELECT statement uses the value of the OUTPUT parameter in  
-- the WHERE clause.  
SELECT OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderNumber = @SalesOrderNumber;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-executing-a-simple-select-statement"></a>D. Executando uma instrução SELECT simples  
 O exemplo a seguir cria e executa uma instrução `SELECT` simples que contém um parâmetro inserido chamado `@level`.  
  
```  
-- Uses AdventureWorks  
  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorksPDW2012.dbo.DimEmployee   
          WHERE EmployeeKey = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
 Para obter exemplos adicionais, consulte [sp_executesql (Transact-SQL)](http://msdn.microsoft.com/library/ms188001.aspx).  
  
## <a name="see-also"></a>Consulte também  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
