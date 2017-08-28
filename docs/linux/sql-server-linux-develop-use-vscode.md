---
title: "Use a extensão do Visual Studio Code mssql para o SQL Server | Microsoft Docs"
description: "Este tutorial mostra como usar a extensão mssql para o código de VS. Essa extensão permite editar e executar scripts Transact-SQL no código VS."
author: erickangMSFT
ms.author: erickang
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a4b2f82ac904d58604b0c27d46624995878e8a35
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>Use o código do Visual Studio para criar e executar scripts Transact-SQL para SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tópico mostra como usar o **mssql** extensão para o código do Visual Studio (VS código) para desenvolver bancos de dados do SQL Server.

Código do Visual Studio é um editor de código gráfica para Linux, macOS e Windows que oferece suporte a extensões. O [**mssql** extensão para código VS] permite que você se conectar ao SQL Server, a consulta com o Transact-SQL (T-SQL) e exibir os resultados.

## <a name="install-vs-code"></a>Instalar o código do VS
1. Se você ainda não tiver instalado o código VS, [baixar e instalar código VS] em seu computador.

2. Inicie código VS.

## <a name="install-the-mssql-extension"></a>Instalar a extensão mssql
As etapas a seguir explicam como instalar a extensão mssql. 

1. Pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comando no código VS. 

2. Selecione **instalar extensão** e tipo **mssql**.
   > [!TIP] 
   > Para macOS, o **CMD** chave é equivalente a **CTRL** chave no Linux e Windows.

2. Clique em instalar **mssql**. 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. O **mssql** extensão leva até um minuto para instalar. Aguarde o aviso que informa ao instalado com êxito.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > Para macOS, você deve instalar o OpenSSL. Este é um pré-requisito para .net Core usado pela extensão de mssql. Siga o **instalar pré-requisitos** etapas o [.Net Core instruções]. Ou, você pode executar os seguintes comandos em seu Terminal macOS.
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > Para Windows 8.1, Windows Server 2012 ou versões anteriores, você deve baixar e instalar o [Windows 10 Universal C Runtime]. Baixe e abra o arquivo zip. Em seguida, execute o instalador (arquivo. msu) direcionando a configuração atual do sistema operacional.

## <a name="create-or-open-a-sql-file"></a>Criar ou abrir um arquivo SQL

O **mssql** extensão habilita comandos mssql e T-SQL IntelliSense no editor quando o modo de idioma é definido como **SQL**.

1. Pressione **CTRL + N**. Código do Visual Studio abre um novo arquivo de 'Texto sem formatação' por padrão. 

2. Pressione **CTRL + K, M** e alterar o modo de linguagem para **SQL**. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. Como alternativa, abra um arquivo existente com extensão de arquivo. SQL. O modo de idioma é automaticamente **SQL** para arquivos que têm a extensão. SQL.  

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

As etapas a seguir mostram como se conectar ao SQL Server com o código de VS.

1. No código VS, pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comando.

2. Tipo **sql** para exibir os comandos mssql.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. Selecione o **MS SQL: conectar** comando. Você pode simplesmente digitar **sqlcon** e pressione **ENTER**.

4. Selecione **criar perfil de Conexão**. Isso cria um perfil de conexão para a instância do SQL Server.

5. Siga os prompts para especificar as propriedades de conexão para o novo perfil de conexão. Depois de especificar cada valor, pressione **ENTER** para continuar. 

   A tabela a seguir descreve as propriedades de perfil de Conexão.

   | Configuração | Description |
   |-----|-----|
   | **Nome do servidor** | O nome da instância do SQL Server. Para este tutorial, use **localhost** para se conectar à instância do SQL Server local no seu computador. Se estiver se conectando a um servidor SQL remoto, digite o nome do computador do SQL Server de destino ou endereço IP. |
   | **[Opcional] Nome do banco de dados** | O banco de dados que você deseja usar. Para fins deste tutorial, não especifique um banco de dados e pressione **ENTER** para continuar. |
   | **Nome de usuário** | Digite o nome de um usuário com acesso ao banco de dados no servidor. Para este tutorial, use o padrão **SA** conta criada durante a instalação do SQL Server. |
   | **Senha (logon SQL)** | Digite a senha para o usuário especificado. | 
   | **Salvar senha?** | Tipo **Sim** para salvar a senha. Caso contrário, digite **não** para fornecer a senha sempre que o perfil de Conexão é usado. |
   | **[Opcional] Insira um nome para este perfil** | O nome do perfil de Conexão. Por exemplo, você pode nomear o perfil **localhost perfil**. 

   > [!Tip] 
   > Você pode criar e editar perfis de conexão no arquivo de configurações do usuário (settings.json). Abra o arquivo de configurações selecionando **preferência** e **as configurações do usuário** no menu de código VS. Para obter mais detalhes, consulte [gerenciar perfis de conexão].

6. Pressione a **ESC** tecla para fechar a mensagem de informações que informa que o perfil é criado e conectado.

   > [!TIP]
   > Se você receber uma falha de conexão, primeira tentativa para diagnosticar o problema da mensagem de erro no **saída** painel no código VS (selecione **saída** no **exibição** menu). Em seguida, examine as [recomendações de solução de problemas de conexão].

7. Verifique se sua conexão na barra de status.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png" alt="Connection status" style="width: 500px;" />

## <a name="create-a-database"></a>Criar um banco de dados

1. No editor, digite **sql** para exibir uma lista de trechos de código editável. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png" alt="SQL snippets" style="width: 500px;" />

2. Selecione **sqlCreateDatabase**.

3. No trecho de código, digite **TutorialDB** para o nome do banco de dados.

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
   ```
   
4. Pressione **CTRL + SHIFT + E** para executar os comandos Transact-SQL. Exiba os resultados na janela de consulta.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png" alt="create database messages" style="width: 500px;" />

   > [!TIP]
   > Você pode personalizar as associações de tecla de atalho para os comandos de extensão mssql. Consulte [personalizar atalhos].

## <a name="create-a-table"></a>Criar uma tabela

1. Remova o conteúdo da janela do editor.

2. Pressione **F1** para exibir a paleta de comando.

3. Tipo **sql** na paleta de comando para exibir os comandos SQL ou tipo **sqluse** para **o banco de dados do MS SQL: Use** comando.

4. Clique em **o banco de dados do MS SQL: Use**e selecione o **TutorialDB** banco de dados. Isso altera o contexto para o novo banco de dados criado na seção anterior.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. No editor, digite **sql** para exibir os trechos de código e, em seguida, selecione **sqlCreateTable** e pressione **insira**.

4. No trecho de código, digite **funcionários** para o nome da tabela.

5. Pressione **guia**e, em seguida, digite **dbo** para o nome do esquema.

   > [!NOTE]
   > Depois de adicionar o trecho de código, você deve digitar os nomes de tabela e esquema sem alterar o foco para fora do editor de códigos do VS.

6. Altere o nome da coluna **Column1** para **nome** e **Column2** para **local**.

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

7. Pressione **CTRL + SHIFT + E** para criar a tabela.

## <a name="insert-and-query"></a>Inserção e consulta

1. Adicione as seguintes instruções para inserir quatro linhas para o **funcionários** tabela. Em seguida, selecione todas as linhas.

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
   > Enquanto você digita, use a Ajuda do IntelliSense T-SQL.
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. Pressione **CTRL + SHIFT + E** para executar os comandos. Os dois resultam conjuntos de exibição no **resultados** janela. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>Exibir e salvar o resultado

1. No **exibição** menu, selecione **alternar Editor grupo Layout** para alternar para layout de divisão vertical ou horizontal.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. Clique o **resultados** e **mensagens** cabeçalho de painel para recolher e expandir o painel.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > Você pode personalizar o comportamento padrão da extensão mssql. Consulte [personalizar opções de extensão].

2. Clique no ícone de grade de maximizar a segunda grade de resultados para aumentar o zoom.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > O ícone de maximizar exibe quando o script T-SQL tem dois ou mais grades de resultados.

3. Abra o menu de contexto de grade com o botão direito do mouse em uma grade. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. Selecione **Selecionar tudo**.

5. Abra o menu de contexto de grade e selecione **Salvar como JSON** para salvar o resultado em um arquivo. JSON.

6. Especifique um nome de arquivo para o arquivo JSON. Para este tutorial, digite **employees.json**.

7. Verifique se o arquivo JSON é salvo e aberto no código VS.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>Próximas etapas

Em um cenário do mundo real, você pode criar um script que você precisa salvar e executar posterior (para administração ou como parte de um projeto de desenvolvimento maior). Nesse caso, você pode salvar o script com um **. SQL** extensão.

Se você estiver familiarizado com o T-SQL, consulte [Tutorial: gravando instruções de Transact-SQL] e [referência Transact-SQL (mecanismo de banco de dados)].

Para obter mais informações sobre o uso ou que contribuem para a extensão do mssql, consulte [wiki de projeto de extensão do mssql].

Para obter mais informações sobre como usar código VS, consulte o [documentação do Visual Studio Code](https://code.visualstudio.com/docs).

[**mssql** a extensão para o código do VS]:https://aka.ms/mssql-marketplace
[baixar e instalar código VS]:https://code.visualstudio.com/Download
[.Net Core instruções]:https://www.microsoft.com/net/core
[gerenciar perfis de conexão]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[recomendações de solução de problemas de conexão]:./sql-server-linux-troubleshooting-guide.md#connection
[personalizar atalhos]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Tutorial: gravando instruções de Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[referência Transact-SQL (mecanismo de banco de dados)]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 Universal C Runtime]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[personalizar opções de extensão]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[wiki de projeto de extensão do mssql]: https://github.com/Microsoft/vscode-mssql/wiki

