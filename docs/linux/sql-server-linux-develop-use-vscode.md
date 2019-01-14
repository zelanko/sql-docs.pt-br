---
title: Use a extensão do Visual Studio Code mssql para o SQL Server no Linux | Microsoft Docs
description: Use a extensão mssql para Visual Studio Code para editar e executar scripts Transact-SQL para o SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: sql-linux
ms.openlocfilehash: 583c7ac13b49370b333e80568c4b52885b58dcf3
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100561"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-on-linux"></a>Use o Visual Studio Code para criar e executar scripts Transact-SQL no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar o *mssql* extensão para o Visual Studio Code para desenvolver bancos de dados do SQL Server no Linux.

## <a name="install-and-start-visual-studio-code"></a>Instalar e iniciar o Visual Studio Code

Visual Studio Code é um editor de código gráfico para Linux, macOS e Windows que dá suporte a extensões. 

1. [Baixe e instale o Visual Studio Code] em seu computador.
   
1. Inicie o Visual Studio Code.
   
   >[!NOTE]
   >Se o Visual Studio Code não inicia quando você está conectado por meio de uma sessão de área de trabalho remota do xrdp, consulte [código do VS não está funcionando no Ubuntu quando conectado o uso do XRDP](https://github.com/Microsoft/vscode/issues/3451).

## <a name="install-the-mssql-extension"></a>Instalar a extensão mssql

O [extensão mssql para Visual Studio Code] permite que você se conecte a um SQL Server com o Transact-SQL (T-SQL) de consulta e exibir os resultados.

1. No Visual Studio Code, selecione **modo de exibição** > **paleta de comandos**, ou pressione **Ctrl**+**Shift** + **P**, ou pressione **F1** para abrir o **paleta de comandos**. 
   
1. No **paleta de comandos**, selecione **extensões: Instalar extensões** na lista suspensa. 
   
1. No **extensões** painel, digite *mssql*.
   
1. Selecione o **SQL Server (mssql)** extensão e, em seguida, selecione **instalar**. 
   
   ![Instalar a extensão mssql](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)   
   
1. Depois de concluir a instalação, selecione **recarregar** para habilitar a extensão. 

## <a name="create-or-open-a-sql-file"></a>Criar ou abrir um arquivo SQL

A extensão mssql permite comandos mssql e T-SQL IntelliSense no editor de códigos quando o modo de idioma é definido como **SQL**.

1. Selecione **arquivo** > **novo arquivo** ou pressione **Ctrl**+**N**. Visual Studio Code abre um novo arquivo de texto sem formatação por padrão. 

1. Selecione **texto sem formatação** na barra de status inferior, ou pressione **Ctrl**+**K** > **M**e selecione **SQL** na lista suspensa de idiomas. 
   
   ![Modo de linguagem SQL](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)   
   
Se você abrir um arquivo existente que tem um *. SQL* extensão de arquivo, o modo de idioma é definido automaticamente para o SQL.  

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Siga estas etapas para criar um perfil de conexão e conecte-se a um SQL Server.

> [!TIP] 
> Você também pode criar e editar perfis de conexão no arquivo de configurações do usuário (*Settings*). Para abrir o arquivo de configurações, selecione **arquivo** > **preferências** > **configurações**. Para obter mais informações, consulte [gerenciar perfis de conexão].
   
1. Pressione **Ctrl**+**Shift**+**P** ou **F1** para abrir o **paleta de comandos**. 
   
1. Tipo de *sql* para exibir o mssql comandos ou tipo *sqlcon*e, em seguida, selecione **MS SQL: Conectar-se** na lista suspensa.
   
   ![comandos MSSQL](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)   
   
   >[!NOTE]
   >Um arquivo SQL, como o arquivo SQL vazio que você criou, deve ter o foco no editor de código antes de executar os comandos mssql. 

1. Selecione **criar o perfil de Conexão** para criar um novo perfil de conexão para o SQL Server.
   
1. Siga os prompts para especificar as propriedades para o novo perfil de conexão. Depois de especificar cada valor, pressione **Enter** para continuar. 
   
   1. **Nome do servidor ou a cadeia de caracteres de conexão ADO**: Especifique o nome da instância do SQL Server. Use *localhost* para se conectar a uma instância do SQL Server no computador local. Para se conectar a um servidor SQL remoto, digite o nome do destino do SQL Server, ou seu endereço IP. Se você precisar especificar uma porta, use uma vírgula para separá-lo a partir do nome. Por exemplo, para um servidor local em execução na porta 1401, insira *localhost, 1401*. 
      
      >[!NOTE]
      >Você também pode inserir a cadeia de caracteres de conexão do ADO do banco de dados aqui, pressione **Enter**, opcionalmente, o nome do perfil de conexão e pressione **Enter** novamente para se conectar e criar o perfil. 
      
   1. **Nome do banco de dados** (opcional): O banco de dados que você deseja usar. Para criar um novo banco de dados, não especifique um banco de dados nome e pressione **Enter** para continuar. 
      
   1. **Tipo de autenticação**: Pressione **Enter** para selecionar **logon SQL**. 
      
   1. **Nome de usuário**: Insira o nome de um usuário com acesso a um banco de dados no servidor.
      
   1. **Senha**: Digite a senha para o usuário especificado.
      
   1. **Salvar senha**: Pressione **Enter** para selecionar **Sim** e salve a senha. Selecione **não** para fornecer a senha sempre que o perfil de conexão é usado. 
      
   1. **Nome do perfil** (opcional): Digite um nome para o perfil de conexão, como *localhost perfil*. 
   
   Depois de selecionar **Enter**, código do Visual Studio cria o perfil de conexão e conecta-se ao SQL Server. 
   
   > [!TIP]
   > Se a conexão falhar, tentar diagnosticar o problema da mensagem de erro entre o **saída** painel no Visual Studio Code. Para abrir o **saída** painel, selecione **exibição** > **saída**. Examine também os [recomendações de solução de problemas de conexão].
   
1. Verifique se sua conexão na barra de status inferior.
   
  ![Status de Conexão](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)   
   
## <a name="create-a-sql-database"></a>Criar um banco de dados SQL

1. No novo arquivo SQL que você iniciou anteriormente, digite *sql* para exibir uma lista de trechos de código editável. 

  ![Trechos de código SQL](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)   
   
1. Selecione **sqlCreateDatabase**.
   
1. No trecho de código, substitua `DatabaseName` com `TutorialDB`:
   
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
   
1. Pressione **Ctrl**+**Shift**+**E** para executar os comandos Transact-SQL. Exiba os resultados na janela de consulta.
   
  ![Criar mensagens de banco de dados](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)   
   
> [!TIP]
> Você pode personalizar as teclas de atalho para os comandos mssql. Ver [personalizar atalhos].

## <a name="create-a-table"></a>Criar uma tabela

1. Exclua o conteúdo da janela do editor de código.
   
1. Pressione **Ctrl**+**Shift**+**P** ou **F1** para abrir o **paleta de comandos**. 
   
1. Tipo de *sql* para exibir o mssql comandos ou tipo *sqluse*e, em seguida, selecione o **banco de dados do MS SQL: Use** comando.
   
1. Selecione a nova **TutorialDB** banco de dados. 
   
   ![Usar banco de dados](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)   
   
1. No editor de códigos, digite *sql* para exibir os trechos de código, selecione **sqlCreateTable**e pressione **Enter**.
   
1. O trecho de código, digite *funcionários* para o nome da tabela e *dbo* para o nome do esquema.
   
1. Crie as colunas, conforme mostrado no código a seguir:
   
   ```sql
   -- Create a new table called 'Employees' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
   DROP TABLE dbo.Employees
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Employees
   (
      EmployeesId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location   [NVARCHAR](50)  NOT NULL
   );
   GO
   ```
   
1. Pressione **Ctrl**+**Shift**+**E** para criar a tabela.

## <a name="insert-and-query"></a>Inserção e consulta

1. Adicione as seguintes instruções para inserir quatro linhas para o **funcionários** tabela. 

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
   
   > [!TIP]
   > Enquanto você digita, use o T-SQL IntelliSense para ajudar a concluir as instruções.
   >![T-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)   
   
1. Pressione **Ctrl**+**Shift**+**E** para executar os comandos. Os dois resultam de exibição de conjuntos na **resultados** janela. 
   
   ![Resultados](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)   

## <a name="view-and-save-the-result"></a>Exibir e salvar o resultado
   
1. Selecione **modo de exibição** > **Layout do Editor** > **inverter o Layout** para alternar para um layout de divisão vertical ou horizontal.
   
1. Selecione o **resultados** e **mensagens** cabeçalhos para recolher e expandir os painéis do painel.
   
   ![Ativar/desativar cabeçalhos](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)   
   
   > [!TIP]
   > Você pode personalizar o comportamento padrão da extensão mssql. Ver [personalizar opções de extensão].
   
1. Selecione o ícone de grade de maximizar na segunda grade de resultado para ampliar a esses resultados.
   
   ![Maximizar a grade](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)   
   
   > [!NOTE]
   > O ícone de maximizar é exibido quando o script T-SQL produz dois ou mais grades de resultados.
   
1. Abra o menu de contexto de grade clicando na grade. 
   
   ![Menu de contexto](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)   
   
1. Selecione **Selecionar tudo**.
   
1. Abra o menu de contexto de grade novamente e selecione **Salvar como JSON** para salvar o resultado para um *. JSON* arquivo.
   
1. Especifique um nome de arquivo para o arquivo JSON. 
   
1. Verifique se o arquivo JSON salva e abre no Visual Studio Code.
   
   ![Salvar como JSON](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)   

Se você precisar salvar e executar scripts SQL mais tarde, para administração ou um projeto de desenvolvimento maior, salvar os scripts com uma *. SQL* extensão.

## <a name="next-steps"></a>Próximas etapas

Se você for novo no T-SQL, consulte [Tutorial: Escrever instruções Transact-SQL] e o [referência de Transact-SQL (mecanismo de banco de dados)].

Para obter mais informações sobre o uso ou que contribuem para a extensão mssql, consulte o [wiki do projeto de extensão MSSQL].

Para obter mais informações sobre como usar o Visual Studio Code, consulte o [documentação do Visual Studio Code](https://code.visualstudio.com/docs).

[extensão MSSQL para Visual Studio Code]:https://aka.ms/mssql-marketplace
[Baixe e instale o Visual Studio Code]:https://code.visualstudio.com/Download
[.Net Core instructions]:https://www.microsoft.com/net/core
[Gerenciar perfis de conexão]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[recomendações de solução de problemas de conexão]:./sql-server-linux-troubleshooting-guide.md#connection
[Personalizar atalhos]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Tutorial: Escrever instruções Transact-SQL]:https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements
[Referência de Transact-SQL (mecanismo de banco de dados)]:https://docs.microsoft.com/sql/t-sql/language-reference
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 Universal C Runtime]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[Personalizar opções de extensão]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[wiki do projeto de extensão MSSQL]: https://github.com/Microsoft/vscode-mssql/wiki
