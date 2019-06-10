---
title: 'Início Rápido: Conectar e consultar um SQL Data Warehouse do Azure'
titleSuffix: Azure Data Studio
description: Este início rápido mostra como usar o Studio de dados do Azure para se conectar a um SQL Data Warehouse do Azure e executar uma consulta
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: f98f6be4502254910b5c144f08a95181ccf1b2a7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800269"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Início Rápido: Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar e consultar dados no Azure SQL Data Warehouse

Neste início rápido demonstra como usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar ao Azure SQL data warehouse e, em seguida, usar instruções Transact-SQL para criar, inserir e selecionar dados. 

## <a name="prerequisites"></a>Prerequisites
Para concluir este início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e um Azure SQL data warehouse.

- [Instale [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se você ainda não tiver um SQL data warehouse, consulte [criar um SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Lembre-se o nome do servidor e credenciais de logon!


## <a name="connect-to-your-data-warehouse"></a>Conectar-se ao data warehouse

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para estabelecer uma conexão ao seu servidor do Azure SQL Data Warehouse.

1. Na primeira vez que você executar [!INCLUDE[name-sos](../includes/name-sos-short.md)] as **Conexão** deve abrir a página. Se você não vir as **Conexão** , clique em **Adicionar Conexão**, ou o **nova Conexão** ícone no **servidores** barra lateral:
   
   ![Novo ícone de Conexão](media/quickstart-sql-dw/new-connection-icon.png)

2. Este artigo usa *logon do SQL*, mas *autenticação do Windows* também tem suporte. Preencha os campos da seguinte maneira usando o nome do servidor, nome de usuário e senha para *sua* servidor SQL do Azure:

   | Configuração       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve ser algo parecido com isto: **sqldwsample.database.windows.net** |
   | **Autenticação** | Logon do SQL| Autenticação do SQL é usada neste tutorial. |
   | **Nome de usuário** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Selecione Sim se você não quiser inserir a senha de cada vez. |
   | **Nome do banco de dados** | *Deixe em branco* | O nome do banco de dados ao qual se conectar. |
   | **Grupo de servidores** | Selecione <Default> | Se você criou um grupo de servidores, você pode definir para um grupo de servidores específicos. | 

   ![Novo ícone de Conexão](media/quickstart-sql-dw/new-connection-screen.png) 

3. Se seu servidor não tiver uma regra de firewall permitindo o estúdio de dados do Azure para se conectar, o **criar nova regra de firewall** é aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, consulte [regras de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nova regra de firewall](media/quickstart-sql-dw/firewall.png)  

4. Depois de se conectar com êxito o servidor é aberto na *servidores* barra lateral.

## <a name="create-the-tutorial-data-warehouse"></a>Criar o tutorial de data warehouse
1. Clique com o botão direito no seu servidor, no Pesquisador de objetos e selecione **nova consulta.**

1. Cole o trecho a seguir no editor de consultas e clique em **executar**:

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>Criar uma tabela

O editor de consultas ainda está conectado para o *mestre* banco de dados, mas podemos deseja criar uma tabela na *TutorialDB* banco de dados. 

1. Alterar o contexto de conexão para **TutorialDB**:

   ![Contexto de alteração](media/quickstart-sql-database/change-context.png)


1. Cole o trecho a seguir no editor de consultas e clique em **executar**:

   > [!NOTE]
   > Você pode anexá-lo para ou substituir a consulta anterior no editor. Observe que clicar em **executar** executa somente a consulta selecionada. Se nada estiver selecionado, clicando em **executar** executa todas as consultas no editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Inserir linhas

1. Cole o trecho a seguir no editor de consultas e clique em **executar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>Exibir o resultado
1. Cole o trecho a seguir no editor de consultas e clique em **executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecione resultados](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Limpar recursos

Outros artigos nesta coleção aproveitam esse início rápido. Se você planeja continuar trabalhando com inícios rápidos subsequentes, não limpe os recursos criados neste início rápido. Se você não planeja continuar, use as etapas a seguir para excluir os recursos criados neste início rápido no portal do Azure.
Limpe recursos excluindo os grupos de recursos que você não precisa mais. Para obter detalhes, consulte [limpar os recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito para um Azure SQL data warehouse e executou uma consulta, experimente o [tutorial do editor de código](tutorial-sql-editor.md).
