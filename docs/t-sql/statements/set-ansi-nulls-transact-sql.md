---
title: SET ANSI_NULLS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_ANSI_NULLS_TSQL
- ANSI_NULLS
- SET ANSI_NULLS
- ANSI_NULLS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULLS statement
- not equal to operator (<>)
- ANSI_NULLS option
- equals operator (=)
- null values [SQL Server], comparison operators
- comparison operators [SQL Server], null values
ms.assetid: aae263ef-a3c7-4dae-80c2-cc901e48c755
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 285803fe112cc0370b8af6049f48846c7ba55cab
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="set-ansinulls-transact-sql"></a>SET ANSI_NULLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Especifica o comportamento compatível ISO dos operadores de comparação Igual a (=) e Diferente de (<>) quando usados com valores nulos na [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF gerarão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_NULLS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_NULLS ON;  
```  
  
## <a name="remarks"></a>Comentários  
 Quando SET ANSI_NULLS for ON, uma instrução SELECT que usa WHERE *column_name* = **nulo** retorna zero linhas mesmo que haja valores nulos em *column_name*. Uma instrução SELECT que usa WHERE *column_name* <> **nulo** retorna zero linhas mesmo que haja valores não nulos em *column_name*.  
  
 Quando SET ANSI_NULLS for OFF, os operadores de comparação Igual a (=) e Diferente de (<>) não seguem o padrão ISO. Uma instrução SELECT que usa WHERE *column_name* = **nulo** retorna as linhas com valores nulos em *column_name*. Uma instrução SELECT que usa WHERE *column_name* <> **nulo** retorna as linhas com valores não nulos na coluna. Além disso, uma instrução SELECT que usa WHERE *column_name* <> *XYZ_value* retorna todas as linhas que não são *XYZ_value* e que não são nulos.  
  
 Quando SET ANSI_NULLS for ON, todas as comparações em relação a um valor nulo serão avaliadas como UNKNOWN. Quando SET ANSI_NULLS for OFF, as comparações de todos os dados em relação a um valor nulo serão avaliadas como TRUE. Se SET ANSI_NULLS não for especificado, a configuração da opção ANSI_NULLS do banco de dados atual será aplicada. Para obter mais informações sobre a opção de banco de dados ANSI_NULLS, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET ANSI_NULLS ON afetará uma comparação somente se um dos operandos dessa comparação for uma variável NULL ou um NULL literal. Se os dois lados da comparação forem colunas ou expressões compostas, a configuração não afetará a comparação.  
  
 Para que um script funcione conforme pretendido, independentemente da opção de banco de dados ANSI_NULLS ou da configuração de SET ANSI_NULLS, use IS NULL e IS NOT NULL nas comparações que possam conter valores nulos.  
  
 SET ANSI_NULLS deve ser definido como ON para executar consultas distribuídas.  
  
 SET ANSI_NULLS também deve ser ON quando você estiver criando ou alterando índices em colunas computadas ou exibições indexadas. Se SET ANSI_NULLS estiver OFF, haverá falha em qualquer instrução CREATE, UPDATE, INSERT e DELETE das tabelas com índices em colunas computadas ou exibições indexadas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro que lista todas as opções de SET que violam os valores necessários. Além disso, ao executar uma instrução SELECT, se SET ANSI_NULLS for OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá ignorar os valores de índice nas exibições ou colunas computadas e resolverá a operação selecionada como se não houvessem tais índices nas tabelas ou exibições.  
  
> [!NOTE]  
>  ANSI_NULLS é uma das sete opções SET que devem ser definidas como valores requeridos ao lidar com índices em colunas computadas ou exibições indexadas. As opções ANSI_PADDING, ANSI_WARNINGS, ARITHABORT, QUOTED_IDENTIFIER e CONCAT_NULL_YIELDS_NULL também devem ser definidas como ON, e NUMERIC_ROUNDABORT deve ser definida como OFF.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem automaticamente ANSI_NULLS como ON ao conectar-se. Essa configuração pode ser definida nas fontes de dados ODBC, nos atributos de conexão ODBC ou nas propriedades de conexão OLE DB definidos no aplicativo antes de conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O padrão para SET ANSI_NULLS é OFF.  
  
 Quando SET ANSI_DEFAULTS é ON, SET ANSI_NULLS está habilitado.  
  
 A configuração de ANSI_NULLS é definida durante a execução ou em tempo de execução e não no momento da análise.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @ANSI_NULLS VARCHAR(3) = 'OFF';  
IF ( (32 & @@OPTIONS) = 32 ) SET @ANSI_NULLS = 'ON';  
SELECT @ANSI_NULLS AS ANSI_NULLS;  
  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa os operadores de comparação Igual a (`=`) e Diferente de (`<>`) para fazer comparações com valores `NULL` e não nulos em uma tabela. O exemplo também mostra que `IS NULL` não é afetada pelo `SET ANSI_NULLS` configuração.  
  
```  
-- Create table t1 and insert values.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 values (NULL),(0),(1);  
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
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [= &#40; É igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [IF... OUTRA &#40; Transact-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [&#60; &#62; &#40; Não igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  

