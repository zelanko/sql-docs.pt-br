---
title: Criando uma tabela (tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 04/18/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b7e26428cbe6815331e0e4c3a30e1fb91b8340b7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409705"
---
# <a name="lesson-1-2---creating-a-table"></a>Lição 1–2 – criando uma tabela
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

Para criar uma tabela, você deve fornecer um nome para a tabela e os nomes e tipos de dados de cada coluna na tabela. Também é uma prática recomendada indicar se são permitidos valores nulos em cada coluna. Para criar uma tabela, você deve ter a permissão `CREATE TABLE` , além da permissão `ALTER SCHEMA` no esquema que conterá a tabela. A função de banco de dados fixa `db_ddladmin` tem essas permissões.  
  
A maioria das tabelas tem uma chave primária, composta de uma ou mais colunas da tabela. Uma chave primária sempre é exclusiva. O [!INCLUDE[ssDE](../includes/ssde-md.md)] aplicará a restrição que nenhum valor de chave primária pode ser repetido na tabela.  
  
Para obter uma lista de tipos de dados e links para uma descrição de cada um, consulte [Tipos de dados &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
> O [!INCLUDE[ssDE](../includes/ssde-md.md)] pode ser instalado diferenciando ou não maiúsculas e minúsculas. Se o [!INCLUDE[ssDE](../includes/ssde-md.md)] for instalado diferenciando maiúsculas e minúsculas, os nomes de objeto sempre terão o mesmo tipo (em maiúsculas ou em minúsculas). Por exemplo, uma tabela denominada OrderData é diferente de uma tabela denominada ORDERDATA. Se o [!INCLUDE[ssDE](../includes/ssde-md.md)] estiver instalado como sem distinção entre maiúsculas e minúsculas, esses dois nomes de tabela serão considerados como sendo a mesma tabela, e esse nome poderá ser usado somente uma vez.  
  
### <a name="to-create-a-database-to-contain-the-new-table"></a>Para criar um banco de dados para conter a tabela nova  
  
-   Copie o código a seguir em uma janela Editor de Consulta.  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>Alternar a conexão do Editor de Consulta com o banco de dados TestData  
  
-   Em uma janela do Editor de Consultas, digite e execute o código a seguir para alterar sua conexão com o banco de dados `TestData` .  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### <a name="to-create-a-table"></a>Para criar uma tabela  
  
-   Em uma janela do Editor de Consultas, digite e execute o seguinte código para criar uma tabela simples chamada `Products`. As colunas na tabela são nomeadas `ProductID`, `ProductName`, `Price`e `ProductDescription`. A coluna `ProductID` é a chave primária da tabela. `int`, `varchar(25)`, `money`e `text` são todos tipos de dados. Somente as colunas `Price` e `ProductionDescription` podem não ter dados quando uma linha for inserida ou alterada. Essa instrução contém um elemento opcional (`dbo.`) chamado de um esquema. O esquema é o objeto do banco de dados que possui a tabela. Se você for um administrador, `dbo` será o esquema padrão. `dbo` representa o proprietário do banco de dados.  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Inserindo e atualizando dados em uma tabela &#40;tutorial&#41;](../t-sql/lesson-1-3-inserting-and-updating-data-in-a-table.md)  
  
## <a name="see-also"></a>Consulte Também  
[CREATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/create-table-transact-sql.md)  
  
  
  

