---
title: 'Início Rápido: Conectar e consultar o SQL Server'
titleSuffix: Azure Data Studio
description: Este guia de início rápido mostra como usar o Azure Data Studio para conectar-se ao SQL Server e executar uma consulta
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: 4117d8c16e96252f792e14d282d285527008874f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959390"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Início Rápido: Conectar e consultar o SQL Server usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Este guia de início rápido mostra como usar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar ao SQL Server e, em seguida, usar instruções T-SQL (Transact-SQL) para criar o *TutorialDB* usado em tutoriais [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="prerequisites"></a>Prerequisites

Para concluir este guia de início rápido, você precisa de [!INCLUDE[name-sos](../includes/name-sos-short.md)] e acesso a um SQL Server.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).

Se você não tiver acesso a um SQL Server, selecione a plataforma dentre os links a seguir (lembre-se do Logon e da Senha do SQL):
- [Windows – Baixar o SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS – Baixar o SQL Server 2017 no Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux – Baixar SQL Server 2017 Developer](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) Edition – você só precisa seguir as etapas para *Criar e Consultar Dados*.


## <a name="connect-to-a-sql-server"></a>Conectar a um SQL Server

   
1. Inicie o **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .
1. Na primeira vez que você executar o [!INCLUDE[name-sos](../includes/name-sos-short.md)], a página **Bem-vindo** deverá se abrir. Se você não vir a página **Bem-vindo**, selecione **Ajuda** > **Bem-vindo**. Selecione **Nova Conexão** para abrir o painel de **Conexão**:
   
   ![Ícone de Nova Conexão](media/quickstart-sql-server/new-connection-icon.png)

1. Este artigo usa o *Logon do SQL*, mas há suporte para a *Autenticação do Windows*. Preencha os campos da seguinte maneira:
 
    - **Nome do Servidor:** localhost
    - **Tipo de Autenticação:** Logon do SQL  
    - **Nome de Usuário:** O nome de usuário para o SQL Server  
    - **Senha:** Senha do SQL Server  
    - **Nome do Banco de Dados:** deixe este campo em branco 
    - **Grupo de Servidores:** \<Padrão\>  

   ![Nova Tela de Conexão](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Criar um banco de dados

As etapas a seguir criam outro banco de dados denominado **TutorialDB**:

1. Clique com o botão direito do mouse no servidor, **localhost** e selecione **Nova consulta**.
1. Cole o snippet a seguir na janela de consultas: 

   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
      CREATE DATABASE [TutorialDB];
   GO
   IF SERVERPROPERTY('ProductVersion') > '12'
       ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON;
   GO
   ```
1. Para executar a consulta, clique em **Executar**.

Depois que a consulta for concluída, o novo **TutorialDB** aparecerá na lista de bancos de dados. Se ele não aparecer, clique com o botão direito do mouse no nó **Banco de Dados** e selecione **Atualizar**.


## <a name="create-a-table"></a>Criar uma tabela

O editor de consultas ainda está conectado ao banco de dados *mestre*, mas queremos criar uma tabela no banco de dados *TutorialDB*. 

1. Altere o contexto de conexão para **TutorialDB**:

   ![Alterar contexto](media/quickstart-sql-server/change-context.png)



1. Cole o snippet a seguir na janela de consultas e clique em **Executar**:

   > [!NOTE]
   > Você pode acrescentar à consulta anterior ou substituí-la no editor. Observe que clicar em **Executar** executa apenas a consulta selecionada. Se nada estiver selecionado, clicar em **Executar** executará todas as consultas no editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
      DROP TABLE dbo.Customers;
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
       CustomerId  int NOT NULL PRIMARY KEY, -- primary key column
       Name        nvarchar(50) NOT NULL,
       Location    nvarchar(50) NOT NULL,
       Email       nvarchar(50) NOT NULL
   );
   GO
   ```

Depois que a consulta for concluída, a nova tabela **Clientes** aparece na lista de tabelas. Talvez seja necessário clicar com o botão direito do mouse no nó **TutorialDB > Tabelas** e selecionar **Atualizar**.

## <a name="insert-rows"></a>Inserir linhas

- Cole o snippet a seguir na janela de consultas e clique em **Executar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId], [Name], [Location], [Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```



## <a name="view-the-data-returned-by-a-query"></a>Exibir os dados retornados por uma consulta
1. Cole o snippet a seguir na janela de consultas e clique em **Executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecionar resultados](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Próximas etapas
Agora que você se conectou com êxito ao SQL Server e executou uma consulta, experimente o [Tutorial do editor de código](tutorial-sql-editor.md).


