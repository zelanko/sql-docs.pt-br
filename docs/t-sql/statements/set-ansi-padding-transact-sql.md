---
title: SET ANSI_PADDING (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 426cbfe673bafe6e1770745ca16ba23fd068fb67
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Controla como a coluna armazena valores menores que o tamanho definido da coluna e valores com espaços em branco à direita em dados do tipo **char**, **varchar**, **binary**e **varbinary** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_PADDING { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_PADDING ON;  
```  
  
## <a name="remarks"></a>Comentários  
 Colunas definidas com **char**, **varchar**, **binário**, e **varbinary** tipos de dados têm um tamanho definido.  
  
 Essa configuração afeta somente a definição de novas colunas. Depois que a coluna é criada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena os valores com base na configuração de quando a coluna foi criada. As colunas existentes não são afetadas por uma alteração posterior a essa configuração.  
  
> [!NOTE]  
>  Recomenda-se que ANSI_PADDING sempre seja definido como ON.  
  
 A tabela a seguir mostra os efeitos da configuração de SET ANSI_PADDING quando valores forem inseridos em colunas com **char**, **varchar**, **binário**, e  **varbinary** tipos de dados.  
  
|Configuração|char (*n*) não NULL ou binary (*n*) não NULL|char (*n*) NULL ou binary (*n*) nulo|varchar (*n*) ou varbinary (*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|Valor de preenchimento original (com à direita de espaços em branco para **char** colunas e com zeros à direita para **binário** colunas) para o comprimento da coluna.|Segue as mesmas regras para **char (***n***)** ou **binário (**  *n*  **)** NOT NULL quando SET ANSI_PADDING é ON.|À direita de espaços em branco em valores de caractere inseridos em **varchar** colunas não serão cortadas. Zeros à direita nos valores binários inseridos nas **varbinary** colunas não serão cortadas. Os valores não são preenchidos com o tamanho da coluna.|  
|OFF|Valor de preenchimento original (com à direita de espaços em branco para **char** colunas e com zeros à direita para **binário** colunas) para o comprimento da coluna.|Segue as mesmas regras para **varchar** ou **varbinary** quando SET ANSI_PADDING é OFF.|À direita de espaços em branco em valores de caractere inseridos em uma **varchar** coluna serão cortados. Zeros à direita nos valores binários inseridos em uma **varbinary** coluna serão cortados.|  
  
> [!NOTE]  
>  Quando preenchidas, **char** colunas são preenchidas com espaços em branco, e **binário** colunas são preenchidas com zeros. Quando cortadas, **char** colunas têm os espaços em branco à direita cortados, e **binário** colunas têm os zeros à direita cortados.  
  
 SET ANSI_PADDING deve ser ON ao criar ou alterar índices em colunas computadas ou exibições indexadas. Para obter mais informações sobre as configurações de opção SET com exibições indexadas e índices em colunas computadas, consulte "Considerações sobre quando você uso das instruções SET" em [instruções SET &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 O padrão para SET ANSI_PADDING é ON. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem automaticamente ANSI_PADDING como ON ao conectar-se. Isso pode ser configurado nas fontes de dados ODBC, nos atributos de conexão ODBC ou nas propriedades de conexão OLE DB definidos no aplicativo antes de conectar. O padrão para SET ANSI_PADDING é OFF para conexões de aplicativos DB-Library.  
  
 A configuração de SET ANSI_PADDING não afeta o **nchar**, **nvarchar**, **ntext**, **texto**, **imagem**, **varbinary (max)**, **varchar (max)**, e **nvarchar (max)** tipos de dados. Eles sempre apresentam o comportamento SET ANSI_PADDING ON. Isso significa que os espaços e zeros à direita não são cortados.  
  
 Quando SET ANSI_DEFAULTS é ON, SET ANSI_PADDING está habilitado.  
  
 A configuração de SET ANSI_PADDING é definida no momento da execução e não no momento da análise.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como a configuração afeta cada um desses tipos de dados.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  

