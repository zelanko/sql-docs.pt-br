---
title: "Início rápido: Conectar e consultar um banco de dados do SQL Azure usando o Studio de operações do SQL (visualização) | Microsoft Docs"
description: "Este guia de início rápido mostra como usar o Studio de operações do SQL (visualização) para se conectar a um banco de dados SQL e executar uma consulta"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0e2d48ed411f883a904decce5d836dde7aaa41b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Início rápido: Usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar e consultar o banco de dados do SQL Azure

Este guia de início rápido demonstra como usar  *[!INCLUDE[name-sos](../includes/name-sos-short.md)]*  para se conectar a um banco de dados do SQL Azure e, em seguida, usar instruções Transact-SQL (T-SQL) para criar o *TutorialDB* usados em [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

## <a name="prerequisites"></a>Prerequisites

Para concluir este guia de início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e um servidor do SQL Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se você ainda não tiver um servidor do SQL Azure, siga um dos seguintes tutoriais do banco de dados SQL (Lembre-se o nome do servidor e credenciais de logon!):

- [Criar banco de dados – Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Criar banco de dados – CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Criar banco de dados - PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conecte-se ao seu servidor de banco de dados SQL

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para estabelecer uma conexão ao seu servidor de banco de dados SQL.

1. Na primeira vez que você executar [!INCLUDE[name-sos](../includes/name-sos-short.md)] o **Conexão** deve abrir a página. Se o **Conexão** página não abre, clique no **nova Conexão** ícone o **servidores** barra lateral:
   
   ![Novo ícone de Conexão](media/quickstart-sql-database/new-connection-icon.png)

2. Este artigo usa *logon SQL*, mas *autenticação do Windows* também tem suporte. Preencha os campos da seguinte maneira:

   | Configuração       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve ser semelhante a esta: **servername.database.windows.net** |
   | **Autenticação** | Logon do SQL| Autenticação do SQL é usada neste tutorial. |
   | **User name** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Selecione Sim se você não deseja digitar a senha cada vez. |
   | **Nome do banco de dados** | *Deixe em branco* | O nome do banco de dados que você deseja se conectar. |
   | **Grupo de servidores** | Selecione<Default> | Se você criou um grupo de servidores, você pode definir para um grupo de servidores específicos. | 

   ![Novo ícone de Conexão](media/quickstart-sql-database/new-connection-screen.png)  

3. Se você receber um erro sobre o firewall, você precisa criar uma regra de firewall. Para criar uma regra de firewall, consulte [as regras de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

4. Depois de se conectar com êxito o servidor aparecerá no *servidores* barra lateral.

## <a name="create-the-tutorial-database"></a>Criar o banco de dados do tutorial

O *TutorialDB* banco de dados é usado em vários [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

1. Clique com o botão direito no seu servidor do SQL Azure na barra lateral de servidores e selecione **nova consulta.**

1. Cole o trecho a seguir no editor de consultas.

   ```sql
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

1. Para executar a consulta, clique em **executar**.


## <a name="create-a-table"></a>Criar uma tabela

O editor de consulta ainda estiver conectado a *mestre* banco de dados, mas deseja criar uma tabela no *TutorialDB* banco de dados. 

1. Alterar o contexto de conexão para **TutorialDB**:

   ![Contexto de alteração](media/quickstart-sql-database/change-context.png)



1. Cole o trecho a seguir no editor de consultas.

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
1. Para executar a consulta, clique em **executar**.

## <a name="insert-rows"></a>Inserir linhas

1. Cole o trecho a seguir no editor de consultas:
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

1. Para executar a consulta, clique em **executar**.

## <a name="view-the-result"></a>Exibir o resultado
1. Cole o trecho a seguir no editor de consultas.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Para executar a consulta, clique em **executar**.

   ![Selecione resultados](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>Limpar recursos

Outros artigos nesta coleção incrementar este guia de início rápido. Se você planeja continuar a trabalhar com os tutoriais subsequentes, limpar os recursos criados neste guia de início rápido. Se você não planeja continuar, use as etapas a seguir para excluir recursos criados por este guia de início rápido no portal do Azure.
Limpe recursos excluindo os grupos de recursos que não é mais necessário. Para obter detalhes, consulte [limpar os recursos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito para um banco de dados do SQL Azure e executar uma consulta, experimente o [tutorial do editor de código](tutorial-sql-editor.md).
