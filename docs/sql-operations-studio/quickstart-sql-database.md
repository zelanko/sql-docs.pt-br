---
title: 'Guia de início rápido: Conectar e consultar um banco de dados SQL do Azure usando o SQL Operations Studio (versão prévia) | Microsoft Docs'
description: Este início rápido mostra como usar o SQL Operations Studio (versão prévia) para se conectar a um banco de dados SQL e executar uma consulta
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 5470e19da9d8641a1337f0f8162fe0a1789820dd
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982258"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Início rápido: Usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar e consultar o banco de dados SQL do Azure

Neste início rápido demonstra como usar *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* para se conectar a um banco de dados SQL do Azure e, em seguida, usar instruções Transact-SQL (T-SQL) para criar as *TutorialDB* usados em [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

## <a name="prerequisites"></a>Prerequisites

Para concluir este início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e um servidor SQL Azure.

- [Instale [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se você ainda não tiver um servidor do SQL Azure, conclua um dos seguintes tutoriais de banco de dados SQL (Lembre-se o nome do servidor e credenciais de logon!):

- [Criar banco de dados – Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Criar banco de dados – CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Criar banco de dados – PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectar-se ao seu servidor de banco de dados SQL

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para estabelecer uma conexão ao seu servidor de banco de dados SQL.

1. Na primeira vez que você executar [!INCLUDE[name-sos](../includes/name-sos-short.md)] as **Conexão** deve abrir a página. Se você não vir as **Conexão** , clique em **Adicionar Conexão**, ou o **nova Conexão** ícone no **servidores** barra lateral:
   
   ![Novo ícone de Conexão](media/quickstart-sql-database/new-connection-icon.png)

2. Este artigo usa *logon do SQL*, mas *autenticação do Windows* também tem suporte. Preencha os campos da seguinte maneira usando o nome do servidor, nome de usuário e senha para *sua* servidor SQL do Azure:

   | Configuração       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve ser algo parecido com isto: **servername.database.windows.net** |
   | **Autenticação** | Logon do SQL| Autenticação do SQL é usada neste tutorial. |
   | **Nome de usuário** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Selecione Sim se você não quiser inserir a senha de cada vez. |
   | **Nome do banco de dados** | *Deixe em branco* | O nome do banco de dados que você deseja se conectar. |
   | **Grupo de servidores** | Selecione <Default> | Se você criou um grupo de servidores, você pode definir para um grupo de servidores específicos. | 

   ![Novo ícone de Conexão](media/quickstart-sql-database/new-connection-screen.png)  

3. Se seu servidor não tiver uma regra de firewall permitindo que o SQL Operations Studio para se conectar, o **criar nova regra de firewall** é aberto. Preencha o formulário para criar uma nova regra de firewall. Para obter detalhes, consulte [regras de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nova regra de firewall](media/quickstart-sql-database/firewall.png)  

4. Depois de se conectar com êxito o servidor é aberto na *servidores* barra lateral.

## <a name="create-the-tutorial-database"></a>Criar o banco de dados do tutorial

As seções a seguir criam o *TutorialDB* banco de dados que é usado em vários [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

1. Clique com o botão direito no seu servidor SQL do Azure, na barra lateral de servidores e selecione **nova consulta.**

1. Cole o trecho a seguir no editor de consultas e clique em **executar**:

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
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Inserir linhas

- Cole o trecho a seguir no editor de consultas e clique em **executar**:

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
1. Cole o trecho a seguir no editor de consultas e clique em **executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecione resultados](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>Limpar recursos

Outros artigos nesta coleção aproveitam esse início rápido. Se você planeja continuar trabalhando com inícios rápidos subsequentes, não limpe os recursos criados neste início rápido. Se você não planeja continuar, use as etapas a seguir para excluir os recursos criados neste início rápido no portal do Azure.
Limpe recursos excluindo os grupos de recursos que você não precisa mais. Para obter detalhes, consulte [limpar os recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Próximas etapas

Agora que você se conectou com êxito para um banco de dados SQL do Azure e executou uma consulta, experimente o [tutorial do editor de código](tutorial-sql-editor.md).
