---
description: Definir ou alterar a ordenação de coluna
title: Definir ou alterar a ordenação de coluna | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f408175a59484aa162c0db654ebf4b1d5656901
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460579"
---
# <a name="set-or-change-the-column-collation"></a>Definir ou alterar a ordenação de coluna
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  É possível substituir a ordenação de banco de dados para dados **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext** especificando uma ordenação diferente para uma coluna específica de uma tabela e usando uma das seguintes opções:  
  
-   A cláusula COLLATE de [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) e [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md), como visto nos exemplos abaixo. 

    -   **Conversão in-loco.** Considere uma das tabelas existentes definidas abaixo:

        ```sql
        -- NVARCHAR column is encoded in UTF-16 because a supplementary character enabled collation is used
        CREATE TABLE dbo.MyTable (CharCol NVARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC);

        -- VARCHAR column is encoded the Latin code page and therefore is not Unicode capable
        CREATE TABLE dbo.MyTable (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI);
        ```

        Para converter a coluna in-loco para usar UTF-8, execute uma instrução `ALTER COLUMN` que define o tipo de dados necessário e uma ordenação habilitada para UTF-8:

        ```sql 
        ALTER TABLE dbo.MyTable 
        ALTER COLUMN CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8
        ```

        Esse método é fácil de implementar, mas é uma operação que possivelmente causa bloqueio e pode se tornar um problema para tabelas grandes e aplicativos ocupados.

    -   **Copiar e substituir.** Considere uma das tabelas existentes definidas abaixo:

        ```sql
        -- NVARCHAR column is encoded in UTF-16 because a supplementary character enabled collation is used
        CREATE TABLE dbo.MyTable (CharCol NVARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC);
        GO

        -- VARCHAR column is encoded using the Latin code page and therefore is not Unicode capable
        CREATE TABLE dbo.MyTable (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI);
        GO
        ```

        Para converter a coluna para usar UTF-8, copie os dados para uma nova tabela na qual a coluna alvo já é o tipo de dados necessário e uma ordenação habilitada para UTF-8, então substitua a tabela antiga:

        ```sql
        CREATE TABLE dbo.MyTableNew (CharCol VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8);
        GO
        INSERT INTO dbo.MyTableNew 
        SELECT * FROM dbo.MyTable;
        GO
        DROP TABLE dbo.MyTable;
        GO
        EXEC sp_rename 'dbo.MyTableNew', 'dbo.MyTable';
        GO
        ```

        Esse método é muito mais rápido do que a conversão in-loco, mas a manipulação de esquemas complexos com muitas dependências (FKs, PKs, gatilhos, DFs) e a sincronização da parte final da tabela (se o banco de dados estiver em uso) exigem mais planejamento.
        
    Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, confira [Modificar colunas (Mecanismo de Banco de Dados)](../../relational-databases/tables/modify-columns-database-engine.md#SSMSProcedure).  
  
-   Usando a propriedade **Column.Collation** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 Você não pode alterar a ordenação de uma coluna atualmente referenciada por qualquer um dos seguintes:  
  
-   Uma coluna computada  
-   Um índice  
-   Estatísticas de distribuição geradas automaticamente ou pela instrução `CREATE STATISTICS`  
-   Uma restrição CHECK  
-   Uma restrição FOREIGN KEY  
  
 Ao trabalhar com **tempdb**, a cláusula [COLLATE](~/t-sql/statements/collations.md) inclui uma opção *database_default* para especificar que a coluna em uma tabela temporária usa a ordenação padrão do banco de dados de usuário atual para a conexão em vez da ordenação de **tempdb**.  
  
## <a name="collations-and-text-columns"></a>Ordenações e colunas de texto  
 Você pode inserir ou atualizar valores em uma coluna **texto** cuja ordenação seja diferente da página de código da ordenação padrão do banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte implicitamente os valores para a ordenação da coluna.  
  
## <a name="collations-and-tempdb"></a>Ordenações e tempdb  
 O banco de dados **tempdb** é criado toda vez que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado e tem a mesma ordenação padrão que o banco de dados **model**. Normalmente isso é igual à ordenação padrão da instância. Se você criar um banco de dados de usuário e especificar uma ordenação padrão diferente do **modelo**, o banco de dados de usuário terá uma ordenação padrão diferente do **tempdb**. Todos os procedimentos armazenados temporários ou tabelas temporárias são criados e armazenados em **tempdb**. Isso significa que todas as colunas implícitas em tabelas temporárias e todas as constantes, variáveis e parâmetros coercíveis padrão em procedimentos armazenados temporários têm ordenações diferentes dos objetos comparáveis criados em tabelas e procedimentos armazenados permanentes.  
  
 Isso pode levar a problemas com uma desigualdade em ordenações entre bancos de dados definidos pelo usuário e objetos de banco de dados do sistema. Por exemplo, uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a ordenação Latin1_General_CS_AS e você executa as seguintes instruções:  
  
```sql  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 Nesse sistema, o banco de dados **tempdb** usa a ordenação Latin1_General_CS_AS com a página de código 1252, e `TestDB` e `TestPermTab.Col1` usam a ordenação `Estonian_CS_AS` com a página de código 1257. Por exemplo:  
  
```sql  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 Com o exemplo anterior, o banco de dados **tempdb** usa a ordenação Latin1_General_CS_AS, `TestDB` e `TestTab.Col1` usam a ordenação `Estonian_CS_AS`. Por exemplo:  
  
```sql  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 Como **tempdb** usa a ordenação do servidor padrão e `TestPermTab.Col1` usa uma ordenação diferente, o SQL Server retorna este erro: "Não é possível resolver o conflito de ordenação entre 'Latin1_General_CI_AS_KS_WS' e 'Estonian_CS_AS' igualmente na operação".  
  
 Para evitar o erro, você pode usar uma das seguintes alternativas:  
  
-   Especifique que a coluna da tabela temporária usa a ordenação padrão do banco de dados de usuário, não **tempdb**. Isso permite que a tabela temporária trabalhe com tabelas formatadas de maneira semelhante em vários bancos de dados, se isso for exigido de seu sistema.  
  
    ```sql  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   Especifique a ordenação correta para a coluna `#TestTempTab`:  
  
    ```sql  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Definir ou alterar a ordenação do servidor](../../relational-databases/collations/set-or-change-the-server-collation.md)   
 [Definir ou alterar a ordenação de banco de dados](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
