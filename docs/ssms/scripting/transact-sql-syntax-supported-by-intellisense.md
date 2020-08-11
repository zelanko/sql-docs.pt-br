---
title: Sintaxe Transact-SQL com suporte do IntelliSense
description: Saiba quais instruções Transact-SQL e elementos de sintaxe são compatíveis com o IntelliSense do SQL Server Management Studio no SQL Server 2019 (15. x).
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL IntelliSense
- IntelliSense [SQL Server], Transact-SQL syntax
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/16/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 772574d5f50c9c3f9666c56abab80d3ce5181d82
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247336"
---
# <a name="transact-sql-syntax-supported-by-intellisense"></a>Sintaxe Transact-SQL com suporte do IntelliSense
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Este tópico descreve as instruções e os elementos de sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] aos quais o IntelliSense dá suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="statements-supported-by-intellisense"></a>Instruções com suporte do IntelliSense  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o IntelliSense dá suporte apenas às instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] mais usadas. Algumas condições gerais do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem impedir que o IntelliSense funcione. Para obter mais informações, consulte [Solucionando problemas do IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/troubleshooting-intellisense.md).  
  
> [!NOTE]  
>  O IntelliSense não está disponível para objetos de banco de dados criptografados, como, por exemplo, procedimentos armazenados criptografados ou funções definidas pelo usuário. A ajuda de parâmetros e Informações Rápidas não estão disponíveis para os parâmetros de procedimentos armazenados estendidos e tipos definidos pelo usuário da Integração CLR.  
  
### <a name="select-statement"></a>Instrução SELECT  
 O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] dá suporte ao IntelliSense para os seguintes elementos de sintaxe na instrução SELECT:  
  
:::row:::
    :::column:::
        SELECT
    :::column-end:::
    :::column:::
        WHERE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        FROM
    :::column-end:::
    :::column:::
        ORDER BY
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        HAVING
    :::column-end:::
    :::column:::
        UNION
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        FOR
    :::column-end:::
    :::column:::
        GROUP BY
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        INÍCIO
    :::column-end:::
    :::column:::
        OPTION (dica)
    :::column-end:::
:::row-end:::

### <a name="additional-transact-sql-statements-that-are-supported"></a>Instruções Transact-SQL adicionais com suporte  
 O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] também dá suporte ao IntelliSense para instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] mostradas na tabela a seguir.  
  
|Instrução Transact-SQL|Sintaxe com suporte|Exceções|  
|-----------------------------|----------------------|----------------|  
|[INSERT](../../t-sql/statements/insert-transact-sql.md)|Toda a sintaxe, exceto a cláusula *execute_statement* .|Nenhum|  
|[UPDATE](../../t-sql/queries/update-transact-sql.md)|Toda a sintaxe.|Nenhum|  
|[DELETE](../../t-sql/statements/delete-transact-sql.md)|Toda a sintaxe.|Nenhum|  
|[DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)|Toda a sintaxe.|Nenhum|  
|[SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)|Toda a sintaxe.|Nenhum|  
|[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)|Execução de procedimentos armazenados definidos pelo usuário, procedimentos armazenados do sistema, funções definidas pelo usuário e funções do sistema.|Nenhum|  
|[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)|Toda a sintaxe.|Nenhum|  
|[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)|Toda a sintaxe.|Nenhum|  
|[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)|Toda a sintaxe.|Não há suporte do IntelliSense para a cláusula EXTERNAL NAME.<br /><br /> Na cláusula AS, o IntelliSense dá suporte apenas às instruções e à sintaxe listadas neste tópico.|  
|[ALTER PROCEDURE](../../t-sql/statements/alter-procedure-transact-sql.md)|Toda a sintaxe|Não há suporte do IntelliSense para a cláusula EXTERNAL NAME.<br /><br /> Na cláusula AS, o IntelliSense dá suporte apenas às instruções e à sintaxe listadas neste tópico.|  
|[USE](../../t-sql/language-elements/use-transact-sql.md)|Toda a sintaxe.|Nenhum|  
  
## <a name="intellisense-in-supported-statements"></a>IntelliSense em instruções com suporte  
 No Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , o IntelliSense dá suporte aos seguintes elementos de sintaxe, quando usados em uma das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] com suporte:  
  
-   Todos os tipos de junção, inclusive APPLY  
  
-   PIVOT e UNPIVOT  
  
-   Referências aos seguintes objetos de banco de dados:  
  
    -   Bancos de dados e esquemas  
  
    -   Tabelas, exibições, funções com valor de tabela e expressões de tabela  
  
    -   Colunas  
  
    -   Procedimentos e parâmetros de procedimentos  
  
    -   Funções escalares e expressões escalares  
  
    -   Variáveis locais  
  
    -   CTE (expressões de tabela comuns)  
  
-   Objetos de banco de dados referenciados apenas nas instruções CREATE ou ALTER no script ou lote, mas que não existem no banco de dados porque o script ou lote ainda não foi executado. Esses objetos são os seguintes:  
  
    -   Tabelas e procedimentos que foram especificados em uma instrução CREATE TABLE ou CREATE PROCEDURE no script ou lote.  
  
    -   Alterações em tabelas e procedimentos que foram especificadas em uma instrução ALTER TABLE ou ALTER PROCEDURE no script ou lote.  
  
    > [!NOTE]  
    >  O IntelliSense não está disponível para as colunas de uma instrução CREATE VIEW até que a instrução CREATE VIEW tenha sido executada.  
  
 O IntelliSense não é fornecido para os elementos listados anteriormente quando eles são usados em outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por exemplo, há suporte do IntelliSense para nomes de colunas usados em uma instrução SELECT, mas não para colunas usadas na instrução CREATE FUNCTION.  
  
## <a name="examples"></a>Exemplos  
 Em um script ou lote [!INCLUDE[tsql](../../includes/tsql-md.md)] , o IntelliSense no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] dá suporte apenas às instruções e à sintaxe listadas neste tópico. Os exemplos de código [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir mostram as instruções e os elementos de sintaxe com suporte do IntelliSense. Por exemplo, no lote a seguir, o IntelliSense está disponível para a instrução `SELECT` , quando codificada por si só, mas não quando a instrução `SELECT` está contida em uma instrução `CREATE FUNCTION` .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 Essa funcionalidade também se aplica aos conjuntos de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] da cláusula AS de uma instrução CREATE PROCEDURE ou ALTER PROCEDURE.  
  
 Em um script ou lote [!INCLUDE[tsql](../../includes/tsql-md.md)] , o IntelliSense dá suporte a objetos que tenham sido especificados em uma instrução CREATE ou ALTER; no entanto, esses objetos não existem no banco de dados, porque as instruções não foram executadas. Por exemplo, você pode digitar o seguinte código no Editor de Consultas:  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 Após digitar `SELECT`, o IntelliSense listará **PrimaryKeyCol**, **FirstNameCol**e **LastNameCol** como possíveis elementos na lista de seleção, mesmo que o script não tenha sido executado e `MyTable` ainda não exista em `MyTestDB`.  
  
  
