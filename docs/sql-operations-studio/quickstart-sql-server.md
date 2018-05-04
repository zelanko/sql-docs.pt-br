---
title: 'Início rápido: Conectar e consultar o SQL Server usando o Studio de operações do SQL (visualização) | Microsoft Docs'
description: Este guia de início rápido mostra como usar o Studio de operações do SQL (visualização) para se conectar ao SQL Server e executar uma consulta
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
ms.openlocfilehash: 287cd20b7db0a1b816211d48bc7a19c8f5066e8c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Início rápido: Conectar e consultar usando o SQL Server [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Este guia de início rápido mostra como usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar ao SQL Server e, em seguida, usar instruções Transact-SQL (T-SQL) para criar o *TutorialDB* usados em [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

## <a name="prerequisites"></a>Prerequisites

Para concluir este guia de início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e o acesso a um servidor SQL.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se você não tiver acesso a um SQL Server, selecione a plataforma os links a seguir (certifique-se de lembrar o logon do SQL e a senha!):
- [Windows – Baixar o SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS – Baixar o SQL Server 2017 no Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)
- [Linux - Download SQL Server 2017 Developer Edition](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-overview#install) -você precisa seguir as etapas até *criar e consultar dados*.


## <a name="connect-to-a-sql-server"></a>Conectar a um SQL Server

   
1. Iniciar **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**.
1. Na primeira vez que você executar *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* o **Conexão** caixa de diálogo é aberta. Se o **Conexão** não abre a caixa de diálogo, clique no **nova Conexão** ícone o **servidores** página:
   
   ![Novo ícone de Conexão](media/quickstart-sql-server/new-connection-icon.png)

1. Este artigo usa *logon SQL*, mas *autenticação do Windows* tem suporte. Preencha os campos da seguinte maneira:
 
    - **Nome do servidor:** localhost
    - **Tipo de autenticação:** logon do SQL  
    - **Nome de usuário:** nome de usuário para o SQL Server  
    - **Senha:** senha para o SQL Server  
    - **Nome do banco de dados:** deixe esse campo em branco 
    - **Grupo de servidores:** \<padrão\>  

   ![Nova tela de Conexão](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Criar um banco de dados

As seguintes etapas criam um banco de dados denominado **TutorialDB**:

1. Clique com o botão direito no seu servidor, **localhost**e selecione **nova consulta.**
1. Cole o trecho a seguir na janela de consulta: 

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

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```
1. Para executar a consulta, clique em **executar** .

Depois que a consulta é concluída, o novo **TutorialDB** aparece na lista de bancos de dados. Se você não estiver visível, clique com botão direito do **bancos de dados** nó e selecione **atualizar**.


## <a name="create-a-table"></a>Criar uma tabela

O editor de consulta ainda estiver conectado a *mestre* banco de dados, mas deseja criar uma tabela no *TutorialDB* banco de dados. 

1. Alterar o contexto de conexão para **TutorialDB**:

   ![Contexto de alteração](media/quickstart-sql-server/change-context.png)



1. Cole o trecho a seguir na janela de consulta e clique em **executar**:

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
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

Depois que a consulta é concluída, o novo **clientes** tabela aparece na lista de tabelas. Talvez seja necessário com o botão direito do **TutorialDB > tabelas** nó e selecione **atualizar**.

## <a name="insert-rows"></a>Inserir linhas

- Cole o trecho a seguir na janela de consulta e clique em **executar**:

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



## <a name="view-the-data-returned-by-a-query"></a>Exibir os dados retornados por uma consulta
1. Cole o trecho a seguir na janela de consulta e clique em **executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecione resultados](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Próximas etapas
Agora que você se conectou com êxito do SQL Server e execute uma consulta, experimente o [tutorial do editor de código](tutorial-sql-editor.md).


