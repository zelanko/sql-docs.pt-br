---
title: Conectar-se ao Azure Synapse Analytics e consultá-lo
description: Este início rápido mostra como usar o Azure Data Studio para se conectar a um pool de SQL dedicado do Azure Synapse Analytics.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.reviewer: alayu, jrasnick
ms.custom: seodec18; seo-lt-2019
ms.date: 10/15/2020
ms.openlocfilehash: f0d6ba76868bb1b8a226145b2aa1306db46baa17
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115870"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-data-using-dedicated-sql-pool-in-azure-synapse-analytics"></a>Início Rápido: Usar o Azure Data Studio para se conectar e consultar dados usando o pool de SQL dedicado no Azure Synapse Analytics

Este início rápido mostra como usar o Azure Data Studio para se conectar a um pool de SQL dedicado do Azure Synapse Analytics.

## <a name="prerequisites"></a>Pré-requisitos
Para concluir este início rápido, você precisa do Azure Data Studio e de um pool de SQL dedicado no Azure Synapse Analytics.

- [Instale o Azure Data Studio](./download-azure-data-studio.md).

Se ainda não tiver um pool de SQL dedicado, confira [Criar um pool de SQL dedicado](/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Lembre-se do nome do servidor e das credenciais de logon.


## <a name="connect-to-your-dedicated-sql-pool"></a>Conectar-se ao seu pool de SQL dedicado

Use o Azure Data Studio para estabelecer uma conexão com o servidor do Azure Synapse Analytics.

1. Na primeira vez que você executar o Azure Data Studio, a página **Conexão** deverá abrir. Se você não vir a página **Conexão**, clique em **Adicionar Conexão** ou no ícone **Nova Conexão** na barra lateral **SERVIDORES**:
   
   ![Ícone de Nova Conexão](media/quickstart-sql-dw/new-connection-icon.png)

2. Este artigo usa o *Logon do SQL*, mas também há suporte para a *Autenticação do Windows*. Preencha os campos da seguinte maneira usando o nome do servidor, o nome de usuário e a *sua* senha para o SQL Server do Azure:

   |   Configuração    | Valor sugerido | Descrição |
   |--------------|-----------------|-------------| 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Por exemplo, o nome será parecido com este: **sqlpoolservername.database.windows.net**. |
   | **Autenticação** | Logon do SQL| A autenticação do SQL é usada neste tutorial. |
   | **Nome de usuário** | A conta do administrador do servidor | Esta é a conta que você especificou quando criou o servidor. |
   | **Senha (Logon do SQL)** | A senha para sua conta do administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou não | Selecione Sim se você não quiser inserir a senha a cada vez. |
   | **Nome do banco de dados** | *deixar em branco* | O nome do banco de dados ao qual conectar. |
   | **Grupo de Servidores** | Selecione <Default> | Se você criou um grupo de servidores, pode definir para um grupo de servidores específico. | 

3. Se o servidor não tiver uma regra de firewall que permita que o Azure Data Studio se conecte, o formulário **Criar nova regra de firewall** será aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, confira [Regras de firewall](/azure/sql-database/sql-database-firewall-configure).

4. Depois de se conectar com êxito, o servidor será aberto na barra lateral *Servidores*.

## <a name="create-a-database-in-your-dedicated-sql-pool"></a>Crie um banco de dados no seu pool de SQL dedicado

1. Clique com o botão direito do mouse no servidor no pesquisador de objetos, e selecione **Nova Consulta**.

2. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

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

O editor de consultas ainda está conectado ao banco de dados *mestre*, mas queremos criar uma tabela no banco de dados *TutorialDB*. 

1. Altere o contexto de conexão para **TutorialDB**:

2. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

   > [!NOTE]
   > Você pode acrescentar à consulta anterior ou substituí-la no editor. Ao clicar em **Executar**, apenas a consulta selecionada será executada. Se nada estiver selecionado, ao clicar em **Executar**, todas as consultas no editor serão executadas.

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

    :::image type="content" source="media/quickstart-sql-dw/create-table.png" alt-text="Crie uma tabela no banco de dados TutorialDB":::


## <a name="insert-rows"></a>Inserir linhas

1. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```

    :::image type="content" source="media/quickstart-sql-dw/create-rows.png" alt-text="Crie uma tabela no banco de dados TutorialDB":::

## <a name="view-the-result"></a>Exibir o resultado

1. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

2. Os resultados da consulta são exibidos:

    :::image type="content" source="media/quickstart-sql-dw/view-results.png" alt-text="Crie uma tabela no banco de dados TutorialDB":::


## <a name="clean-up-resources"></a>Limpar os recursos

Se você não pretende continuar trabalhando com os bancos de dados de amostras criados neste artigo, [exclua o grupo de recursos](/azure/azure/synapse-analytics/sql-data-warehouse/create-data-warehouse-portal#clean-up-resources).

## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito a um Azure Synapse Analytics e executou uma consulta, experimente o [Tutorial do editor de código](tutorial-sql-editor.md).