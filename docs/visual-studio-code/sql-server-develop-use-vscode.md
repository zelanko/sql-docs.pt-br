---
title: Usar a extensão mssql do Visual Studio Code
description: Use a extensão mssql para Visual Studio Code para editar e executar scripts do Transact-SQL para SQL Server em Linux.
ms.topic: conceptual
ms.prod: sql
ms.technology: tools-other
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
author: markingmyname
ms.author: maghan
ms.date: 10/28/2019
ms.openlocfilehash: 657dab5c2d80bc4ae4c404872386eb993e242235
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896532"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>Usar o Visual Studio Code para criar e executar scripts do Transact-SQL

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo mostra como usar a extensão **mssql** para Visual Studio Code para desenvolver bancos de dados do SQL Server. Como Visual Studio Code é multiplataforma, você pode usar a extensão **mssql** em Linux, macOS e Windows.

## <a name="install-and-start-visual-studio-code"></a>Instalar e iniciar o Visual Studio Code

O Visual Studio Code é um editor de código gráfico multiplataforma compatível com extensões.

1. [Baixe e instale Visual Studio Code](https://code.visualstudio.com/) em seu computador.

2. Inicie o Visual Studio Code.

    >[!NOTE]
    >Se Visual Studio Code não iniciar quando você estiver conectado por meio de uma sessão de área de trabalho remota do xrdp, confira [O VS Code não está funcionando no Ubuntu](https://github.com/Microsoft/vscode/issues/3451) quando conectado usando XRDP.

## <a name="install-the-mssql-extension"></a>Instalar a extensão mssql

A [extensão mssql para Visual Studio Code](https://aka.ms/mssql-marketplace) permite que você se conecte a um SQL Server, consulte com o Transact-SQL (T-SQL) e exiba os resultados.

1. No Visual Studio Code, selecione **Exibir** > **Paleta de Comandos** ou pressione **Ctrl**+**Shift**+**P** ou **F1** para abrir a **Paleta de Comandos**.

2. Na **Paleta de Comandos**, selecione **Extensões: Instalar Extensões** no menu suspenso.

3. No painel **Extensões**, digite *mssql*.

4. Selecione a extensão **SQL Server (MSSQL)** e, em seguida, selecione **Instalar**.

   ![Instalar a extensão mssql](./media/sql-server-develop-use-vscode/vscode-extension.png)

5. Após a conclusão da instalação, selecione **Recarregar** para habilitar a extensão.

## <a name="create-or-open-a-sql-file"></a>Criar ou abrir um arquivo SQL

A extensão mssql habilita comandos MSSQL e o T-SQL IntelliSense no editor de códigos quando o modo de linguagem é definido como **SQL**.

1. Selecione **Arquivo** > **Novo Arquivo** ou pressione **Ctrl**+**N**. O Visual Studio Code abre um novo arquivo de texto sem formatação por padrão. 

2. Selecione **Texto Sem Formatação** na barra de status inferior ou pressione **Ctrl**+**K** > **M** selecione **SQL** na lista suspensa idiomas. 

   ![Modo de linguagem SQL](./media/sql-server-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > Se esta for a primeira vez que você usou a extensão, a extensão instalará suporte a ferramentas do SQL Server.

Se você abrir um arquivo existente que tenha uma extensão de arquivo *.sql*, o modo de linguagem será definido automaticamente como SQL.  

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Siga estas etapas para criar um perfil de conexão e conectar-se a um SQL Server.

1. Pressione **Ctrl**+**Shift**+**P** ou **F1** para abrir a **Paleta de comandos**. 

2. Digite *sql* para exibir os comandos mssql ou digite *sqlcon* e, em seguida, selecione **MS SQL: Conectar** na lista suspensa.

   ![Comandos mssql](./media/sql-server-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >Um arquivo SQL, como o arquivo SQL vazio que você criou, deve ter o foco no editor de código antes que você possa executar os comandos mssql.

3. Selecione o comando **MS SQL: Gerenciar Perfis de Conexão**.

4. Em seguida, selecione **Criar** para criar um novo perfil de conexão para seu SQL Server.

5. Siga os prompts para especificar as propriedades para o novo perfil de conexão. Depois de especificar cada valor, pressione **Enter** para continuar.

   | Propriedades da conexão | Descrição |
   |---|---|
   | **Nome do servidor ou cadeia de conexão ADO** | Especifique o nome da instância do SQL Server. Use *localhost* para conectar-se a uma instância do SQL Server em seu computador local. Para conectar-se a um SQL Server remoto, insira o nome do SQL Server de destino ou seu endereço IP. Para conectar-se a um contêiner do SQL Server, especifique o endereço IP do computador host do contêiner. Se você precisar especificar uma porta, use uma vírgula para separá-la do nome. Por exemplo, para um servidor que escuta na porta 1401, insira `<servername or IP>,1401`.<br/><br/>Como alternativa, você pode inserir a cadeia de conexão ADO para seu banco de dados aqui. |
   | **Nome do banco de dados** (opcional) | O banco de dados que você deseja usar. Para conectar-se ao banco de dados padrão, não especifique um nome de banco de dados aqui. |
   | **Tipo de Autenticação** | Escolha **Integrado** ou **Logon do SQL**. |
   | **Nome de usuário** | Se você tiver selecionado o **Logon do SQL**, insira o nome de um usuário com acesso a um banco de dados no servidor. |
   | **Senha** | Digite a senha para o usuário especificado. |
   | **Salvar Senha** | Pressione **Enter** para selecionar **Sim** e salvar a senha. Selecione **Não** para que a senha seja solicitada sempre que o perfil de conexão for usado. |
   | **Nome do Perfil** (opcional) | Digite um nome para o perfil de conexão, como *perfil do localhost*. |

   Depois de inserir todos os valores e selecionar **Enter**, o Visual Studio Code cria o perfil de conexão e conecta-se ao SQL Server.

   > [!TIP]
   > Se a conexão falhar, tente diagnosticar o problema usando a mensagem de erro no painel **Saída** no Visual Studio Code. Para abrir o painel **Saída**, selecione **Exibir** > **Saída**. Também examine as [recomendações de solução de problemas de conexão](../linux/sql-server-linux-troubleshooting-guide.md).

6. Verifique sua conexão na barra de status inferior.

   ![Status da conexão](./media/sql-server-develop-use-vscode/vscode-connection-status.png)

Como alternativa às etapas anteriores, também é possível criar e editar perfis de conexão no arquivo Configurações do Usuário (*settings.json*). Para abrir o arquivo de configurações, selecione **Arquivo** > **Preferências** > **Configurações**. Para obter mais informações, confira [Gerenciar perfis de conexão](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles).

## <a name="create-a-sql-database"></a>Criar um Banco de Dados SQL

1. No novo arquivo SQL que você iniciou anteriormente, digite *sql* para exibir uma lista de snippets editáveis.

   ![Snippets de SQL](./media/sql-server-develop-use-vscode/vscode-sql-snippets.png)

2. Selecione **sqlCreateDatabase**.

3. No snippet, digite `TutorialDB` para substituir 'DatabaseName':

   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

4. Pressione **Ctrl**+**Shift**+**E** para executar os comandos Transact-SQL. Exiba os resultados na janela de consulta.

    ![Criar mensagens de banco de dados](./media/sql-server-develop-use-vscode/vscode-create-database-messages.png)

    > [!TIP]
    > Você pode personalizar as teclas de atalho para os comandos mssql. Confira [Personalizar atalhos](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts).

## <a name="create-a-table"></a>Criar uma tabela

1. Exclua o conteúdo da janela do editor de código.

2. Pressione **Ctrl**+**Shift**+**P** ou **F1** para abrir a **Paleta de comandos**.

3. Digite *sql* para exibir os comandos mssql ou digite *sqluse* e, em seguida, selecione o comando **MS SQL: Usar Banco de Dados**.

4. Selecione o novo banco de dados **TutorialDB**.

   ![Usar o banco de dados](./media/sql-server-develop-use-vscode/vscode-use-database.png)

5. No editor de códigos, digite *sql* para exibir os snippets, selecione **sqlCreateTable** e pressione **Enter**.

6. No snippet, digite `Employees` para o nome da tabela.

7. Pressione **Tab** para ir para o próximo campo e digite `dbo` para o nome do esquema.

8. Substitua as definições de coluna pelas seguintes colunas:

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

9. Pressione **Ctrl**+**Shift**+**E** para criar a tabela.

## <a name="insert-and-query"></a>Inserir e consultar

1. Adicione as instruções a seguir para inserir quatro linhas na tabela **Employees**.

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')
   GO
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location
   FROM dbo.Employees as e
   GO
   ```

   Enquanto você digita, o T-SQL IntelliSense ajuda a concluir as instruções:

   ![T-SQL IntelliSense](./media/sql-server-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > A extensão MSSQL também tem comandos para ajudar a criar instruções INSERT e SELECT. Isso não foi usado no exemplo anterior.

2. Pressione **Ctrl**+**Shift**+**E** para executar os comandos. Os dois conjuntos de resultados são exibidos na janela **Resultados**.

   ![Resultados](./media/sql-server-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>Exiba e salve o resultado

1. Selecione **Exibir** > **Layout do Editor** > **Inverter Layout** para alternar para um layout de divisão vertical ou horizontal.

2. Selecione os cabeçalhos **Resultados** e **Mensagens** para recolher e expandir os painéis.

   ![Alternar cabeçalhos](./media/sql-server-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > Você pode personalizar o comportamento padrão da extensão mssql. Confira [Personalizar opções de extensão](https://github.com/Microsoft/vscode-mssql/wiki/customize-options).

3. Selecione o ícone de maximizar grade na segunda grade de resultados para ampliar esses resultados.

   ![Maximizar grade](./media/sql-server-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > O ícone de maximizar é exibido quando seu script T-SQL produz duas ou mais grades de resultado.

4. Abra o menu de contexto de grade clicando com o botão direito do mouse na grade.

   ![Menu de contexto](./media/sql-server-develop-use-vscode/vscode-grid-context-menu.png)

5. Selecione **Selecionar Tudo**.

6. Abra o menu de contexto da grade novamente e selecione **Salvar como JSON** para salvar o resultado em um arquivo *.json*.

7. Especifique um nome de arquivo para o arquivo JSON.

8. Verifique se o arquivo JSON é salvo e aberto em Visual Studio Code.

   ![Salvar como JSON](./media/sql-server-develop-use-vscode/vscode-save-as-json.png)

Se você precisar salvar e executar scripts SQL posteriormente, para administração ou um projeto de desenvolvimento maior, salve os scripts com uma extensão *.sql*.

## <a name="next-steps"></a>Próximas etapas

Se você for novo no T-SQL, confira o [Tutorial: Escreva instruções Transact-SQL](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements) e a [Referência do Transact-SQL (Mecanismo de Banco de Dados)](https://docs.microsoft.com/sql/t-sql/language-reference).

Para obter mais informações sobre como usar ou contribuir com a extensão MSSQL, confira o [wiki do projeto de extensão mssql](https://github.com/Microsoft/vscode-mssql/wiki).

Para obter mais informações sobre como usar Visual Studio Code, confira a documentação do [Visual Studio Code](https://code.visualstudio.com/docs).