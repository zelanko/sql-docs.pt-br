---
description: SET ANSI_PADDING (Transact-SQL)
title: SET ANSI_PADDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: be98a76b74f9c4b9882c55de8b18ea045a1be85c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496489"
---
# <a name="set-ansi_padding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Controla como a coluna armazena valores menores que o tamanho definido da coluna e valores com espaços em branco à direita em dados do tipo **char**, **varchar**, **binary**e **varbinary** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe
  
```syntaxsql
-- Syntax for SQL Server

SET ANSI_PADDING { ON | OFF }
```

```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_PADDING ON
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
 Colunas definidas com os tipos de dados **char**, **varchar**, **binary** e **varbinary** têm um tamanho definido.  
  
 Essa configuração afeta somente a definição de novas colunas. Depois que a coluna é criada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena os valores com base na configuração de quando a coluna foi criada. As colunas existentes não são afetadas por uma alteração posterior a essa configuração.  
  
> [!NOTE]  
> ANSI_PADDING sempre deve ser definido como ON.  
  
 A tabela a seguir mostra os efeitos da configuração SET ANSI_PADDING quando valores são inseridos em colunas com os tipos de dados **char**, **varchar**, **binary** e **varbinary**.  
  
|Configuração|char(*n*) NOT NULL ou binary(*n*) NOT NULL|char(*n*) NULL ou binary(*n*) NULL|varchar(*n*) ou varbinary(*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ATIVADO|Valor original de preenchimento (com espaços em branco à direita para colunas **char** e com zeros à direita para colunas **binary**) até o comprimento da coluna.|Siga as mesmas regras de **char(** _n_ **)** ou **binary(** _n_ **)** NOT NULL quando SET ANSI_PADDING for ON.|Os espaços em branco à direita em valores de caractere inseridos em colunas **varchar** não são cortados. Os zeros à direita em valores binários inseridos em colunas **varbinary** não são cortados. Os valores não são preenchidos com o tamanho da coluna.|  
|OFF|Valor original de preenchimento (com espaços em branco à direita para colunas **char** e com zeros à direita para colunas **binary**) até o comprimento da coluna.|Segue as mesmas regras para **varchar** ou **varbinary** quando SET ANSI_PADDING está OFF.|Os espaços em branco à direita em valores de caractere inseridos em uma coluna **varchar** são cortados. Os zeros à direita em valores binários inseridos em uma coluna **varbinary** são cortados.|  
  
> [!NOTE]  
> Quando preenchidas, as colunas **char** são preenchidas com espaços em branco e as colunas **binary** são preenchidas com zeros. Quando cortadas, as colunas **char** têm os espaços em branco à direita cortados e as colunas **binary** têm os zeros à direita cortados.  
  
ANSI_PADDING deve ser ON ao criar ou alterar índices em colunas computadas ou exibições indexadas. Para obter mais informações sobre as configurações da opção SET com exibições indexadas e índices em colunas computadas, consulte "Considerações sobre o uso das instruções SET" em [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
O padrão para SET ANSI_PADDING é ON. O driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC e o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem automaticamente ANSI_PADDING como ON ao conectar. Isso pode ser configurado nas fontes de dados ODBC, nos atributos de conexão ODBC ou nas propriedades de conexão OLE DB definidos no aplicativo antes de conectar. O padrão para SET ANSI_PADDING é OFF para conexões de aplicativos DB-Library.  
  
 A configuração de SET ANSI_PADDING não afeta os tipos de dados **nchar**, **nvarchar**, **ntext**, **text**, **image**, **varbinary(max)**, **varchar(max)** e **nvarchar(max)**. Eles sempre apresentam o comportamento SET ANSI_PADDING ON. Isso significa que os espaços e zeros à direita não são cortados.  
  
Quando ANSI_DEFAULTS é ON, ANSI_PADDING está habilitado.  
  
A configuração de ANSI_PADDING é definida no momento da execução, e não no momento da análise.  
  
Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```sql  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
```  
  
## <a name="permissions"></a>Permissões  
Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra como a configuração afeta cada um desses tipos de dados.  

Defina ANSI_PADDING como ON e teste.

```sql  
PRINT 'Testing with ANSI_PADDING ON'  
SET ANSI_PADDING ON;  
GO  
  
CREATE TABLE t1 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',  
   varbinarycol  
FROM t1;  
GO  
```

Agora defina ANSI_PADDING como OFF e teste.

```sql
PRINT 'Testing with ANSI_PADDING OFF';  
SET ANSI_PADDING OFF;  
GO  
  
CREATE TABLE t2 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',  
   varbinarycol  
FROM t2;  
GO  
  
DROP TABLE t1;  
DROP TABLE t2;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
