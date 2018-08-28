---
title: SET QUOTED_IDENTIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/03/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
caps.latest.revision: 48
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c4f0175980ae6a785b15bc0458c401bf5a1d706
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082969"
---
# <a name="set-quotedidentifier-transact-sql"></a>SET QUOTED_IDENTIFIER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga as regras ISO relativas às aspas que delimitam identificadores e cadeias de caracteres literais. Identificadores delimitados por aspas duplas podem ser palavras-chave reservadas [!INCLUDE[tsql](../../includes/tsql-md.md)] ou podem conter caracteres que nem sempre são permitidos pelas regras da sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET QUOTED_IDENTIFIER { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET QUOTED_IDENTIFIER ON   
```  
  
## <a name="remarks"></a>Remarks  
 Quando SET QUOTED_IDENTIFIER está ON, os identificadores podem ser delimitados por aspas duplas e literais devem ser delimitadas por aspas simples. Quando SET QUOTED_IDENTIFIER está OFF, os identificadores não podem estar entre aspas e devem seguir todas as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md). Literais podem ser delimitados por aspas simples ou duplas.  
  
 Quando SET QUOTED_IDENTIFIER está ON (padrão), todas as cadeias de caracteres delimitadas por aspas duplas são interpretadas como identificadores de objetos. Portanto identificadores entre aspas não precisam seguir as regras [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Elas podem ser palavras-chave reservadas e incluir caracteres geralmente não permitidos nos identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]. Aspas duplas não podem ser usadas para delimitar expressões de cadeias de caracteres literais. Aspas simples devem ser usadas para delimitar cadeias de caracteres literais. Se um sinal de aspas simples (**'**) fizer parte da cadeia de caracteres literal, ele poderá ser representado por duas aspas simples (**''**). SET QUOTED_IDENTIFIER deve estar ON quando palavras-chave reservadas são usadas para nomes de objetos do banco de dados.  
  
 Quando SET QUOTED_IDENTIFIER está OFF, cadeias de caracteres literais em expressões podem ser delimitadas por aspas simples ou duplas. Se uma cadeia de caracteres literal estiver delimitada por aspas duplas, a cadeia de caracteres poderá conter aspas simples inseridas, como apóstrofos.  
  
 SET QUOTED_IDENTIFIER deve estar ON quando você está criando ou alterando índices em colunas computadas ou exibições indexadas. Se SET QUOTED_IDENTIFIER estiver OFF, as instruções CREATE, UPDATE, INSERT e DELETE em tabelas com índices em colunas computadas ou exibições indexadas falharão. Para obter mais informações sobre as configurações da opção SET com exibições indexadas e índices em colunas computadas, consulte "Considerações sobre o uso das instruções SET" em [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 SET QUOTED_IDENTIFIER deverá estar definido como ON quando você estiver criando um índice filtrado.  
  
 SET QUOTED_IDENTIFIER deverá estar definido como ON quando você invocar métodos de tipo de dados XML.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem QUOTED_IDENTIFIER automaticamente como ON durante a conexão. Isso pode ser configurado em fontes de dados ODBC, em atributos de conexão ODBC ou em propriedades de conexão OLE DB. O padrão para SET QUOTED_IDENTIFIER é OFF para conexões de aplicativos DB-Library.  
  
 Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela mesmo que a opção esteja definida como OFF quando a tabela é criada.  
  
 Quando um procedimento armazenado é criado, as configurações SET QUOTED_IDENTIFIER e SET ANSI_NULLS são capturadas e usadas para invocações subsequentes desse procedimento armazenado.  
  
 Quando executada dentro de um procedimento armazenado, a configuração de SET QUOTED_IDENTIFIER não é alterada.  
  
 Quando SET ANSI_DEFAULTS está ON, SET QUOTED_IDENTIFIER está habilitado.  
  
 SET QUOTED_IDENTIFIER também corresponde à configuração QUOTED_IDENTIFIER de ALTER DATABASE. Para obter mais informações sobre as configurações de banco de dados, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET QUOTED_IDENTIFIER entra em vigor no momento da análise e afeta apenas a análise, não a execução da consulta.  
  
 Para um lote ad hoc de nível superior, a análise começa usando a configuração atual da sessão para QUOTED_IDENTIFIER.  Conforme o lote é analisado, qualquer ocorrência de SET QUOTED_IDENTIFIER mudará o comportamento de análise desse ponto em diante e salvará essa configuração para a sessão.  Portanto depois que o lote for analisado e executado, a configuração QUOTED_IDENTIFER da sessão será definida de acordo com a última ocorrência de SET QUOTED_IDENTIFIER no lote.  
 SQL estático em um procedimento armazenado é analisado usando a configuração QUOTED_IDENTIFIER em vigor para o lote que criou ou alterou o procedimento armazenado.  SET QUOTED_IDENTIFIER não tem efeito quando aparece no corpo de um procedimento armazenado como SQL estático.  
  
 Para um lote aninhado usando sp_executesql ou EXEC(), a análise inicia usando a configuração de QUOTED_IDENTIFIER da sessão.  Se o lote aninhado dentro de um procedimento armazenado a análise começará a usar a configuração QUOTED_IDENTIFIER do procedimento armazenado.  Conforme o lote aninhado é analisado, qualquer ocorrência de SET QUOTED_IDENTIFIER mudará o comportamento de análise desse ponto em diante, mas a configuração QUOTED_IDENTIFIER da sessão não será atualizada.  
  
 O uso de colchetes, **[** e **]**, para delimitar identificadores não é afetado pela configuração QUOTED_IDENTIFIER.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';  
IF ( (256 & @@OPTIONS) = 256 ) SET @QUOTED_IDENTIFIER = 'ON';  
SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;  
  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>A. Usando uma configuração de identificador entre aspas e nomes de objetos de palavra reservada  
 O exemplo a seguir mostra que a configuração de `SET QUOTED_IDENTIFIER` deve estar `ON`, e as palavras-chave em nomes de tabelas devem estar entre aspas duplas para criar e usar objetos que têm nomes de palavras-chave reservados.  
  
```  
SET QUOTED_IDENTIFIER OFF  
GO  
-- An attempt to create a table with a reserved keyword as a name  
-- should fail.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Will succeed.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SELECT "identity","order"   
FROM "select"  
ORDER BY "order";  
GO  
  
DROP TABLE "SELECT";  
GO  
  
SET QUOTED_IDENTIFIER OFF;  
GO  
```  
  
### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. Usando uma configuração de identificador entre aspas simples e duplas  
 O exemplo a seguir mostra a maneira como aspas simples e duplas são usadas em expressões de cadeias de caracteres com `SET QUOTED_IDENTIFIER` dedinido como `ON` e `OFF`.  
  
```  
SET QUOTED_IDENTIFIER OFF;  
GO  
USE AdventureWorks2012;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'Test')  
   DROP TABLE dbo.Test;  
GO  
USE AdventureWorks2012;  
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;  
GO  
  
-- Literal strings can be in single or double quotation marks.  
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");  
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');  
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');  
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');  
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");  
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Strings inside double quotation marks are now treated   
-- as object names, so they cannot be used for literals.  
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');  
GO  
  
-- Object identifiers do not have to be in double quotation marks  
-- if they are not reserved keywords.  
SELECT ID, String   
FROM dbo.Test;  
GO  
  
DROP TABLE dbo.Test;  
GO  
  
SET QUOTED_IDENTIFIER OFF;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ID          String 
 ----------- ------------------------------ 
 1           'Text in single quotes' 
 2           'Text in single quotes' 
 3           Text with 2 '' single quotes 
 4           "Text in double quotes" 
 5           "Text in double quotes" 
 6           Text with 2 "" double quotes 
 7           Text with a single ' quote
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)  
  
  
