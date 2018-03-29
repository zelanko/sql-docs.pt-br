---
Title: 'Tutorial: Connect and Query SQL Server using SQL Server Management Studio'
description: Um Tutorial para se conectar ao SQL Server usando o SQL Server Management Studio e executar consultas T-SQL básicas.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 7b389c5b58dc0afde077f70e2fd8bec7c6cac4d0
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-connect-and-query-sql-server-using-sql-server-management-studio"></a>Tutorial: conectar-se consultar o SQL Server usando o SQL Server Management Studio
Este Tutorial ensina como usar o SSMS (SQL Server Management Studio) para se conectar à instância do SQL Server e executar alguns comandos básicos do T-SQL (Transact-SQL). Este artigo demonstra como fazer o seguinte:
    - [Conectar a um SQL Server](#connect-to-a-sql-server)
    - [Criar um novo banco de dados (**TutorialDB**)](#create-a-database)
    - [Criar uma tabela (**Clientes**) no seu novo banco de dados](#create-a-table)
    - [Inserir linhas na sua nova tabela **Clientes**](#insert-rows)
    - [Consultar a tabela **Clientes** e exibir os resultados](#view-query-results)
    - [Usar a tabela da janela de consulta para verificar suas propriedades de conexão](#verify-your-query-window-connection-properties)
    - [Alterar a qual servidor sua janela de consulta está conectada](#change-server-connection-within-query-window)


## <a name="prerequisites"></a>Prerequisites
Para concluir este Tutorial, você precisa do SQL Server Management Studio e acesso a um SQL Server. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

Se você não tiver acesso a um SQL Server, selecione a plataforma dentre os links a seguir (lembre-se do Login e da Senha do SQL se escolher a Autenticação SQL):
- [Windows – Baixar o SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS – Baixar o SQL Server 2017 no Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server"></a>Conectar a um SQL Server

1. Inicie o SSMS (Start SQL Server Management Studio).
1. Na primeira vez que você executar o SSMS, a caixa de diálogo **Conectar ao Servidor** é aberta. 
      - Se a caixa de diálogo **Conectar ao Servidor** não abrir, ela poderá ser aberta manualmente em **Pesquisador de Objetos** > **Conectar** (ou ícone ao lado dele) > **Mecanismo de Banco de Dados**.

        ![Conectar ao Pesquisador de Objetos](media/connect-query-sql-server/connectobjexp.png)

1. Na caixa de diálogo **Conectar ao Servidor**, preencha as opções de conexão: 

    - **Tipo de servidor**: Mecanismo de Banco de Dados (normalmente é o selecionado por padrão)
    - **Autenticação**: Autenticação do Windows (este artigo usa a Autenticação do Windows, mas o Logon do SQL tem suporte e solicita um nome de usuário/senha se selecionado)

      ![Conexão](media/connect-query-sql-server/connection.png)

        Também é possível modificar as opções de conexão adicionais (como o banco de dados ao qual você está se conectando, o valor de tempo limite de conexão e o protocolo de rede) clicando no botão **Opções**. Para a finalidade deste artigo, tudo foi deixado nos valores padrão. 

1. Depois que os campos foram preenchidos, clique em **Conectar**. 

1. Você pode verificar se a conexão foi bem-sucedida para o SQL Server explorando os objetos no **Pesquisador de Objetos**: 

   ![Conexão bem-sucedida](media/connect-query-sql-server/successfulconnection.png)


## <a name="create-a-database"></a>Criar um banco de dados
As etapas a seguir criam outro banco de dados denominado TutorialDB. 

1. Clique com o botão direito do mouse no servidor no **Pesquisador de Objetos** e selecione **Nova Consulta**:

   ![Nova Consulta](media/connect-query-sql-server/newquery.png)
   
1. Cole o seguinte trecho de código T-SQL na janela de consulta: 
   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```
2. Para executar a consulta, clique em **Executar** (ou pressione F5 no teclado). 

   ![Executar Consulta](media/connect-query-sql-server/execute.png)
  
 
Depois que a consulta for concluída, o novo **TutorialDB** aparece na lista de bancos de dados no **Pesquisador de Objetos**. Se ele não aparecer, clique com botão direito do mouse no nó Banco de Dados e selecione **Atualizar**.  


## <a name="create-a-table"></a>Criar uma Tabela
As etapas a seguir criarão uma tabela no banco de dados **TutorialDB** recém-criado. No entanto, o editor de consultas ainda está no contexto do banco de dados *mestre* e você deseja criar uma tabela no banco de dados *TutorialDB*. 

1. Altere o contexto de conexão da sua consulta de banco de dados mestre para **TutorialDB** selecionando o banco de dados desejado na lista suspensa de banco de dados. 

   ![Alterar banco de dados](media/connect-query-sql-server/changedb.png)

1. Cole o seguinte trecho de código T-SQL na janela de consulta, selecione-o e clique em **Executar** (ou pressione F5 no seu teclado): 
    - Você pode substituir o texto existente na janela de consulta ou acrescentá-lo no final. Se você quiser executar tudo na janela de consulta, clique em **Executar**. Se você quiser executar uma parte do texto, selecione essa parte e clique em **Executar**.  
  
   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```
Depois que a consulta for concluída, a nova tabela **Clientes** aparece na lista de tabelas no **Pesquisador de Objetos**. Se a tabela não estiver visível, clique com botão direito do mouse no nó **TutorialDB > Tabelas** no **Pesquisador de Objetos** e selecione **Atualizar**.

## <a name="insert-rows"></a>Inserir linhas
A etapa a seguir inserirá algumas linhas na tabela **Clientes** criada anteriormente. 

Cole o seguinte trecho de código T-SQL na janela de consulta e clique em **Executar**: 


   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-query-results"></a>Exibir Resultados da Consulta
Os resultados de uma consulta são visíveis sob a janela de texto de consulta. As etapas a seguir permitirão consultar a tabela **Clientes** e exibir as linhas que foram inseridas anteriormente.  

1. Cole o seguinte trecho de código T-SQL na janela de consulta e clique em **Executar**: 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```
1. Os resultados da consulta são exibidos na área onde o texto foi inserido: 

   ![Resultados da consulta](media/connect-query-sql-server/queryresults.png)


1.  Você pode modificar a maneira como os resultados são apresentados selecionando uma destas opções:

     ![resultados](media/connect-query-sql-server/results.png)

    - Por padrão, os resultados estarão em **Exibição em Grade**, que é o botão do meio e mostra os resultados em uma tabela. 
    - O primeiro botão exibirá os resultados em **Exibição de Texto**, conforme mostrado na imagem na próxima seção.
    - O terceiro botão permitirá salvar os resultados em um arquivo com extensão *.rpt por padrão.

## <a name="verify-your-query-window-connection-properties"></a>Verifique as propriedades de conexão da janela de consulta
Você pode encontrar informações sobre as propriedades de conexão nos resultados da sua consulta. 
- Depois de executar a consulta mencionados acima da etapa anterior, revise as propriedades de conexão na parte inferior da janela de consulta.
    - Você pode determinar a qual servidor e banco de dados você está conectado e o usuário com o qual você fez logon.
    - Você também pode ver a duração da consulta e o número de linhas retornado pela consulta executada anteriormente.
    
    ![Propriedades da Conexão](media/connect-query-sql-server/connectionproperties.png)  
    Nesta imagem, os resultados são exibidos em **Exibição de Texto**.  

## <a name="change-server-connection-within-query-window"></a>Alterar a conexão de servidor na Janela de Consulta
Você pode alterar a qual servidor sua janela de consulta atual está conectada seguindo estas etapas.
1. Clique com o botão direito do mouse na janela de consulta > Conexão > Alterar conexão.
2. Isso abrirá a caixa de diálogo **Conectar ao Servidor** novamente, permitindo que você altere o servidor ao qual sua consulta está conectado. 
 
   ![Alterar Conexão](media/connect-query-sql-server/changeconnection.png)
   - Observe que isso não altera a qual servidor o **Pesquisador de Objetos** está conectado, apenas a janela de consulta atual. 



