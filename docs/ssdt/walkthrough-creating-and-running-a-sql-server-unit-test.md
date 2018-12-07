---
title: 'Passo a passo: criar e executar um teste de unidade do SQL Server | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 992c1d8e-3729-438b-9ef4-cd103e28f145
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71be318c40c5776440bf427cad57ed3fb903e55a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540931"
---
# <a name="walkthrough-creating-and-running-a-sql-server-unit-test"></a>Passo a passo: Criar e Executar um Teste de Unidade do SQL Server
Neste passo a passo, você criará um teste de unidade do SQL Server que verifica o comportamento de vários procedimentos armazenados. Os testes de unidade do SQL Server são criados para facilitar a identificação de falhas no código que podem resultar em comportamento incorreto do aplicativo. Você pode executar testes de unidade do SQL Server e teste de aplicativo como parte de um pacote automatizado de testes.  
  
Neste passo a passo, você executará as seguintes tarefas:  
  
-   [Criar um script que contenha um esquema de banco de dados](#CreateScript)  
  
-   [Criar um projeto de banco de dados e importar esse esquema](#CreateProjectAndImport)  
  
-   [Implantar o projeto de banco de dados em um ambiente de desenvolvimento isolado](#DeployDBProj)  
  
-   [Criar testes de unidade do SQL Server](#CreateDBUnitTests)  
  
-   [Definir a lógica do teste](#DefineTestLogic)  
  
-   [Executar testes de unidade do SQL Server](#RunTests)  
  
-   [Adicionar um teste de unidade negativo](#NegativeTest)  
  
Depois que um dos testes de unidade detecta um erro em um procedimento armazenado, você corrige esse erro e executa o teste novamente.  
  
## <a name="prerequisites"></a>Prerequisites  
Para concluir esse passo a passo, você precisa se conectar a um servidor de banco de dados (ou banco de dados LocalDB) no qual tenha permissões para criar e implantar um banco de dados. Para saber mais, confira [Permissões necessárias para os recursos de banco de dados do Visual Studio](https://msdn.microsoft.com/library/aa833413(VS.100).aspx).  
  
## <a name="CreateScript"></a>Criar um script que contenha um esquema de banco de dados  
  
#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>Para criar um script a partir do qual você possa importar um esquema  
  
1.  No menu **Arquivo** , aponte para **Novo**e clique em **Arquivo**.  
  
    A caixa de diálogo **Novo Arquivo** será exibida.  
  
2.  Na lista **Categorias** , clique em **Geral** caso esse item ainda não esteja realçado.  
  
3.  Na lista **Modelos** , clique em **Arquivo SQL**e clique em **Abrir**.  
  
    O editor de Transact\-SQL é aberto.  
  
4.  Copie o seguinte código Transact\-SQL e cole-o no editor de Transact\-SQL.  
  
    ```  
    PRINT N'Creating Sales...';  
    GO  
    CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
    GO  
    PRINT N'Creating Sales.Customer...';  
    GO  
    CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Orders...';  
    GO  
    CREATE TABLE [Sales].[Orders] (  
        [CustomerID] INT      NOT NULL,  
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,  
        [OrderDate]  DATETIME NOT NULL,  
        [FilledDate] DATETIME NULL,  
        [Status]     CHAR (1) NOT NULL,  
        [Amount]     INT      NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDSales...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];  
    GO  
    PRINT N'Creating Sales.Def_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];  
    GO  
    PRINT N'Creating Sales.Def_Orders_Status...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];  
    GO  
    PRINT N'Creating Sales.PK_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.PK_Orders_OrderID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;  
    GO  
    PRINT N'Creating Sales.CK_Orders_FilledDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.CK_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.uspCancelOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'X'  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspFillOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspFillOrder]  
    @OrderID INT, @FilledDate DATETIME  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'F',  
           [FilledDate] = @FilledDate  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspNewCustomer...';  
    GO  
    CREATE PROCEDURE [Sales].[uspNewCustomer]  
    @CustomerName NVARCHAR (40)  
    AS  
    BEGIN  
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);  
    SELECT SCOPE_IDENTITY()  
    END  
    GO  
    PRINT N'Creating Sales.uspPlaceNewOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]  
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'  
    AS  
    BEGIN  
    DECLARE @RC INT  
    BEGIN TRANSACTION  
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)   
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)  
    SELECT @RC = SCOPE_IDENTITY();  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders + @Amount  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    RETURN @RC  
    END  
    GO  
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]  
    @CustomerID INT=0  
    AS  
    BEGIN  
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]  
      FROM [Sales].[Customer] AS C  
      INNER JOIN [Sales].[Orders] AS O  
         ON [O].[CustomerID] = [C].[CustomerID]  
      WHERE [C].[CustomerID] = @CustomerID  
    END  
    GO  
    ```  
  
5.  Salve o arquivo. Anote o local, pois você deve usar esse script no próximo procedimento.  
  
6.  No menu **Arquivo** , clique em **Fechar Solução**.  
  
    Em seguida, você cria um projeto de banco de dados e importa o esquema do script criado.  
  
## <a name="CreateProjectAndImport"></a>Criar um projeto de banco de dados e importar um esquema  
  
#### <a name="to-create-a-database-project"></a>Para criar um projeto de banco de dados  
  
1.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  Em **Modelos Instalados**, selecione o nó **SQL Server** e selecione **Projeto de Banco de Dados do SQL Server**.  
  
3.  Em **Nome**, digite **SimpleUnitTestDB**.  
  
4.  Selecione a caixa de seleção **Criar diretório para a solução** se ela ainda não estiver selecionada.  
  
5.  Desmarque a caixa de seleção **Adicionar ao Controle de Origem** se ela ainda não estiver desmarcada e clique em **OK**.  
  
    O projeto de banco de dados é criado e aparece no **Gerenciador de Soluções**. Em seguida, você importa o esquema de banco de dados de um script.  
  
#### <a name="to-import-a-database-schema-from-a-script"></a>Para importar um esquema de banco de dados de um script.  
  
1.  No menu **Projeto**, clique em **Importar** e, em seguida, em **Script (\*.sql)**.  
  
2.  Clique em **Avançar** após ler a página de boas-vindas.  
  
3.  Clique no botão **Procurar**e vá para o diretório em que você salvou o arquivo .sql.  
  
4.  Clique duas vezes no arquivo .sql e clique em **Concluir**.  
  
    O script é importado, e os objetos que estão definidos no script são adicionados ao projeto de banco de dados.  
  
5.  Analise o resumo e clique em **Concluir** para concluir a operação.  
  
    > [!NOTE]  
    > O procedimento Sales.uspFillOrder contém um erro de codificação intencional que você descobrirá e corrigirá mais adiante neste procedimento.  
  
#### <a name="to-examine-the-resulting-project"></a>Para examinar o projeto resultante  
  
1.  No **Gerenciador de Soluções**, examine os arquivos de script que foram importados para o projeto.  
  
2.  No **Pesquisador de Objetos do SQL Server**, observe o banco de dados no nó Projetos.  
  
## <a name="DeployDBProj"></a>Implantar no LocalDB  
Por padrão, quando você pressiona F5, implanta (ou publica) o banco de dados em um banco de dados LocalDB. Você pode alterar o local do banco de dados indo para a guia Depurar da página de propriedades do projeto e alterando a cadeia de conexão.  
  
## <a name="CreateDBUnitTests"></a>Criar testes de unidade do SQL Server  
  
#### <a name="to-create-a-sql-server-unit-test-for-the-stored-procedures"></a>Para criar um teste de unidade do SQL Server para os procedimentos armazenados  
  
1.  No **Pesquisador de Objetos do SQL Server**, expanda o nó de projetos de **SimpleUnitTestDB** e, em seguida, expanda **Programabilidade** e o nó **Procedimentos Armazenados**.  
  
2.  Clique com o botão direito do mouse em um dos procedimentos armazenados e clique em **Criar Testes de Unidade** para exibir a caixa de diálogo **Criar Testes de Unidade**.  
  
3.  Marque as caixas de seleção para todos os cinco procedimentos armazenados: **Sales.uspCancelOrder**, **Sales.uspFillOrder**, **Sales.uspNewCustomer**, **Sales.uspPlaceNewOrder**e **Sales.uspShowOrderDetails**.  
  
4.  Na lista suspensa **Projeto**, selecione **Criar um novo projeto de teste do Visual C#**.  
  
5.  Aceite os nomes padrão do projeto e da classe, e clique em **OK**.  
  
6.  Na caixa de diálogo configuração de teste, em **Executar testes de unidade usando a seguinte conexão de dados**, especifique uma conexão com o banco de dados implantado anteriormente neste passo a passo. Por exemplo, se você usou o local de implantação padrão, que é LocalDB, clique em **Nova Conexão** e especifique **(LocalDB)\Projects**. Em seguida, escolha o nome do banco de dados. Em seguida, clique em OK para fechar a caixa de diálogo **Propriedades da Conexão** .  
  
    > [!NOTE]  
    > Se for necessário testar exibições ou procedimentos armazenados que tenham permissões restritas, você normalmente especificará essa conexão nessa etapa. Em seguida, você especificará a conexão secundária, com permissões mais amplas, para validar o teste. Se você tiver uma conexão secundária, deverá adicionar esse usuário ao projeto de banco de dados e criará um logon para esse usuário no script de pré-implantação.  
  
7.  Na caixa de diálogo de configuração de teste, na seção **Implantação** , marque a caixa de seleção **Implantar automaticamente o projeto de banco de dados antes que os testes de unidade sejam executados** .  
  
8.  Em **Projeto de Banco de Dados**, clique em **SimpleUnitTestDB.sqlproj**.  
  
9. Em **Configuração da implantação**, clique em **Depurar**.  
  
    Você também pode gerar dados de teste como parte dos testes de unidade do SQL Server. Neste passo a passo, você ignorará essa etapa porque os testes criarão seus próprios dados.  
  
10. Clique em **OK**.  
  
    O projeto de teste é compilado e o Designer de Teste de Unidade do SQL Server é exibido. Em seguida, você atualizará a lógica do teste no script Transact\-SQL dos testes de unidade.  
  
## <a name="DefineTestLogic"></a>Definir a lógica do teste  
Esse banco de dados simples tem duas tabelas, Customer e Order. Você atualiza o banco de dados usando os seguintes procedimentos armazenados:  
  
-   uspNewCustomer - Este procedimento armazenado adiciona um registro à tabela Customer, que define as colunas YTDOrders e YTDSales do cliente como zero.  
  
-   uspPlaceNewOrder - Este procedimento armazenado adiciona um registro à tabela Orders para o cliente especificado e atualiza o valor de YTDOrders no registro correspondente da tabela Customer.  
  
-   uspFillOrder - Este procedimento armazenado atualiza um registro na tabela Orders alterando o status de 'O' para 'F' e incrementa o valor de YTDSales no registro correspondente da tabela Customer.  
  
-   uspCancelOrder - Este procedimento armazenado atualiza um registro na tabela Orders alterando o status de 'O' para 'F' e incrementa o valor de YTDOrders no registro correspondente da tabela Customer.  
  
-   uspShowOrderDetails - Este procedimento armazenado une a tabela Orders à tabela Custom e mostra os registros de um cliente específico.  
  
> [!NOTE]  
> Este exemplo ilustra como criar um teste simples de unidade do SQL Server. Em um banco de dados real, você poderia somar os valores totais de todos os pedidos com o status 'O' ou 'F' de um cliente específico. Os procedimentos neste passo a passo também não contêm tratamento de erro. Por exemplo, eles não impedem que você chame uspFillOrder para um pedido que já tenha sido preenchido.  
  
Os testes presumem que o banco de dados começa em um estado limpo. Você criará os testes que verificam as seguintes condições:  
  
-   uspNewCustomer - Verifique se a tabela Customer contém uma linha depois que o procedimento armazenado é executado.  
  
-   uspPlaceNewOrder - Para o cliente que tem uma CustomerID igual a 1, insira um pedido de US$ 100. Verifique se o valor de YTDOrders desse cliente é 100 e se o valor de YTDSales é zero.  
  
-   uspFillOrder - Para o cliente que tem a CustomerID 1, insira um pedido de US$ 50. Preencha esse pedido. Verifique se os valores de YTDOrders e YTDSales são 50.  
  
-   uspShowOrderDetails - Para o cliente que tem uma CustomerID igual a 1, insira pedidos de US$ 100, US$ 50 e US$ 5. Verifique se uspShowOrderDetails retorna o número certo de colunas e se o conjunto de resultados tem a soma de verificação esperada.  
  
> [!NOTE]  
> Para um conjunto completo de testes de unidade do SQL Server, você normalmente verificará se as outras colunas foram definidas corretamente. Para manter este passo a passo em um tamanho gerenciável, ele não descreve como verificar o comportamento de uspCancelOrder.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspnewcustomer"></a>Para gravar o teste de unidade do SQL Server de uspNewCustomer  
  
1.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspNewCustomerTest** e verifique se **Teste** está realçado na lista adjacente.  
  
    Depois que você executar a etapa anterior, poderá criar o script de teste para a ação de teste na unidade de teste.  
  
2.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    -- ssNoVersion unit test for Sales.uspNewCustomer  
    DECLARE @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @CustomerName = 'Fictitious Customer';  
  
    EXECUTE @RC = [Sales].[uspNewCustomer] @CustomerName;  
  
    SELECT * FROM [Sales].[Customer];  
    ```  
  
3.  No painel **Condições de Teste**, clique na condição de teste Inconclusivo e clique no ícone **Excluir Condição de Teste** (o x vermelho).  
  
4.  No painel **Condições de Teste**, clique em **Contagem de Linhas** na lista e clique no ícone **Adicionar Condição de Teste** (o + verde).  
  
5.  Abra a janela **Propriedades** (selecione a condição de teste e pressione F4) e defina a propriedade **Row Count** como 1.  
  
6.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
    Agora você definirá a lógica de teste de unidade de uspPlaceNewOrder.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspplaceneworder"></a>Para gravar o teste de unidade do SQL Server de uspPlaceNewOrder  
  
1.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspPlaceNewOrderTest** e verifique se **Teste** está realçado na lista adjacente.  
  
    Depois que você executar essa etapa, poderá criar o script de teste da ação de teste no teste de unidade.  
  
2.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    -- ssNoVersion unit test for Sales.uspPlaceNewOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDOrders] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC  
    ```  
  
3.  No painel **Condições de Teste** , clique na condição de teste Inconclusivo e clique em **Excluir Condição de Teste**.  
  
4.  No painel **Condições de Teste** , clique em **Valor Escalar** na lista e clique em **Adicionar Condição de Teste**.  
  
5.  Na janela **Propriedades** , defina a propriedade **Valor Esperado** como 100.  
  
6.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspPlaceNewOrderTest** e verifique se **Pré-Teste** está realçado na lista adjacente.  
  
    Após executar essa etapa, você poderá especificar as instruções que colocarão seus dados no estado necessário para que o teste seja executado. Nesse exemplo, crie o registro do cliente para que um pedido possa ser inserido.  
  
7.  Clique em **Clique aqui para criar** para criar um script de pré-teste.  
  
8.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    -- Add a customer for this test with the name 'Fictitious Customer'  
    DECLARE @NewCustomerID AS INT, @CustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
       @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
    ```  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
    Agora você criará o teste de unidade de uspFillOrder.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspfillorder"></a>Para gravar o teste de unidade do SQL Server de uspFillOrder  
  
1.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspFillOrderTest** e verifique se **Teste** está realçado na lista adjacente.  
  
    Depois que você executar essa etapa, poderá criar o script de teste da ação de teste no teste de unidade.  
  
2.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDSales] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC;  
    ```  
  
3.  No painel **Condições de Teste** , clique na condição de teste Inconclusivo e clique em **Excluir Condição de Teste**.  
  
4.  No painel **Condições de Teste** , clique em **Valor Escalar** na lista e clique em **Adicionar Condição de Teste**.  
  
5.  Na janela **Propriedades** , defina a propriedade **Valor Esperado** como 100.  
  
6.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspFillOrderTest** e verifique se **Pré-Teste** está realçado na lista adjacente. Após executar essa etapa, você poderá especificar as instruções que colocarão seus dados no estado necessário para que o teste seja executado. Nesse exemplo, crie o registro do cliente para que um pedido possa ser inserido.  
  
7.  Clique em **Clique aqui para criar** para criar um script de pré-teste.  
  
8.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspshoworderdetails"></a>Para gravar o teste de unidade do SQL Server de uspShowOrderDetails  
  
1.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspShowOrderDetailsTest** e verifique se **Teste** está realçado na lista adjacente.  
  
    Depois que você executar essa etapa, poderá criar o script de teste da ação de teste no teste de unidade.  
  
2.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  No painel **Condições de Teste** , clique na condição de teste Inconclusivo e clique em **Excluir Condição de Teste**.  
  
4.  No painel **Condições de Teste** , clique em **Esquema Esperado** na lista e clique em **Adicionar Condição de Teste**.  
  
5.  Na janela **Propriedades**, na propriedade **Configuração**, clique no botão Procurar ('**...**').  
  
6.  Na caixa de diálogo de **Configuração para expectedSchemaCondition1** , especifique uma conexão com o banco de dados. Por exemplo, se você usou o local de implantação padrão, que é LocalDB, clique em **Nova Conexão** e especifique **(LocalDB)\Projects**. Em seguida, escolha o nome do banco de dados.  
  
7.  Clique em **Recuperar**. (Se for necessário, clique em **Recuperar** até ver os dados.)  
  
    O corpo Transact\-SQL do teste de unidade é executado, e o esquema resultante aparece na caixa de diálogo. Como o código de pré-teste não foi executado, nenhum dado será retornado. Como você está apenas verificando o esquema, e não os dados, não tem problema.  
  
8.  Clique em **OK**.  
  
    O esquema esperado é armazenado com a condição de teste.  
  
9. Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspShowOrderDetailsTest** e verifique se **Pré-Teste** está realçado na lista adjacente. Após executar essa etapa, você poderá especificar as instruções que colocarão seus dados no estado necessário para que o teste seja executado. Nesse exemplo, crie o registro do cliente para que um pedido possa ser inserido.  
  
10. Clique em **Clique aqui para criar** para criar um script de pré-teste.  
  
11. Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'FictitiousCustomer'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
12. Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspShowOrderDetailsTest** e clique em **Teste** na lista adjacente.  
  
    Você deve fazer isso porque deseja aplicar a condição de soma de verificação ao teste, e não ao pré-teste.  
  
13. No painel **Condições de Teste** , clique em **Soma de Verificação de Dados** na lista e clique em **Adicionar Condição de Teste**.  
  
14. Na janela **Propriedades**, na propriedade **Configuração**, clique no botão Procurar ('**...**').  
  
15. Na caixa de diálogo **Configuração para checksumCondition1** , especifique uma conexão com o banco de dados.  
  
16. Substitua o Transact\-SQL na caixa de diálogo (no botão **Editar Conexão**) com o código a seguir:  
  
    ```  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @FilledDate AS DATETIME;  
    DECLARE @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
    Esse código combina o código Transact\-SQL do pré-teste com o Transact\-SQL do próprio teste. Você precisará de ambos para retornar os mesmos resultados que o teste retornará quando você executá-lo.  
  
17. Clique em **Recuperar**. (Se for necessário, clique em **Recuperar** até ver os dados.)  
  
    O Transact\-SQL especificado é executado, e uma soma de verificação é calculada para os dados retornados.  
  
18. Clique em **OK**.  
  
    A soma de verificação calculada é armazenada com a condição de teste. A soma de verificação esperada aparece na coluna Valor da condição de teste Soma de Verificação de Dados.  
  
19. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
    Neste ponto do processo, você estará pronto para a execução dos testes.  
  
## <a name="RunTests"></a>Executar testes de unidade do SQL Server  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>Para executar testes de unidade do SQL Server  
  
1.  No menu **Teste**, aponte para **Janelas**e clique em **Modo de Teste** no Visual Studio 2010 ou **Gerenciador de Testes** no Visual Studio 2012.  
  
2.  Na janela **Modo de Teste** (Visual Studio 2010), clique em **Atualizar** na barra de ferramentas para atualizar a lista de testes. Para ver a lista de testes no **Gerenciador de Testes** (Visual Studio 2012), crie a solução.  
  
    A janela **Modo de Teste** ou **Gerenciador de Teste** lista os testes que você criou anteriormente neste passo a passo, e aos quais adicionou instruções Transact\-SQL e condições de teste. O teste TestMethod1 está vazio e não é usado neste passo a passo.  
  
3.  Clique com o botão direito do mouse em **Sales_uspNewCustomerTest** e clique em **Executar Seleção**.  
  
    O Visual Studio usa o contexto privilegiado que você especificou para se conectar ao banco de dados e aplicar o plano de geração de dados. O Visual Studio alterna para o contexto de execução antes de executar o script Transact\-SQL no teste. Por fim, o Visual Studio avalia os resultados do script Transact\-SQL com base nos critérios que você especificou na condição de teste, e um resultado de aprovação ou falha é exibido na janela **Resultados de Teste**.  
  
4.  Exiba o resultado na janela **Resultados do Teste** .  
  
    O teste é aprovado, o que significa que a instrução **SELECT** retornará uma linha quando ele for executado.  
  
5.  Repita a etapa 3 dos testes Sales_uspPlaceNewOrderTest, Sales_uspFillOrderTest e Sales_uspShowOrderDetailsTest. Estes serão os resultados:  
  
    |Teste|Resultado esperado|  
    |--------|-------------------|  
    |Sales_uspPlaceNewOrderTest|Aprovado|  
    |Sales_uspShowOrderDetailsTest|Aprovado|  
    |Sales_uspFillOrderTest|Falha com o erro a seguir: "Falha na condição ScalarValueCondition (scalarValueCondition2): ResultSet 1 Linha 1 Coluna 1: valores não correspondentes, '-100' real '100' esperado." Esse erro ocorre porque a definição do procedimento armazenado contém um erro secundário.|  
  
    Em seguida, você corrigirá o erro e executará o teste novamente.  
  
#### <a name="to-correct-the-error-in-salesuspfillorder"></a>Para corrigir o erro em Sales.uspFillOrder  
  
1.  No nó Projetos do **Pesquisador de Objetos do SQL Server** do seu banco de dados, clique duas vezes no procedimento armazenado **uspFillOrder** para abrir sua definição no editor de Transact\-SQL.  
  
2.  Na definição, localize a seguinte instrução Transact\-SQL:  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
3.  Altere a cláusula SET na instrução para que corresponda à seguinte instrução:  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales + @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
4.  No menu **Arquivo** , clique em **Save uspFillOrder.sql**.  
  
5.  No **Modo de Teste**, clique com o botão direito do mouse em **Sales_uspFillOrderTest** e clique em **Executar Seleção**.  
  
    O teste é aprovado.  
  
## <a name="NegativeTest"></a>Adicionar um teste de unidade negativo  
Você pode criar um teste negativo para verificar se um teste apresentará falha quando realmente deveria. Por exemplo, se você tentar cancelar um pedido que já foi preenchido, esse teste apresentará falha. Nesta parte do passo a passo, você cria um teste de unidade negativo para o procedimento armazenado Sales.uspCancelOrder.  
  
Para criar e verificar um teste negativo, execute as seguintes tarefas:  
  
-   Atualize o procedimento armazenado para testar as condições de falha  
  
-   Defina um novo teste de unidade  
  
-   Modifique o código do teste de unidade para indicar que ele deve apresentar falha  
  
-   Execute o teste de unidade  
  
#### <a name="to-update-the-stored-procedure"></a>Para atualizar os procedimento armazenado  
  
1.  No nó Projetos do **Pesquisador de Objetos do SQL Server** do banco de dados SimpleUnitTestDB, expanda o nó Programabilidade, expanda o nó Procedimentos Armazenados e clique duas vezes em uspCancelOrder.  
  
2.  No editor de Transact\-SQL, atualize a definição do procedimento para que corresponda ao código a seguir:  
  
    ```  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
        DECLARE @Delta INT, @CustomerID INT, @PriorStatus CHAR(1)  
        BEGIN TRANSACTION  
            BEGIN TRY  
                IF (NOT EXISTS(SELECT [CustomerID] from [Sales].[Orders] WHERE [OrderID] = @OrderID))  
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR( 'That order does not exist.', -- Message text  
                               16, -- severity  
                                1 -- state  
                            ) WITH LOG;  
                END  
  
                SELECT @Delta = [Amount], @CustomerID = [CustomerID], @PriorStatus = [Status]  
                 FROM [Sales].[Orders] WHERE [OrderID] = @OrderID  
  
                IF @PriorStatus <> 'O'   
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR ( 'You can only cancel open orders.', -- Message text  
                                16, -- Severity  
                                1 -- State  
                                ) WITH LOG;  
                END  
                ELSE  
                BEGIN  
                    -- If we make it to here, then we can cancel the order. Update the status to 'X' first...  
                    UPDATE [Sales].[Orders]  
                       SET [Status] = 'X'  
                    WHERE [OrderID] = @OrderID  
                    -- and then remove the amount from the YTDOrders for the customer  
                    UPDATE [Sales].[Customer]  
                           SET  
                               YTDOrders = YTDOrders - @Delta  
                    WHERE [CustomerID] = @CustomerID  
                    COMMIT TRANSACTION  
                    RETURN 1; -- indicate success  
                END  
            END TRY  
            BEGIN CATCH  
                DECLARE @ErrorMessage NVARCHAR(4000);  
                DECLARE @ErrorSeverity INT;  
                DECLARE @ErrorState INT;  
  
                SELECT @ErrorMessage = ERROR_MESSAGE(),  
                       @ErrorSeverity = ERROR_SEVERITY(),  
                       @ErrorState = ERROR_STATE();  
  
                ROLLBACK TRANSACTION  
                -- Use RAISERROR inside the CATCH block to return  
                -- error information about the original error that  
                -- caused execution to jump to the CATCH block.  
                RAISERROR (@ErrorMessage, -- Mesasge text  
                           @ErrorSeverity, -- Severity  
                           @ErrorState -- State  
                          );  
                RETURN 0; -- indicate failure  
            END CATCH;  
    END  
    ```  
  
3.  No menu **Arquivo** , clique em **Save uspCancelOrder.sql**.  
  
4.  Pressione F5 para implantar **SimpleUnitTestDB**.  
  
    Você implanta as atualizações para o procedimento armazenado uspCancelOrder. Você não alterou nenhum outro objeto; portanto, esse procedimento armazenado será atualizado.  
  
    Agora você definirá o teste de unidade associado desse procedimento.  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspcancelorder"></a>Para gravar o teste de unidade do SQL Server de uspCancelOrder  
  
1.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspCancelOrderTest** e verifique se **Teste** está realçado na lista adjacente.  
  
    Depois que você executar essa etapa, poderá criar o script de teste da ação de teste no teste de unidade.  
  
2.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- try to cancel an order for that customer that has already been filled  
    EXECUTE @RC = [Sales].[uspCancelOrder] @OrderID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  No painel **Condições de Teste** , clique na condição de teste Inconclusivo e clique no ícone **Excluir Condição de Teste** .  
  
4.  No painel **Condições de Teste** , clique em **Valor Escalar** na lista e clique no ícone **Adicionar Condição de Teste** .  
  
5.  Na janela **Propriedades** , defina a propriedade **Valor Esperado** como 0.  
  
6.  Na barra de navegação do Designer de Teste de Unidade do SQL Server, clique em **Sales_uspCancelOrderTest** e verifique se **Pré-Teste** está realçado na lista adjacente. Após executar essa etapa, você poderá especificar as instruções que colocarão seus dados no estado necessário para que o teste seja executado. Nesse exemplo, crie o registro do cliente para que um pedido possa ser inserido.  
  
7.  Clique em **Clique aqui para criar** para criar um script de pré-teste.  
  
8.  Atualize as instruções Transact\-SQL no editor de Transact\-SQL para que correspondam às seguintes instruções:  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @FilledDate AS DATETIME, @Status AS CHAR (1), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
       @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
       @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @OrderID = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- fill the order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    COMMIT TRANSACTION  
    ```  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
    Neste ponto do processo, você estará pronto para a execução dos testes.  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>Para executar testes de unidade do SQL Server  
  
1.  No **Modo de Teste**, clique com o botão direito do mouse em **Sales_uspCancelOrderTest** e clique em **Executar Seleção**.  
  
2.  Exiba o resultado na janela **Resultados do Teste** .  
  
    O teste apresentará falha e o seguinte erro será exibido:  
  
    **Test method TestProject1.SqlServerUnitTests1.Sales_uspCancelOrderTest threw exception: System.Data.SqlClient.SqlException: você só pode cancelar os pedidos abertos.**  
  
    Em seguida, modifique o código para indicar que a exceção é esperada.  
  
#### <a name="to-modify-the-code-for-the-unit-test"></a>Para modificar o código do teste de unidade  
  
1.  No **Gerenciador de Soluções**, expanda **TestProject1**, clique com o botão direito do mouse em **SqlServerUnitTests1.cs** e clique em **Exibir Código**.  
  
2.  No editor de códigos, navegue até o método Sales_uspCancelOrderTest. Modifique os atributos do método para que correspondam ao seguinte código:  
  
    ```  
    [TestMethod(), ExpectedSqlException(Severity=16, MatchFirstError=false, State=1)]  
    public void Sales_uspCancelOrderTest()  
    ```  
  
    Você especifica que espera ver uma exceção específica. Se desejar, você pode especificar um número de erro. Se você não adicionar esse atributo, o teste de unidade apresentará falha e uma mensagem aparecerá na janela Resultados do Teste.  
  
    > [!IMPORTANT]  
    > Atualmente, o Visual Studio 2012 não oferece suporte ao atributo ExpectedSqlException. Para obter informações para solucionar isso, consulte [Não foi possível executar o teste de unidade de banco de dados com "Falha esperada"](https://social.msdn.microsoft.com/Forums/en-US/ssdt/thread/e74e06ad-e3c9-4cb0-97ad-a6f235a52345).  
  
3.  No menu Arquivo, clique em Salvar SqlServerUnitTests1.cs.  
  
    Em seguida, você executará novamente o teste de unidade para verificar que ele falhou como esperado.  
  
#### <a name="to-re-run-the-sql-server-unit-tests"></a>Para executar novamente testes de unidade do SQL Server  
  
1.  No **Modo de Teste**, clique com o botão direito do mouse em **Sales_uspCancelOrderTest** e clique em **Executar Seleção**.  
  
2.  Exiba o resultado na janela **Resultados do Teste** .  
  
    O teste é aprovado, o que significa que o procedimento apresentou falha quando deveria.  
  
## <a name="next-steps"></a>Next Steps  
Em um projeto típico, você definirá testes de unidade adicionais para verificar se todos os objetos de banco de dados essenciais estão funcionando corretamente. Quando o conjunto de testes for concluído, você fará check-in dos testes para controle de versão a fim de compartilhá-los com a equipe.  
  
Após estabelecer uma linha de base, você poderá criar e modificar objetos de banco de dados e, em seguida, criar testes associados para verificar se uma alteração afetará o comportamento esperado.  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[Como criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[Como configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
