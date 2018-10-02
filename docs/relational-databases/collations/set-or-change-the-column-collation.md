---
title: Definir ou alterar o agrupamento de coluna | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bf856f9ae013dd2f19cb72b04c0c2296d0185511
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661904"
---
# <a name="set-or-change-the-column-collation"></a>Definir ou alterar o agrupamento de coluna
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  É possível substituir o agrupamento de banco de dados para dados **char**, **varchar**, **text**, **nchar**, **nvarchar**e **ntext** especificando um agrupamento diferente para uma coluna específica de uma tabela e usando uma das seguintes opções:  
  
-   A cláusula COLLATE de [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) e [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md). Por exemplo:  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Usando a propriedade **Column.Collation** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 Você não pode alterar o agrupamento de uma coluna atualmente referenciada por qualquer um dos seguintes:  
  
-   Uma coluna computada  
  
-   Um índice  
  
-   Estatísticas de distribuição geradas automaticamente ou pela instrução CREATE STATISTICS  
  
-   Uma restrição CHECK  
  
-   Uma restrição FOREIGN KEY  
  
 Ao trabalhar com **tempdb**, a cláusula [COLLATE](~/t-sql/statements/collations.md) inclui uma opção *database_default* para especificar que a coluna em uma tabela temporária usa o agrupamento padrão do banco de dados de usuário atual para a conexão em vez do agrupamento de **tempdb**.  
  
## <a name="collations-and-text-columns"></a>Agrupamentos e colunas de texto  
 Você pode inserir ou atualizar valores em uma coluna **texto** cujo agrupamento seja diferente da página de código do agrupamento padrão do banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte implicitamente os valores para o agrupamento da coluna.  
  
## <a name="collations-and-tempdb"></a>Agrupamentos e tempdb  
 O banco de dados **tempdb** é criado toda vez que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado e tem o mesmo agrupamento padrão que o banco de dados **model** . Normalmente isso é igual ao agrupamento padrão da instância. Se você criar um banco de dados de usuário e especificar um agrupamento padrão diferente do **modelo**, o banco de dados de usuário terá um agrupamento padrão diferente do **tempdb**. Todos os procedimentos armazenados temporários ou tabelas temporárias são criados e armazenados em **tempdb**. Isso significa que todas as colunas implícitas em tabelas temporárias e todas as constantes, variáveis e parâmetros coercíveis padrão em procedimentos armazenados temporários têm agrupamentos diferentes dos objetos comparáveis criados em tabelas e procedimentos armazenados permanentes.  
  
 Isso pode levar a problemas com uma desigualdade em agrupamentos entre bancos de dados definidos pelo usuário e objetos de banco de dados do sistema. Por exemplo, uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o agrupamento Latin1_General_CS_AS e você executa as seguintes instruções:  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 Nesse sistema, o banco de dados **tempdb** usa o agrupamento Latin1_General_CS_AS com a página de código 1252, e `TestDB` e `TestPermTab.Col1` usam o agrupamento `Estonian_CS_AS` com a página de código 1257. Por exemplo:  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 Com o exemplo anterior, o banco de dados **tempdb** usa o agrupamento Latin1_General_CS_AS, `TestDB` e `TestTab.Col1` usam o agrupamento `Estonian_CS_AS` . Por exemplo:  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 Como **tempdb** usa o agrupamento do servidor padrão e `TestPermTab.Col1` usa um agrupamento diferente, o SQL Server retorna este erro: "Não é possível resolver o conflito de agrupamento entre 'Latin1_General_CI_AS_KS_WS' e 'Estonian_CS_AS' igualmente na operação."  
  
 Para evitar o erro, você pode usar uma das seguintes alternativas:  
  
-   Especifique que a coluna da tabela temporária usa o agrupamento padrão do banco de dados de usuário, não **tempdb**. Isso permite que a tabela temporária trabalhe com tabelas formatadas de maneira semelhante em vários bancos de dados, se isso for exigido de seu sistema.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   Especifique o agrupamento correto para a coluna `#TestTempTab` :  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Definir ou alterar o agrupamento do servidor](../../relational-databases/collations/set-or-change-the-server-collation.md)   
 [Definir ou alterar o agrupamento de banco de dados](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
