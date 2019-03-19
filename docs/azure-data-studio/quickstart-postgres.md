---
title: 'Início Rápido: Conectar e consultar PostgreSQL'
titleSuffix: Azure Data Studio
description: Neste início rápido mostra como usar o Studio de dados do Azure para se conectar ao PostgreSQL e executar uma consulta
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
manager: craigg
ms.openlocfilehash: dbf7b427c8c978538370a576aa50c35dd15417cf
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161882"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>Início Rápido: Conectar e consultar PostgreSQL usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Neste início rápido mostra como usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] conectem Postgres, e, em seguida, usar instruções SQL para criar o banco de dados *tutorialdb* e consultá-lo.

## <a name="prerequisites"></a>Prerequisites

Para concluir este início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)], a extensão do PostgreSQL para [! INCLUIR[sos nome](../includes/name-sos-short.md)e o acesso a um servidor PostgreSQL.

- [Instale [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).
- [Instalar a extensão do PostgreSQL para o Azure Data Studio](postgres-extension.md).
- [Instalar o PostgreSQL](https://www.postgresql.org/download/). (Como alternativa, você pode criar um banco de dados do Postgres na nuvem usando [postgres az backup](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>Conectar-se ao PostgreSQL

1. Inicie **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**.

2. Na primeira vez que você inicie [!INCLUDE[name-sos](../includes/name-sos-short.md)] as **Conexão** caixa de diálogo é aberta. Se o **Conexão** caixa de diálogo não abre, clique no **nova Conexão** ícone no **servidores** página:

   ![Novo ícone de Conexão](media/quickstart-postgresql/new-connection-icon.png)

3. No formulário pop-up, vá para **tipo de Conexão** e selecione **PostgreSQL** na lista suspensa.


4. Preencha os campos restantes usando o nome do servidor, nome de usuário e senha para seu servidor PostgreSQL. 

   ![Nova tela de Conexão](media/quickstart-postgresql/new-connection-screen.png)  

   | Configuração       | Valor de exemplo | Descrição |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | localhost | O nome do servidor totalmente qualificado |
   | **Nome de usuário** | postgres | O nome de usuário que você deseja fazer logon com. |
   | **Senha (logon do SQL)** | *password* | A senha para a conta que você está fazendo logon em com. |
   | **Senha** | *Verificar* | Essa caixa de seleção se você não quiser inserir a senha sempre que você se conectar. |
   | **Nome do banco de dados** | \<Default\> | Preencha este se você quiser que a conexão para especificar um banco de dados. |
   | **Grupo de servidor** | \<Default\> | Essa opção permite que você atribuir essa conexão a um grupo de servidor específico que você cria. | 
   | **Nome (opcional)** | *Deixe em branco* | Essa opção permite que você especifique um nome amigável para o servidor. | 

5. Selecione **Conectar**. 

Depois de se conectar com êxito, o servidor é aberto na **servidores** barra lateral.


## <a name="create-a-database"></a>Criar um banco de dados

As seguintes etapas criam um banco de dados denominado **tutorialdb**:

1. Clique com botão direito no seu servidor PostgreSQL na **servidores** barra lateral e selecione **nova consulta**.

2. Cole essa instrução SQL no editor de consultas que se abre.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. Na barra de ferramentas, selecione **executar** para executar a consulta. As notificações aparecem na **mensagens** painel para mostrar o progresso da consulta.

>[!TIP]
> Você pode usar **F5** em seu teclado para executar a instrução em vez de usar **executar**.

Depois que a consulta for concluída, clique com botão direito **bancos de dados** e selecione **atualize** para ver **tutorialdb** na lista sob o **bancos de dados** nó .


## <a name="create-a-table"></a>Criar uma tabela

 As etapas a seguir criam uma tabela na **tutorialdb**:

1. Alterar o contexto de conexão para **tutorialdb** usando a lista suspensa no editor de consultas. 

   ![Contexto de alteração](media/quickstart-postgresql/change-context.png)

2. Cole a seguinte instrução SQL no editor de consultas e clique em **executar**. 

   > [!NOTE]
   > Você pode anexá-lo ou substituir a consulta existente no editor. Clicando em **executar** executa somente a consulta que está realçada. Se nada é realçado, clique em **executar** executa todas as consultas no editor.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>Inserir linhas

Cole o trecho a seguir na janela de consulta e clique em **executar**:

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>Consultar os dados

1. Cole o trecho a seguir no editor de consultas e clique em **executar**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Os resultados da consulta são exibidos:

   ![Exibir resultados](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre o [cenários disponíveis para Postgres no estúdio de dados do Azure](postgres-extension.md). 