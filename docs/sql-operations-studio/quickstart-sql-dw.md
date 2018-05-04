---
title: 'Início rápido: Conectar e consultar um Azure SQL Data Warehouse usando o Studio de operações do SQL (visualização) | Microsoft Docs'
description: Este guia de início rápido mostra como usar o Studio de operações do SQL (visualização) para se conectar a um banco de dados SQL e executar uma consulta
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: eeb496f814546034ac4e7d90cb0f1f734bf5bb47
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Início rápido: Usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar e consultar dados no Azure SQL Data Warehouse

Este guia de início rápido demonstra como usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar ao SQL Azure data warehouse e, em seguida, usar instruções Transact-SQL para criar, inserir e selecione os dados. 

## <a name="prerequisites"></a>Prerequisites
Para concluir este guia de início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e um data warehouse do SQL Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se você ainda não tiver um SQL data warehouse, consulte [criar um Data Warehouse do SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Lembre-se o nome do servidor e credenciais de logon!


## <a name="connect-to-your-data-warehouse"></a>Conecte-se ao data warehouse

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para estabelecer uma conexão ao seu servidor do Azure SQL Data Warehouse.

1. Na primeira vez que você executar [!INCLUDE[name-sos](../includes/name-sos-short.md)] o **Conexão** deve abrir a página. Se você não vir o **Conexão** , clique em **Adicionar Conexão**, ou o **nova Conexão** ícone o **servidores** barra lateral:
   
   ![Novo ícone de Conexão](media/quickstart-sql-dw/new-connection-icon.png)

2. Este artigo usa *logon SQL*, mas *autenticação do Windows* também tem suporte. Preencha os campos da seguinte maneira usando o nome do servidor, o nome de usuário e a senha para *sua* servidor SQL do Azure:

   | Configuração       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve ser semelhante a esta: **sqldwsample.database.windows.net** |
   | **Autenticação** | Logon do SQL| Autenticação do SQL é usada neste tutorial. |
   | **Nome de usuário** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Selecione Sim se você não deseja digitar a senha cada vez. |
   | **Nome do banco de dados** | *Deixe em branco* | O nome do banco de dados ao qual se conectar. |
   | **Grupo de servidores** | Selecione <Default> | Se você criou um grupo de servidores, você pode definir para um grupo de servidores específicos. | 

   ![Novo ícone de Conexão](media/quickstart-sql-dw/new-connection-screen.png) 

3. Se o servidor não tiver uma regra de firewall permitindo operações de SQL Studio para se conectar, o **criar nova regra de firewall** é aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, consulte [as regras de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nova regra de firewall](media/quickstart-sql-dw/firewall.png)  

4. Depois de se conectar com êxito o servidor é aberto no *servidores* barra lateral.

## <a name="create-the-tutorial-data-warehouse"></a>Criar o tutorial de data warehouse
1. Clique com o botão direito no seu servidor, no Pesquisador de objetos e selecione **nova consulta.**

1. Cole o trecho a seguir no editor de consulta e clique em **executar**:

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

O editor de consulta ainda estiver conectado a *mestre* banco de dados, mas deseja criar uma tabela no *TutorialDB* banco de dados. 

1. Alterar o contexto de conexão para **TutorialDB**:

   ![Contexto de alteração](media/quickstart-sql-database/change-context.png)


1. Cole o trecho a seguir no editor de consulta e clique em **executar**:

   > [!NOTE]
   > Você pode anexá-lo para ou substitua a consulta anterior no editor. Observe que clicar nos **executar** executa somente a consulta selecionada. Se nada estiver selecionado, clicando em **executar** executa todas as consultas no editor.

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

1. Cole o trecho a seguir no editor de consulta e clique em **executar**:

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
1. Cole o trecho a seguir no editor de consulta e clique em **executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecione resultados](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Limpar recursos

Outros artigos nesta coleção incrementar este guia de início rápido. Se você planeja continuar a trabalhar com os tutoriais subsequentes, limpar os recursos criados neste guia de início rápido. Se você não planeja continuar, use as etapas a seguir para excluir recursos criados por este guia de início rápido no portal do Azure.
Limpe recursos excluindo os grupos de recursos que não é mais necessário. Para obter detalhes, consulte [limpar os recursos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito para um data warehouse do SQL Azure e executar uma consulta, experimente o [tutorial do editor de código](tutorial-sql-editor.md).