---
title: 'Início Rápido: Conectar e consultar um banco de dados SQL do Azure'
titleSuffix: Azure Data Studio
description: Este início rápido mostra como usar o Studio de dados do Azure para se conectar a um banco de dados SQL e executar uma consulta
ms.custom: seodec18
ms.date: 12/21/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: d368f38589530f27db98c3c61b9cec4610818ae4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63255967"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Início Rápido: Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar e consultar o banco de dados SQL do Azure

Neste início rápido, você usará [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar a um servidor de banco de dados SQL. Em seguida, você vai executar instruções Transact-SQL (T-SQL) para criar e consultar o banco de dados TutorialDB, que é usado em outros [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

## <a name="prerequisites"></a>Prerequisites

Para concluir este início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e um servidor de banco de dados SQL.

- [Instalar o [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

Se você não tiver um servidor SQL Azure, conclua um dos inícios rápidos de banco de dados SQL a seguir. Lembre-se o nome totalmente qualificado do servidor e as credenciais para etapas posteriores de logon:

- [Criar banco de dados – Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Criar banco de dados – CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Criar banco de dados – PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectar-se ao seu servidor de banco de dados SQL

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para estabelecer uma conexão ao seu servidor de banco de dados SQL.

1. Na primeira vez que você executar [!INCLUDE[name-sos](../includes/name-sos-short.md)] as **Conexão** deve abrir a página. Se você não vir as **Conexão** página, selecione **Adicionar Conexão**, ou o **nova Conexão** ícone no **servidores** barra lateral:
   
   ![Novo ícone de Conexão](media/quickstart-sql-database/new-connection-icon.png)

2. Este artigo usa SQL entrar, mas também dá suporte à autenticação do Windows. Preencha os campos a seguir usando o nome do servidor, nome de usuário e senha para o Azure SQL server:

   | Configuração       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Algo como: **servername.database.windows.net**. |
   | **Autenticação** | Logon do SQL| Este tutorial usa a autenticação do SQL. |
   | **Nome de usuário** | O nome de usuário de conta de administrador do servidor | O nome de usuário da conta usada para criar o servidor. |
   | **Senha (logon do SQL)** | A senha de conta de administrador do servidor | A senha da conta usada para criar o servidor. |
   | **Salvar senha?** | Sim ou Não | Selecione **Sim** se você não quiser inserir a senha de cada vez. |
   | **Nome do banco de dados** | *Deixe em branco* | Você só estiver se conectando ao servidor aqui. |
   | **Grupo de servidores** | Selecione <Default> | Você pode definir esse campo para um grupo de servidor específico que você criou. | 

   ![Novo ícone de Conexão](media/quickstart-sql-database/new-connection-screen.png)  

3. Selecione **Conectar**.

4. Se seu servidor não tiver uma regra de firewall permitindo o estúdio de dados do Azure para se conectar, o **criar nova regra de firewall** é aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, consulte [regras de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nova regra de firewall](media/quickstart-sql-database/firewall.png)  

Depois de se conectar com êxito, o servidor é aberto na **servidores** barra lateral.

## <a name="create-the-tutorial-database"></a>Criar o banco de dados do tutorial

As seções a seguir criam o banco de dados TutorialDB usado em outros [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

1. Clique com botão direito no servidor SQL do Azure na **servidores** barra lateral e selecione **nova consulta**.

1. Cole esse SQL no editor de consultas.

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

1. Na barra de ferramentas, selecione **executar**. As notificações aparecem na **mensagens** painel mostrando o progresso da consulta.

## <a name="create-a-table"></a>Criar uma tabela

O editor de consultas está conectado a **mestre** banco de dados, mas podemos deseja criar uma tabela na **TutorialDB** banco de dados. 

1. Conectar-se para o **TutorialDB** banco de dados.

   ![Contexto de alteração](media/quickstart-sql-database/change-context2.png)



1. Criar um `Customers` tabela. 

   Substitua a consulta anterior no editor de consultas com este e selecione **executar**.

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


## <a name="insert-rows-into-the-table"></a>Inserir linhas na tabela

Substitua a consulta anterior com este e selecione **executar**.

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

## <a name="view-the-result"></a>Exibir o resultado

Substitua a consulta anterior com este e selecione **executar**.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

Exibirem os resultados da consulta:

   ![Selecione resultados](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>Limpar recursos

Os artigos de início rápido posteriores aproveitam os recursos criados aqui. Se você planeja trabalhar com estes artigos, certifique-se para não excluir esses recursos. Caso contrário, no portal do Azure, exclua os recursos que você não precisa mais. Para obter detalhes, consulte [limpar os recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito a um banco de dados SQL do Azure e executar uma consulta, tente as [tutorial do editor de código](tutorial-sql-editor.md).
