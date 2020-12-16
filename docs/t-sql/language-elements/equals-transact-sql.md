---
description: = (É igual a) (Transact-SQL)
title: = (Equals) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- =
- = (Equals)
- Equals
- =_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 18885245-5f55-4831-8f0b-7f2a3e82e246
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4027e2dedb8c5417172d6c7507600549a3dc8252
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484018"
---
# <a name="-equals-transact-sql"></a>= (É igual a) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Compara a igualdade de duas expressões (um operador de comparação) na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
expression = expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida. Se as expressões não são do mesmo tipo de dados, o tipo de dados para uma expressão deve ser implicitamente conversível para o tipo de dados da outra expressão. A conversão é baseada nas regras de [precedência de tipo de dados](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Booliano  
  
## <a name="remarks"></a>Comentários  
 Quando você compara usando uma expressão NULL, o resultado depende da configuração `ANSI_NULLS`:  
  
-   Se `ANSI_NULLS` for definido como ativado, o resultado de qualquer comparação com NULL será UNKNOWN, seguindo a convenção ANSI que NULL é um valor desconhecido e não pode ser comparado com nenhum outro valor, incluindo outros NULLs.  
  
-   Se `ANSI_NULLS` for definido como desativado, o resultado da comparação de NULL com NULL será TRUE, e o resultado da comparação de NULL com qualquer outro valor será FALSE.  

Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).
  
 Uma expressão booliana que resulta em UNKNOWN comporta-se de maneira semelhante a FALSE na maioria dos casos, mas não em todos. Consulte [NULL e UNKNOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/null-and-unknown-transact-sql.md) e [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md) para obter mais informações.  
  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using--in-a-simple-query"></a>a. Usando = em uma consulta simples  
 O exemplo a seguir usa o operador Igual a para retornar todas as linhas da tabela `HumanResources.Department` em que o valor na coluna `GroupName` é igual à palavra 'produção'.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE GroupName = 'Manufacturing';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
DepartmentID Name  
------------ --------------------------------------------------  
7            Production  
8            Production Control  
  
(2 row(s) affected)  
  
```  
  
### <a name="b-comparing-null-and-non-null-values"></a>B. Comparando valores NULL e não NULL  
 O exemplo a seguir usa os operadores de comparação Igual a (`=`) e Diferente de (`<>`) para fazer comparações com valores `NULL` e não nulos em uma tabela. O exemplo também mostra que `IS NULL` não é afetado pela configuração de `SET ANSI_NULLS`.  
  
```sql  
-- Create table t1 and insert 3 rows.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 VALUES (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Testing default setting  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
a  
-----------  
0  
1  
  
(2 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
Testing ANSI_NULLS ON  
a  
-----------  
  
(0 row(s) affected)  
  
a  
-----------  
  
(0 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
Testing SET ANSI_NULLS OFF  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
a  
-----------  
0  
1  
  
(2 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
