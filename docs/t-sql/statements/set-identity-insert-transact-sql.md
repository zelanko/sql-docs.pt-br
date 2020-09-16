---
title: SET IDENTITY_INSERT (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para a instrução SET IDENTITY_INSERT. Quando definido como ON, isso permite inserir valores explícitos na coluna de identidade de uma tabela.
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET IDENTITY_INSERT
- SET_IDENTITY_INSERT_TSQL
- IDENTITY_INSERT_TSQL
- IDENTITY_INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY_INSERT option
- SET IDENTITY_INSERT statement
- identity values [SQL Server], explicit values
- identity columns [SQL Server], explicit values
ms.assetid: a5dd49f2-45c7-44a8-b182-e0a5e5c373ee
author: markingmyname
ms.author: maghan
monkerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 08c8fd59e702d668f7218757021f415b0bea3e39
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544185"
---
# <a name="set-identity_insert-transact-sql"></a>SET IDENTITY_INSERT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Permite inserir valores explícitos na coluna de identidade de uma tabela.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
SET IDENTITY_INSERT [ [ database_name . ] schema_name . ] table_name { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name*  
 É o nome do banco de dados no qual a tabela especificada reside.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela pertence.  
  
 *table_name*  
 É o nome de uma tabela com uma coluna de identidade.  
  
## <a name="remarks"></a>Comentários  
 Em qualquer momento, somente uma tabela em uma sessão pode ter a propriedade IDENTITY_INSERT definida como ON. Se uma tabela já possui essa propriedade definida como ON, e uma instrução SET IDENTITY_INSERT ON for emitida para outra tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro declarando que SET IDENTITY_INSERT já é ON e informará para o que a tabela está definida como ON.  
  
 Se o valor inserido for maior que o valor de identidade atual para a tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará automaticamente o novo valor inserido como valor de identidade atual.  
  
 A configuração de IDENTITY_INSERT é definida na execução ou em tempo de execução, e não em tempo de análise.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ser proprietário da tabela ou ter a permissão ALTER na tabela.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela com uma coluna de identidade e mostra como a configuração `SET IDENTITY_INSERT` pode ser usada para preencher uma lacuna nos valores de identidade causados por uma instrução `DELETE`.  
  
```sql
USE AdventureWorks2012;  
GO  
-- Create tool table.  
CREATE TABLE dbo.Tool(  
   ID INT IDENTITY NOT NULL PRIMARY KEY,   
   Name VARCHAR(40) NOT NULL  
);  
GO  
-- Inserting values into products table.  
INSERT INTO dbo.Tool(Name)   
VALUES ('Screwdriver')  
        , ('Hammer')  
        , ('Saw')  
        , ('Shovel');  
GO  
  
-- Create a gap in the identity values.  
DELETE dbo.Tool  
WHERE Name = 'Saw';  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
  
-- Try to insert an explicit ID value of 3;  
-- should return an error:
-- An explicit value for the identity column in table 'AdventureWorks2012.dbo.Tool' can only be specified when a column list is used and IDENTITY_INSERT is ON.
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
-- SET IDENTITY_INSERT to ON.  
SET IDENTITY_INSERT dbo.Tool ON;  
GO  
  
-- Try to insert an explicit ID value of 3.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
-- Drop products table.  
DROP TABLE dbo.Tool;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
