---
title: 'Início Rápido: Conectar e consultar um SQL Data Warehouse do Azure'
titleSuffix: Azure Data Studio
description: Este guia de início rápido mostra como usar o Azure Data Studio para conectar-se a um SQL Data Warehouse do Azure e executar uma consulta
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: 810d03ab97fd584e1ddaab45e06a21377b81685d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959405"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Início Rápido: Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectar-se ao SQL Data Warehouse do Azure e consultá-lo

Este guia de início rápido demonstra como usar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar ao SQL Data Warehouse do Azure e, em seguida, usar instruções Transact-SQL para criar, inserir e selecionar dados. 

## <a name="prerequisites"></a>Prerequisites
Para concluir este guia de início rápido, você precisa de [!INCLUDE[name-sos](../includes/name-sos-short.md)] e de um SQL Data Warehouse do Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).

Se você ainda não tiver um SQL data warehouse, confira [Criar um SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Lembre-se do nome do servidor e das credenciais de logon.


## <a name="connect-to-your-data-warehouse"></a>Como conectar-se ao data warehouse

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para estabelecer uma conexão com o servidor do SQL Data Warehouse do Azure.

1. Na primeira vez que você executar o [!INCLUDE[name-sos](../includes/name-sos-short.md)], a página **Conexão** deverá se abrir. Se você não vir a página **Conexão**, clique em **Adicionar Conexão** ou no ícone **Nova Conexão** na barra lateral **SERVIDORES**:
   
   ![Ícone de Nova Conexão](media/quickstart-sql-dw/new-connection-icon.png)

2. Este artigo usa o *Logon do SQL*, mas também há suporte para a *Autenticação do Windows*. Preencha os campos da seguinte maneira usando o nome do servidor, o nome de usuário e a *sua* senha para o SQL Server do Azure:

   | Configuração       | Valor sugerido | Descrição |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve ser algo assim: **sqldwsample.database.windows.net** |
   | **Autenticação** | Logon do SQL| A autenticação do SQL é usada neste tutorial. |
   | **User name** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Selecione Sim se você não quiser inserir a senha a cada vez. |
   | **Nome do banco de dados** | *deixar em branco* | O nome do banco de dados ao qual se conectar. |
   | **Grupo de Servidores** | Selecione <Default> | Se você criou um grupo de servidores, pode definir para um grupo de servidores específico. | 

   ![Ícone de Nova Conexão](media/quickstart-sql-dw/new-connection-screen.png) 

3. Se o servidor não tiver uma regra de firewall que permita que o Azure Data Studio se conecte, o formulário **Criar nova regra de firewall** será aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, confira [Regras de firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nova regra de firewall](media/quickstart-sql-dw/firewall.png)  

4. Depois de se conectar com êxito, o servidor será aberto na barra lateral *Servidores*.

## <a name="create-the-tutorial-data-warehouse"></a>Criar o data warehouse do tutorial
1. Clique com o botão direito do mouse no servidor no pesquisador de objetos e selecione **Nova Consulta**.

1. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

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

   ![Alterar contexto](media/quickstart-sql-database/change-context.png)


1. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

   > [!NOTE]
   > Você pode acrescentar à consulta anterior ou substituí-la no editor. Observe que clicar em **Executar** executa apenas a consulta selecionada. Se nada estiver selecionado, clicar em **Executar** executará todas as consultas no editor.

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


## <a name="view-the-result"></a>Exibir o resultado
1. Cole o snippet a seguir no editor de consultas e clique em **Executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecionar resultados](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Limpar os recursos

Outros artigos nesta coleção se baseiam neste guia de início rápido. Se você planeja continuar trabalhando com guias de início rápido subsequentes, não limpe os recursos criados neste guia de início rápido. Se você não planeja continuar, use as etapas a seguir para excluir os recursos criados por este guia de início rápido no portal do Azure.
Limpe os recursos excluindo os grupos de recursos de que você não precisa mais. Para obter detalhes, confira [Limpar recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito a um SQL Data Warehouse do Azure e executou uma consulta, experimente o [Tutorial do editor de código](tutorial-sql-editor.md).
