---
title: Números em sequência | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sequence number object, overview
- sequence [Database Engine]
- autonumbers, sequences
- sequence numbers [SQL Server]
- sequence number object
ms.assetid: c900e30d-2fd3-4d5f-98ee-7832f37e79d1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f56e354023c869fb04d296b63ac748abec763e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126780"
---
# <a name="sequence-numbers"></a>Números de sequência
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Uma sequência é um objeto associado a um esquema definido pelo usuário que gera uma sequência de valores numéricos de acordo com a especificação com a qual a sequência foi criada. A sequência de valores numéricos é gerada em ordem crescente ou decrescente em um intervalo definido e pode seguir um ciclo (repetir-se) conforme solicitado. As sequências, ao contrário das colunas de identidade, não são associadas a tabelas. Um aplicativo se refere a um objeto de sequência para receber seu próximo valor. A relação entre sequências e tabelas é controlada pelo aplicativo. Os aplicativos de usuário podem referenciar um objeto de sequência e coordenar as chaves de valores em várias linhas e tabelas.  
  
 Uma sequência é criada independentemente das tabelas com o uso da instrução **CREATE SEQUENCE** . Opções permitem que você controle o incremento, os valores máximo e mínimo, o ponto de partida, o recurso de reinício automático e o cache para melhorar desempenho. Para obter informações sobre as opções, veja [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 Ao contrário dos valores de coluna de identidade, que são gerados quando as linhas são inseridas, um aplicativo pode obter o próximo número de sequência antes de inserir a linha chamando a função [NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md) . O número de sequência é alocado quando NEXT VALUE FOR é chamado, mesmo quando o número nunca é inserido em uma tabela. A função NEXT VALUE FOR pode ser usada como o valor padrão para uma coluna em uma definição de tabela. Use [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) para obter um intervalo de vários números de sequência de uma só vez.  
  
 Uma sequência pode ser definida como qualquer tipo de dados integer. Se o tipo de dados não for especificado, uma sequência assumirá o padrão **bigint**.  
  
## <a name="using-sequences"></a>Usando sequências  
 Use sequências em vez de colunas de identidade nos seguintes cenários:  
  
-   O aplicativo requer um número antes da inserção na tabela.  
  
-   O aplicativo requer o compartilhamento de uma única série de números entre várias tabelas ou várias colunas dentro de uma tabela.  
  
-   O aplicativo deve reiniciar a série de números quando um número especificado é alcançado. Por exemplo, depois de atribuir valores de 1 a 10, o aplicativo inicia a atribuição de valores de 1 a 10.  
  
-   O aplicativo requer que valores de sequência sejam classificados por outro campo. A função NEXT VALUE FOR pode aplicar a cláusula OVER à chamada de função. A cláusula OVER garante que os valores retornados sejam gerados na ordem da subcláusula ORDER BY da cláusula OVER.  
  
-   Um aplicativo requer que vários números sejam atribuídos ao mesmo tempo. Por exemplo, um aplicativo precisa reservar cinco números sequenciais. A solicitação de valores de identidade poderia resultar em intervalos na série se fossem emitidos números para outros processos simultaneamente. A chamada a sp_sequence_get_range pode recuperar vários números na sequência de uma só vez.  
  
-   Você precisa alterar a especificação da sequência, como o valor de incremento.  
  
## <a name="limitations"></a>Limitações  
 Ao contrário das colunas de identidade, cujos valores não podem ser alterados, os valores de sequência não são protegidos automaticamente após a inserção na tabela. Para impedir a alteração de valores de sequência, use um gatilho de atualização na tabela reverter alterações.  
  
 A exclusividade não é imposta automaticamente para valores de sequência. A capacidade de reutilizar valores de sequência é determinada pelo design. Se os valores de sequência em uma tabela precisarem ser exclusivos, crie um índice exclusivo na coluna. Se os valores de sequência em uma tabela precisarem ser exclusivos em um grupo de tabelas, crie gatilhos para evitar duplicatas causadas por instruções de atualização ou pelo ciclo de números de sequência.  
  
 O objeto de sequência gera números de acordo com sua definição, mas o objeto de sequência não controla como os números são usados. Os números de sequência inseridos em uma tabela podem ter intervalos quando uma transação é revertida, quando um objeto de sequência é compartilhado por várias tabelas ou quando os números de sequência são alocados e não são usados em tabelas. Quando criado com a opção CACHE, um desligamento inesperado, como uma deficiência de energia, pode perder os números de sequência no cache.  
  
 Se houver várias instâncias da função **NEXT VALUE FOR** especificando o mesmo gerador de sequência em uma única instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , todas as instâncias retornarão o mesmo valor para uma determinada linha processada por essa instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esse comportamento é coerente com o padrão ANSI.  
 
 Os números de sequência são gerados fora do escopo da transação atual. Eles serão consumidos se a transação que usa o número de sequência for confirmada ou revertida. A validação duplicada só ocorre quando o registro está totalmente preenchido. Isso pode resultar em alguns casos em que o mesmo número é usado para mais de um registro durante a criação, mas em seguida é identificado como uma duplicata. Se isso ocorrer e outros valores de numeração automática tiverem sido aplicados a registros subsequentes, o resultado poderá ser um intervalo entre os valores de numeração automática.
  
## <a name="typical-use"></a>Usos comum  
 Para criar um número de sequência de inteiros com incrementos de 1 a partir de -2.147,483.648 até 2.147.483.647, use a instrução a seguir.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    INCREMENT BY 1 ;  
```  
  
 Para criar um número de sequência de inteiros semelhante a uma coluna de identidade com incrementos de 1 a partir de 1 até 2.147.483.647, use a instrução a seguir.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
  
```  
  
## <a name="managing-sequences"></a>Gerenciando sequências  
 Para obter informações sobre sequências, consulte [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 Há outros exemplos nos tópicos [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md), [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md) e [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md).  
  
### <a name="a-using-a-sequence-number-in-a-single-table"></a>A. Usando um número de sequência em uma única tabela  
 O exemplo a seguir cria um esquema denominado Test, uma tabela denominada Orders e uma sequência denominada CountBy1 e insere linhas na tabela usando a função NEXT VALUE FOR.  
  
```  
--Create the Test schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Orders  
    (OrderID int PRIMARY KEY,  
    Name varchar(20) NOT NULL,  
    Qty int NOT NULL);  
GO  
  
-- Create a sequence  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
-- Insert three records  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Tire', 2) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Seat', 1) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Brake', 1) ;  
GO  
  
-- View the table  
SELECT * FROM Test.Orders ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `OrderID  Name    Qty`  
  
 `1        Tire    2`  
  
 `2        Seat    1`  
  
 `3        Brake   1`  
  
### <a name="b-calling-next-value-for-before-inserting-a-row"></a>B. Chamando NEXT VALUE FOR antes de inserir uma linha  
 Usando a tabela `Orders` criada no exemplo A, o exemplo a seguir declara uma variável denominada `@nextID`e, em seguida, usa a função NEXT VALUE FOR para definir a variável como o próximo número de sequência disponível. O aplicativo deve fazer algum processamento do pedido, como fornecer ao cliente o número `OrderID` do seu pedido em potencial, e depois validar a ordem. Independentemente de quanto tempo este processamento possa levar, ou de quantas outras ordens sejam adicionadas durante o processo, o número original é preservado para ser usado por esta conexão. Por fim, a instrução `INSERT` adiciona o pedido à tabela `Orders` .  
  
```  
DECLARE @NextID int ;  
SET @NextID = NEXT VALUE FOR Test.CountBy1;  
-- Some work happens  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (@NextID, 'Rim', 2) ;  
GO  
  
```  
  
### <a name="c-using-a-sequence-number-in-multiple-tables"></a>C. Usando um número de sequência em várias tabelas  
 Este exemplo presume que um processo de monitoramento de linha de produção recebe a notificação dos eventos que ocorrem em toda a fábrica. Cada evento recebe um número `EventID` exclusivo e com aumento monotônico. Todos os eventos usam o mesmo número de sequência `EventID` , de forma que os relatórios que combinam todos os eventos possam identificar cada evento de modo exclusivo. Entretanto, os dados do evento são armazenados em três tabelas diferentes, dependendo do tipo de evento. O exemplo de código cria um esquema chamado `Audit`, uma sequência chamada `EventCounter`e três tabelas que usam cada uma a sequência `EventCounter` como valor padrão. Em seguida, o exemplo adiciona linhas às três tabelas e consulta os resultados.  
  
```  
CREATE SCHEMA Audit ;  
GO  
CREATE SEQUENCE Audit.EventCounter  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
CREATE TABLE Audit.ProcessEvents  
(  
    EventID int PRIMARY KEY CLUSTERED   
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EventCode nvarchar(5) NOT NULL,  
    Description nvarchar(300) NULL  
) ;  
GO  
  
CREATE TABLE Audit.ErrorEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NULL,  
    ErrorNumber int NOT NULL,  
    EventDesc nvarchar(256) NULL  
) ;  
GO  
  
CREATE TABLE Audit.StartStopEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NOT NULL,  
    StartOrStop bit NOT NULL  
) ;  
GO  
  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 0) ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (72, 0) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (2735,   
    'Clean room temperature 18 degrees C.') ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (18, 'Spin rate threashold exceeded.') ;  
INSERT Audit.ErrorEvents (EquipmentID, ErrorNumber, EventDesc)   
    VALUES (248, 82, 'Feeder jam') ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 1) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (1841, 'Central feed in bypass mode.') ;  
-- The following statement combines all events, though not all fields.  
SELECT EventID, EventTime, Description FROM Audit.ProcessEvents   
UNION SELECT EventID, EventTime, EventDesc FROM Audit.ErrorEvents   
UNION SELECT EventID, EventTime,   
CASE StartOrStop   
    WHEN 0 THEN 'Start'   
    ELSE 'Stop'  
END   
FROM Audit.StartStopEvents  
ORDER BY EventID ;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `EventID  EventTime                Description`  
  
 `1        2009-11-02 15:00:51.157  Start`  
  
 `2        2009-11-02 15:00:51.160  Start`  
  
 `3        2009-11-02 15:00:51.167  Clean room temperature 18 degrees C.`  
  
 `4        2009-11-02 15:00:51.167  Spin rate threshold exceeded.`  
  
 `5        2009-11-02 15:00:51.173  Feeder jam`  
  
 `6        2009-11-02 15:00:51.177  Stop`  
  
 `7        2009-11-02 15:00:51.180  Central feed in bypass mode.`  
  
### <a name="d-generating-repeating-sequence-numbers-in-a-result-set"></a>D. Gerando números de sequência repetidos em um conjunto de resultados  
 O exemplo a seguir demonstra dois recursos de números de sequência: ciclos e o uso de `NEXT VALUE FOR` em uma instrução select.  
  
```  
CREATE SEQUENCE CountBy5  
   AS tinyint  
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 5  
    CYCLE ;  
GO  
  
SELECT NEXT VALUE FOR CountBy5 AS SurveyGroup, Name FROM sys.objects ;  
GO  
```  
  
### <a name="e-generating-sequence-numbers-for-a-result-set-by-using-the-over-clause"></a>E. Gerando números de sequência para um conjunto de resultados usando a cláusula OVER  
 O exemplo a seguir usa a cláusula `OVER` para classificar o conjunto de resultados por `Name` antes de adicionar a coluna de números de sequência.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Samples ;  
GO  
  
CREATE SEQUENCE Samples.IDLabel  
    AS tinyint  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="f-resetting-the-sequence-number"></a>F. Redefinindo o número de sequência  
 O exemplo E consumiu os primeiros 79 dos números de sequência `Samples.IDLabel`. (Sua versão do `AdventureWorks2012` poderá retornar um número diferente de resultados.) Execute a instrução a seguir para consumir os próximos 79 números de sequência (de 80 a 158).  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
 Execute a instrução a seguir para reiniciar a sequência `Samples.IDLabel`.  
  
```  
ALTER SEQUENCE Samples.IDLabel  
RESTART WITH 1 ;  
```  
  
 Execute a instrução select novamente para verificar se a sequência `Samples.IDLabel` foi reiniciada com o número 1.  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="g-changing-a-table-from-identity-to-sequence"></a>G. Alterando uma tabela de identidade para sequência  
 O exemplo a seguir cria um esquema e tabela contendo três linhas para o exemplo. Em seguida, o exemplo adiciona uma nova coluna e remove a coluna antiga.  
  
```  
-- Create a schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Department  
    (  
        DepartmentID smallint IDENTITY(1,1) NOT NULL,  
        Name nvarchar(100) NOT NULL,  
        GroupName nvarchar(100) NOT NULL  
    CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC)   
    ) ;  
GO  
  
-- Insert three rows into the table  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Engineering', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Tool Design', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Sales', 'Sales and Marketing');  
GO  
  
-- View the table that will be changed  
SELECT * FROM Test.Department ;  
GO  
  
-- End of portion creating a sample table  
--------------------------------------------------------  
-- Add the new column that does not have the IDENTITY property  
ALTER TABLE Test.Department   
    ADD DepartmentIDNew smallint NULL  
GO  
  
-- Copy values from the old column to the new column  
UPDATE Test.Department  
    SET DepartmentIDNew = DepartmentID ;  
GO  
  
-- Drop the primary key constraint on the old column  
ALTER TABLE Test.Department  
    DROP CONSTRAINT [PK_Department_DepartmentID];  
-- Drop the old column  
ALTER TABLE Test.Department  
    DROP COLUMN DepartmentID ;  
GO  
  
-- Rename the new column to the old columns name  
EXEC sp_rename 'Test.Department.DepartmentIDNew',   
    'DepartmentID', 'COLUMN';  
GO  
  
-- Change the new column to NOT NULL  
ALTER TABLE Test.Department  
    ALTER COLUMN DepartmentID smallint NOT NULL ;  
-- Add the unique primary key constraint  
ALTER TABLE Test.Department  
    ADD CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC) ;  
-- Get the highest current value from the DepartmentID column   
-- and create a sequence to use with the column. (Returns 3.)  
SELECT MAX(DepartmentID) FROM Test.Department ;  
-- Use the next desired value (4) as the START WITH VALUE;  
CREATE SEQUENCE Test.DeptSeq  
    AS smallint  
    START WITH 4  
    INCREMENT BY 1 ;  
GO  
  
-- Add a default value for the DepartmentID column  
ALTER TABLE Test.Department  
    ADD CONSTRAINT DefSequence DEFAULT (NEXT VALUE FOR Test.DeptSeq)   
        FOR DepartmentID;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;   
-- Test insert  
INSERT Test.Department (Name, GroupName)  
    VALUES ('Audit', 'Quality Assurance') ;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;  
GO  
  
```  
  
 As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que usam `SELECT *` receberão a nova coluna como a última coluna, e não a primeira. Se isso não for aceitável, você deverá criar uma tabela totalmente nova, mover os dados para ela e recriar as permissões na nova tabela.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)  
  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)  
  
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)  
  
 [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  
