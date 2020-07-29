---
title: 'Tutorial do T-SQL: criar e consultar objetos de banco de dados | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 9fb8656b-0e4e-4ada-b404-4db4d3eea995
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a8691ed6a84fce3eb12c8e13b2235356486c42f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248694"
---
# <a name="lesson-1-create-and-query-database-objects"></a>Lição 1: criar e consultar objetos de banco de dados
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

Esta lição mostra como criar um banco de dados, criar uma tabela no banco de dados e, então, acessar e alterar os dados na tabela. Como esta lição é uma introdução ao uso de [!INCLUDE[tsql](../includes/tsql-md.md)], ela não usa nem descreve as várias opções disponíveis para essas instruções.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] As instruções podem ser escritas e enviadas ao [!INCLUDE[ssDE](../includes/ssde-md.md)] das seguintes maneiras:  
  
-   Usando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Este tutorial pressupõe que você esteja usando o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], mas também é possível usar o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Express, que está disponível como um download gratuito no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=14630).  
  
-   Usando o [utilitário sqlcmd](../tools/sqlcmd-utility.md).  
  
-   Conectando de um aplicativo criado por você.  
  
O código é executado da mesma maneira no [!INCLUDE[ssDE](../includes/ssde-md.md)] e com as mesmas permissões, independentemente de como você envia as instruções de código.  
  
Para executar [!INCLUDE[tsql](../includes/tsql-md.md)] instruções no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], abra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e conecte-se a uma instância de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  

## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, você precisa de acesso ao SQL Server Management Studio e a uma instância do SQL Server. 

- Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Se você não tiver uma instância de SQL Server, crie uma. Para criar uma, selecione a plataforma nos links a seguir. Se você escolher Autenticação do SQL, use suas credenciais de logon do SQL Server.
- **Windows**: [baixe o SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [baixe o SQL Server 2017 no Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="create-a-database"></a>Criar um banco de dados
Como muitas instruções [!INCLUDE[tsql](../includes/tsql-md.md)], a instrução [`CREATE DATABASE`](statements/create-database-transact-sql.md) tem um parâmetro obrigatório: o nome do banco de dados.` CREATE DATABASE` também tem muitos parâmetros opcionais, como o local de disco onde você deseja armazenar os arquivos de banco de dados. Quando você executa `CREATE DATABASE` sem os parâmetros opcionais, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa valores padrão para muitos destes parâmetros.

1.  Em uma janela do Editor de Consultas, digite, mas não execute o seguinte código:  
  
    ```sql  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  Use o ponteiro para selecionar as palavras `CREATE DATABASE`e, em seguida, pressione **F1**. O tópico `CREATE DATABASE` em Manuais Online do SQL Server deverá ser aberto. Você pode usar esta técnica para localizar a sintaxe completa de `CREATE DATABASE` e para as outras instruções que são usadas neste tutorial.  
  
3.  No Editor de Consultas, pressione **F5** para executar a instrução e criar um banco de dados denominado `TestData`.  
  
Ao criar um banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] faz uma cópia do banco de dados **modelo** e renomeia a cópia para o nome do banco de dados. Esta operação deve levar somente alguns segundos, a menos que você especifique um tamanho inicial grande do banco de dados como um parâmetro opcional.  
  
> [!NOTE]  
> A palavra-chave GO separa instruções quando mais de uma instrução é enviada em um único lote. GO é opcional quando o lote contém somente uma instrução.  

## <a name="create-a-table"></a>Criar uma tabela

[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

Para criar uma tabela, você deve fornecer um nome para a tabela e os nomes e tipos de dados de cada coluna na tabela. Também é uma prática recomendada indicar se são permitidos valores nulos em cada coluna. Para criar uma tabela, você deve ter a permissão `CREATE TABLE` , além da permissão `ALTER SCHEMA` no esquema que conterá a tabela. A função de banco de dados fixa [`db_ddladmin`](../relational-databases/security/authentication-access/database-level-roles.md) tem essas permissões.  
  
A maioria das tabelas tem uma chave primária, composta de uma ou mais colunas da tabela. Uma chave primária sempre é exclusiva. O [!INCLUDE[ssDE](../includes/ssde-md.md)] aplicará a restrição que nenhum valor de chave primária pode ser repetido na tabela.  
  
Para obter uma lista de tipos de dados e links para uma descrição de cada um, consulte [Tipos de dados &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
> O [!INCLUDE[ssDE](../includes/ssde-md.md)] pode ser instalado diferenciando ou não maiúsculas e minúsculas. Se o [!INCLUDE[ssDE](../includes/ssde-md.md)] for instalado diferenciando maiúsculas e minúsculas, os nomes de objeto sempre terão o mesmo tipo (em maiúsculas ou em minúsculas). Por exemplo, uma tabela denominada OrderData é diferente de uma tabela denominada ORDERDATA. Se o [!INCLUDE[ssDE](../includes/ssde-md.md)] estiver instalado como sem distinção entre maiúsculas e minúsculas, esses dois nomes de tabela serão considerados como sendo a mesma tabela, e esse nome poderá ser usado somente uma vez.  
  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>Alternar a conexão do Editor de Consulta com o banco de dados TestData  

Em uma janela do Editor de Consultas, digite e execute o código a seguir para alterar sua conexão com o banco de dados `TestData` .  
  
  ```sql  
  USE TestData  
  GO  
  ```  
  
### <a name="create-the-table"></a>Criar a tabela

Em uma janela do Editor de Consultas, digite e execute o seguinte código para criar uma tabela chamada `Products`. As colunas na tabela são nomeadas `ProductID`, `ProductName`, `Price`e `ProductDescription`. A coluna `ProductID` é a chave primária da tabela. `int`, `varchar(25)`, `money`e `varchar(max)` são todos tipos de dados. Somente as colunas `Price` e `ProductionDescription` podem não ter dados quando uma linha for inserida ou alterada. Essa instrução contém um elemento opcional (`dbo.`) chamado de um esquema. O esquema é o objeto do banco de dados que possui a tabela. Se você for um administrador, `dbo` será o esquema padrão. `dbo` representa o proprietário do banco de dados.  
  
  ```sql  
  CREATE TABLE dbo.Products  
     (ProductID int PRIMARY KEY NOT NULL,  
     ProductName varchar(25) NOT NULL,  
     Price money NULL,  
     ProductDescription varchar(max) NULL)  
  GO  
 ```  

## <a name="insert-and-update-data-in-a-table"></a>Inserir e atualizar dados em uma tabela
Agora que você criou a tabela **Products** , está pronto para inserir dados na tabela usando a instrução INSERT. Depois que os dados forem inseridos, você alterará o conteúdo de uma linha usando uma instrução UPDATE. Você usará a cláusula WHERE da instrução UPDATE para restringir a atualização a uma única linha. As quatro instruções inserem os dados a seguir.  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3,17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|Colchete de 3 mm|0.52||  
  
A sintaxe básica é: INSERT, nome da tabela, lista de colunas, VALUES e uma lista de valores a serem inseridos. Os dois hifens antes de uma linha indicam que a linha é um comentário e o texto será ignorado pelo compilador. Neste caso, o comentário descreve uma variação admissível da sintaxe.  
  
### <a name="insert-data-into-a-table"></a>Inserir dados em uma tabela  
  
1.  Execute a instrução a seguir para inserir uma linha na tabela `Products` que foi criada na tarefa anterior.
  
   ```sql 
   -- Standard syntax  
   INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
       VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
   GO   
   ```  

   > [!NOTE]
   > Se a inserção tiver sucesso, vá para a próxima etapa.
   >
   > Se a inserção falhar, talvez a tabela de `Product` já tenha uma linha com essa ID de produto. Para continuar, exclua todas as linhas na tabela e repita a etapa anterior. [`TRUNCATE TABLE`](statements/truncate-table-transact-sql.md) exclui todas as linhas na tabela. 
   >
   > Execute o seguinte comando para excluir todas as linhas na tabela:
   > 
   > ```sql
   >TRUNCATE TABLE TestData.dbo.Products;
   > GO
   >```
   >
   > Depois de truncar a tabela, repita o comando `INSERT` nesta etapa.

2.  A instrução a seguir mostra como você pode alterar a ordem na qual os parâmetros são fornecidos alternando o posicionamento de `ProductID` e `ProductName` na lista de campos (entre parênteses) e na lista de valores.  
  
   ```sql  
   -- Changing the order of the columns  
   INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
       VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
   GO    
   ```  
  
3.  A instrução a seguir demonstra que os nomes das colunas são opcionais, desde que os valores estejam listados na ordem correta. Esta sintaxe é comum, mas não é recomendada, pois possivelmente outras usuários terão dificuldade para compreender o código. `NULL` é especificado para a coluna `Price` porque o preço desse produto ainda não é conhecido.  
  
   ```sql  
   -- Skipping the column list, but keeping the values in order  
   INSERT dbo.Products  
       VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
   GO  
  ```  
  
4.  O nome de esquema é opcional, desde que você esteja acessando e alterando uma tabela em seu esquema padrão. Como a coluna `ProductDescription` permite valores nulos e nenhum valor está sendo fornecido, o nome de coluna `ProductDescription` e o valor podem ser descartados completamente da instrução.  
  
   ```sql  
   -- Dropping the optional dbo and dropping the ProductDescription column  
   INSERT Products (ProductID, ProductName, Price)  
       VALUES (3000, '3 mm Bracket', 0.52)  
   GO  
   ```  
  
### <a name="update-the-products-table"></a>Atualizar a tabela de produtos  
Digite e execute a instrução `UPDATE` a seguir para alterar o `ProductName` do segundo produto de `Screwdriver`para `Flat Head Screwdriver`.  
  
  ```sql  
  UPDATE dbo.Products  
      SET ProductName = 'Flat Head Screwdriver'  
      WHERE ProductID = 50  
  GO  
  ```  

## <a name="read-data-from-a-table"></a>Ler dados de uma tabela
Use a instrução SELECT para ler os dados em uma tabela. A instrução SELECT é um das instruções [!INCLUDE[tsql](../includes/tsql-md.md)] mais importantes e há muitas variações na sintaxe. Para este tutorial, você trabalhará com cinco versões simples.  
  
### <a name="read-the-data-in-a-table"></a>Ler os dados em uma tabela  
  
1.  Digite e execute as instruções seguintes para ler os dados na tabela `Products` .  
  
  ```sql 
  -- The basic syntax for reading data from a single table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
  GO  
  ```  
  
2.  Você pode usar um asterisco (`*`) para selecionar todas as colunas na tabela. O asterisco é para consultas ad hoc. Em código permanente, forneça a lista de colunas para que a instrução retorne as colunas previstas, mesmo se uma coluna nova for adicionada posteriormente à tabela.  
  
  ```sql  
  -- Returns all columns in the table  
  -- Does not use the optional schema, dbo  
  SELECT * FROM Products  
  GO   
  ```  
  
3.  Você pode omitir colunas que não deseja retornar. As colunas serão retornadas na ordem em que são listadas.  
  
  ```sql  
  -- Returns only two of the columns from the table  
  SELECT ProductName, Price  
      FROM dbo.Products  
  GO    
  ```  
  
4.  Use uma cláusula `WHERE` para limitar as linhas que serão retornadas ao usuário.  
  
  ``` sql 
  -- Returns only two of the records in the table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
      WHERE ProductID < 60  
  GO    
  ```  
  
5.  Você pode trabalhar com os valores nas colunas à medida que elas forem retornadas. O exemplo seguinte executa uma operação matemática na coluna `Price` . Colunas que foram alteradas dessa maneira não terão um nome, a menos que você forneça um, usando a palavra-chave `AS` .  
  
  ```sql  
  -- Returns ProductName and the Price including a 7% tax  
  -- Provides the name CustomerPays for the calculated column  
  SELECT ProductName, Price * 1.07 AS CustomerPays  
      FROM dbo.Products  
  GO  
  ```  
  
### <a name="useful-functions-in-a-select-statement"></a>Funções úteis em uma instrução SELECT  
Para obter informações sobre algumas funções que você pode usar para trabalhar com instruções SELECT, consulte os seguintes tópicos:  

:::row:::
    :::column:::
        [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)
    :::column-end:::
    :::column:::
        [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [Funções matemáticas &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)
    :::column-end:::
    :::column:::
        [Funções de texto e imagem &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)
    :::column-end:::
:::row-end:::

## <a name="create-views-and-stored-procedures"></a>Criar exibições e procedimentos armazenados
Uma exibição é uma instrução SELECT armazenada e um procedimento armazenado é uma ou mais instruções [!INCLUDE[tsql](../includes/tsql-md.md)] executadas como um lote.  
  
Exibições são tabelas do tipo para consultas e não aceitam parâmetros. Procedimentos armazenados são mais complexos que exibições. Procedimentos armazenados podem ter parâmetros de entrada e saída e conter instruções para controlar o fluxo do código, como instruções IF e WHILE. É uma boa prática de programação usar procedimentos armazenados para todas as ações repetitivas no banco de dados.  
  
Neste exemplo, você usará CREATE VIEW para criar uma exibição que seleciona apenas duas das colunas na tabela **Products** . Em seguida, você usará CREATE PROCEDURE para criar um procedimento armazenado que aceita um parâmetro de preço e retorna apenas produtos que custam menos do que o valor do parâmetro especificado.  
  
### <a name="create-a-view"></a>Criar uma exibição  
  
Execute a instrução a seguir para criar uma exibição que executa uma instrução SELECT e retorna os nomes e preços de nossos produtos para o usuário.  
  
  ```sql  
  CREATE VIEW vw_Names  
     AS  
     SELECT ProductName, Price FROM Products;  
  GO    
  ```  
  
### <a name="test-the-view"></a>Teste a exibição  
  
Exibições são tratadas como tabelas. Use uma instrução `SELECT` para acessar uma exibição.  
  
  ```sql  
  SELECT * FROM vw_Names;  
  GO   
  ```  
  
### <a name="create-a-stored-procedure"></a>Criar um procedimento armazenado  
  
A instrução a seguir cria um `pr_Names`de nome de procedimento armazenado, aceita um parâmetro de entrada denominado `@VarPrice` do tipo de dados `money`. O procedimento armazenado imprime a instrução `Products less than` concatenada com o parâmetro de entrada que é alterado do tipo de dados `money` para o tipo de dados de caractere `varchar(10)` . Depois, o procedimento executa uma instrução `SELECT` na exibição, passando o parâmetro de entrada como parte da cláusula `WHERE` . Isso retorna todos os produtos que custam menos do que o valor do parâmetro de entrada.  
  
  ```sql  
  CREATE PROCEDURE pr_Names @VarPrice money  
     AS  
     BEGIN  
        -- The print statement returns text to the user  
        PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
        -- A second statement starts here  
        SELECT ProductName, Price FROM vw_Names  
              WHERE Price < @varPrice;  
     END  
  GO    
  ```  
  
### <a name="test-the-stored-procedure"></a>Testar o procedimento armazenado  
  
Para testar o procedimento armazenado, digite e execute a instrução a seguir. O procedimento deve retornar os nomes dos dois produtos inseridos na tabela `Products` , na Lição 1, com um preço menor que `10.00`.  
  
  ```sql  
  EXECUTE pr_Names 10.00;  
  GO  
  ```  

## <a name="next-steps"></a>Próximas etapas
O próximo artigo ensina a configurar permissões em objetos de banco de dados. Os objetos criados na lição 1 também serão usados na lição 2. 

Vá até o próximo artigo para saber mais:
> [!div class="nextstepaction"]
> [Próximas etapas](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
  
