---
title: Conectar-se a uma instância do SQL Server e consultá-la
description: Um tutorial para conectar-se a uma instância do SQL Server usando o SQL Server Management Studio e executando consultas T-SQL básicas.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: markingmyname
ms.author: maghan
ms.reviewer: sstein; maghan
ms.topic: tutorial
ms.prod_service: sql-tools
ms.prod: sql
ms.technology: ssms
ms.custom: seo-lt-2019
ms.date: 03/13/2018
ms.openlocfilehash: ac805437d716bbc7e8fdf95f491c64331ddb4658
ms.sourcegitcommit: 844793cd1c058e6bba136f050734e7dc62024a82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/25/2020
ms.locfileid: "77575542"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio-ssms"></a>Tutorial: conectar-se a uma instância do SQL Server e consultá-la usando o SSMS (SQL Server Management Studio)

Este tutorial ensina a usar o SSMS (SQL Server Management Studio) para conectar-se à instância do SQL Server e executar alguns comandos T-SQL (Transact-SQL) básicos. O artigo demonstra como fazer o seguinte nas etapas abaixo:

> [!div class="checklist"]
> * Conectar a uma instância do SQL Server
> * Criar um banco de dados ("TutorialDB")
> * Criar uma tabela ("Clientes") no novo banco de dados
> * Inserir linhas na nova tabela
> * Consultar a nova tabela e exibir os resultados
> * Usar a tabela da janela de consulta para verificar as propriedades da conexão
> * Alterar o servidor ao qual a janela de consulta está conectada

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este tutorial, você precisa de acesso ao SQL Server Management Studio e a uma instância do SQL Server. 

* Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Se você não tiver acesso a uma instância do SQL Server, selecione sua plataforma nos links a seguir. Se você escolher Autenticação do SQL, use suas credenciais de logon do SQL Server.

* **Windows**: [Baixe o SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
* **macOS**: [baixe o SQL Server 2017 no Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="connect-to-a-sql-server-instance"></a>Conectar a uma instância do SQL Server

1. Inicie o SQL Server Management Studio. Na primeira vez em que você executar o SSMS, a janela **Conectar-se ao Servidor** será aberta. Se ela não for aberta, você poderá abri-la manualmente selecionando **Pesquisador de Objetos** > **Conectar** > **Mecanismo de Banco de Dados**.

    ![O link de conexão no Pesquisador de Objetos](media/connect-query-sql-server/connectobjexp.png)

2. Na janela **Conectar-se ao servidor**, siga a lista a seguir:

    * Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados** (geralmente a opção padrão).
    * Para **Nome do servidor**, insira o nome da instância do SQL Server. [Este artigo usa o nome da instância SQL2016ST no nome do host NODE5 (NODE5\SQL2016ST)]. Se você não tiver certeza de como determinar o nome da instância do SQL Server, confira [Mais dicas e truques para usar o SSMS](ssms-tricks.md#determine-sql-server-name).

    * Para **Autenticação**, selecione **Autenticação do Windows**. Este artigo usa a Autenticação do Windows, mas também é possível fazer o logon do SQL Server. Se você selecionar **Logon do SQL**, deverá inserir um nome de usuário e uma senha. Para obter mais informações sobre os tipos de autenticação, confira [Conectar ao servidor (mecanismo de banco de dados)](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine).

    ![Campo "Nome do servidor" com a opção de usar a instância do SQL Server](media/connect-query-sql-server/connection2.png)

    Você também pode modificar as opções de conexão adicionais selecionando **Opções**. Exemplos de opções de conexão são o banco de dados ao qual você está se conectando, o valor do tempo limite de conexão e o protocolo de rede. Este artigo usa os valores padrão para todas as opções.

3. Depois de preencher todos os campos, selecione **Conectar**.

### <a name="examples-of-successful-connections"></a>Exemplos de conexões bem-sucedidas

Para verificar se a conexão do SQL Server foi bem-sucedida, expanda e explore os objetos no **Pesquisador de Objetos**. Esses objetos são diferentes dependendo do tipo de servidor ao qual você escolha conectar-se. 

* Conectando-se a um SQL Server local – neste caso, ao NODE5\SQL2016ST: ![Conectando-se a um servidor local](media/connect-query-sql-server/connect-on-prem.png)

* Conectando-se ao banco de dados SQL do Azure – neste caso, ao msftestserver.database.windows.net: ![Conectando-se a um banco de dados SQL do Azure](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > Neste tutorial, você já usou a *Autenticação do Windows* para conectar-se ao SQL Server local, mas esse método não é compatível com o banco de dados SQL do Azure. Como tal, essa imagem mostra o uso da autenticação do SQL para se conectar ao banco de dados SQL do Azure. Para obter mais informações, confira [Autenticação local do SQL](../../relational-databases/security/choose-an-authentication-mode.md) e [Autenticação do SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#access-management). 

## <a name="create-a-database"></a>Criar um banco de dados

Crie um banco de dados chamado TutorialDB seguindo estas etapas:

1. Clique com o botão direito do mouse na instância do servidor no Pesquisador de Objetos e selecione **Nova Consulta**:

   ![O link de nova consulta](media/connect-query-sql-server/newquery.png)

2. Cole o seguinte snippet de código T-SQL na janela de consulta: 

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

3. Para executar a consulta, selecione **Executar** (ou F5 no teclado).

   ![O comando Executar](media/connect-query-sql-server/execute.png)
  
    Depois que a consulta for concluída, o novo banco de dados TutorialDB aparecerá na lista de bancos de dados no Pesquisador de Objetos. Se ele não for exibido, clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Atualizar**.  

## <a name="create-a-table-in-the-new-database"></a>Criar uma tabela no novo banco de dados

Nesta seção, você criará uma tabela no banco de dados TutorialDB recém-criado. Como o editor de consultas ainda está no contexto do banco de dados *mestre*, mude o contexto de conexão para o banco de dados *TutorialDB* executando as seguintes etapas:

1. Selecione o banco de dados desejado na lista suspensa de bancos de dados, conforme é mostrado aqui: 

   ![Alterar banco de dados](media/connect-query-sql-server/changedb.png)

2. Cole o seguinte snippet de código T-SQL na janela de consulta, selecione-o e, em seguida, escolha **Executar** (ou F5 no teclado).  
   Você pode substituir o texto existente na janela de consulta ou acrescentá-lo no final. Para executar tudo na janela de consulta, selecione **Executar**. Se você acrescentou o texto, o ideal será executar apenas a parte do texto; portanto, realce essa parte e, em seguida, escolha **Executar**.  
  
   ```sql
   USE [TutorialDB]
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

Depois que a consulta for concluída, a nova tabela Clientes será exibida na lista de tabelas no Pesquisador de Objetos. Se a tabela não for exibida, clique com o botão direito do mouse no nó **TutorialDB** > **Tabelas** no Pesquisador de Objetos e selecione **Atualizar**.

## <a name="insert-rows-into-the-new-table"></a>Inserir linhas na nova tabela

Insira algumas linhas na tabela Clientes que você já criou. Para fazer isso, cole o seguinte snippet de código T-SQL na janela de consulta e, em seguida, selecione **Executar**:

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

## <a name="query-the-table-and-view-the-results"></a>Consultar a tabela e exibir os resultados

Os resultados de uma consulta são exibidos abaixo da janela de texto de consulta. Para consultar a tabela Clientes e exibir as linhas que já foram inseridas, siga estas etapas:

1. Cole o seguinte snippet de código T-SQL na janela de consulta e, em seguida, selecione **Executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    Os resultados da consulta são exibidos na área em que o texto foi inserido: 

   ![A lista de resultados](media/connect-query-sql-server/queryresults.png)

2. Modifique a maneira em que os resultados são apresentados selecionando uma das seguintes opções:

     ![Três opções para exibir os resultados da consulta](media/connect-query-sql-server/results.png)

    * O botão do meio exibe os resultados na **Exibição em Grade**, que é a opção padrão. 
    * O primeiro botão exibe os resultados na **Exibição de Texto**, conforme é mostrado na imagem na próxima seção.
    * O terceiro botão permite salvar os resultados em um arquivo cuja extensão é .rpt por padrão.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Verificar as propriedades da conexão usando a tabela da janela de consulta

Você pode encontrar informações sobre as propriedades de conexão nos resultados da sua consulta. Depois de executar na etapa anterior a consulta já mencionada, examine as propriedades de conexão na parte inferior da janela de consulta.

* É possível determinar o servidor e o banco de dados aos quais você está conectado e o nome de usuário que você usa.
* Também é possível exibir a duração da consulta e o número de linhas retornadas pela consulta executada anteriormente.

    ![Propriedades da conexão](media/connect-query-sql-server/connectionproperties.png)

    > [!Note]
    > Na imagem, os resultados são exibidos em **Exibição de Texto**.

## <a name="change-the-server-based-on-the-query-window"></a>Alterar o servidor com base na janela de consulta

É possível alterar o servidor ao qual a janela de consulta atual está conectada seguindo estas etapas:

1. Clique com o botão direito do mouse na janela de consulta e, em seguida, selecione **Conexão** > **Alterar conexão**. A janela **Conectar-se ao servidor** será aberta novamente.

2. Altere o servidor que usa sua consulta.

   ![O comando Alterar Conexão](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > Esta ação altera apenas o servidor ao qual a janela de consulta está conectada, não o servidor que o Pesquisador de Objetos usa.

## <a name="azure-data-studio"></a>Azure Data Studio

Você também pode se conectar e consultar o [SQL Server](../../azure-data-studio/quickstart-sql-server.md), um [Banco de Dados SQL do Azure](../../azure-data-studio/quickstart-sql-database.md) e [Data warehouses SQL do Azure](../../azure-data-studio/quickstart-sql-dw.md) usando o Azure Data Studio.

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Esses artigos ajudam nos diversos recursos disponíveis no SSMS. Estes artigos ensinam a administrar os componentes do SSMS e a encontrar os recursos que você usa com regularidade.

* [Script](scripting-ssms.md)
* [Usando modelos no SSMS](../template/templates-ssms.md)
* [Configuração do SSMS](ssms-configuration.md)
* [Mais dicas e truques para usar o SSMS](ssms-tricks.md)
* [Azure Data Studio](../../azure-data-studio/download.md)