---
title: Use a extensão do Visual Studio Code mssql para o SQL Server | Microsoft Docs
description: Este tutorial mostra como usar a extensão mssql para o VS Code. Essa extensão permite que você edite e execute scripts Transact-SQL no VS Code.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: sql-linux
ms.openlocfilehash: be5a40a904389979c1646aab9d8b4420ac71356a
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084738"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>Use o Visual Studio Code para criar e executar scripts Transact-SQL para o SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar o **mssql** extensão para o Visual Studio Code (VS Code) para desenvolver bancos de dados do SQL Server.

Visual Studio Code é um editor de código gráfico para Linux, macOS e Windows que dá suporte a extensões. O [**mssql** extensão para código VS] permite que você se conectar ao SQL Server, a consulta com o Transact-SQL (T-SQL) e exibir os resultados.

## <a name="install-vs-code"></a>Instalar o VS Code
1. Se você ainda não instalou VS Code [baixar e instalar o VS Code] em seu computador.

2. Inicie o VS Code.

## <a name="install-the-mssql-extension"></a>Instalar a extensão mssql
As etapas a seguir explicam como instalar a extensão mssql. 

1. Pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comandos no VS Code. 

2. Selecione **instalar extensão** e digite **mssql**.
   > [!TIP] 
   > Para macOS, o **CMD** chave é equivalente a **CTRL** chave no Linux e Windows.

2. Clique em instalar **mssql**. 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. O **mssql** extensão leva até um minuto para instalar. Aguarde até que o aviso que informa a instalado com êxito.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > Para macOS, você deve instalar o OpenSSL. Esse é um pré-requisito para o.Net Core usada pela extensão mssql. Siga as **instalar pré-requisitos** as etapas na [Instruções do.Net Core]. Ou, você pode executar os comandos a seguir no seu Terminal do macOS.
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > Para Windows 8.1, Windows Server 2012 ou versões anteriores, você deverá baixar e instalar o [Tempo de execução C Universal do Windows 10]. Baixe e abra o arquivo zip. Em seguida, execute o instalador (arquivo. msu) direcionando a configuração do sistema operacional atual.

## <a name="create-or-open-a-sql-file"></a>Criar ou abrir um arquivo SQL

O **mssql** extensão habilita comandos mssql e T-SQL IntelliSense no editor quando o modo de idioma é definido como **SQL**.

1. Pressione **CTRL + N**. Visual Studio Code abre um novo arquivo de 'Texto sem formatação' por padrão. 

2. Pressione **CTRL + K, M** e altere o modo de linguagem para **SQL**. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. Como alternativa, abra um arquivo existente com a extensão de arquivo. SQL. O modo de linguagem é automaticamente **SQL** para arquivos que têm a extensão. SQL.  

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

As etapas a seguir mostram como se conectar ao SQL Server com o VS Code.

1. No VSCode, pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comandos.

2. Tipo de **sql** para exibir os comandos mssql.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. Selecione o **MS SQL: conectar-se** comando. Você pode simplesmente digitar **sqlcon** e pressione **ENTER**.

4. Selecione **criar perfil de Conexão**. Isso cria um perfil de conexão para sua instância do SQL Server.

5. Siga os prompts para especificar as propriedades de conexão para o novo perfil de conexão. Depois de especificar cada valor, pressione **ENTER** para continuar. 

   A tabela a seguir descreve as propriedades de perfil de Conexão.

   | Configuração | Description |
   |-----|-----|
   | **Nome do servidor** | O nome da instância do SQL Server. Neste tutorial, use **localhost** para se conectar à instância do SQL Server local em seu computador. Se estiver se conectando a um servidor SQL remoto, digite o nome do computador do SQL Server de destino ou endereço IP. Se você precisar especificar uma porta para a instância do SQL Server, use uma vírgula para separá-lo a partir do nome. Por exemplo para um servidor local em execução na porta 1401 você digitaria **localhost, 1401**. |
   | **[Opcional] Nome do banco de dados** | O banco de dados que você deseja usar. Para fins deste tutorial, não especificar um banco de dados e pressione **ENTER** para continuar. |
   | **Nome de usuário** | Insira o nome de um usuário com acesso a um banco de dados no servidor. Para este tutorial, use o padrão **SA** conta criada durante a instalação do SQL Server. |
   | **Senha (logon do SQL)** | Digite a senha para o usuário especificado. | 
   | **Salvar senha?** | Tipo de **Sim** para salvar a senha. Caso contrário, digite **não** para fornecer a senha sempre que o perfil de Conexão é usado. |
   | **[Opcional] Insira um nome para este perfil** | O nome do perfil de Conexão. Por exemplo, você pode nomear o perfil **localhost perfil**. 

   > [!Tip] 
   > Você pode criar e editar perfis de conexão no arquivo de configurações do usuário (Settings). Abra o arquivo de configurações, selecionando **preferência** e, em seguida **configurações do usuário** no menu do VS Code. Para obter mais informações, consulte [gerenciar perfis de conexão].

6. Pressione a tecla **ESC** para fechar a mensagem de informações que informa que o perfil está criado e conectado.

   > [!TIP]
   > Se você receber uma falha de conexão, primeira tentativa para diagnosticar o problema da mensagem de erro no **saída** painel no VS Code (selecionar **saída** no **exibição** menu). Em seguida, examine as [recomendações de solução de problemas de conexão].

7. Verifique sua conexão na barra de status.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png" alt="Connection status" style="width: 500px;" />

## <a name="create-a-database"></a>Criar um banco de dados

1. No editor, digite **sql** para exibir uma lista de trechos de código editável. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png" alt="SQL snippets" style="width: 500px;" />

2. Selecione **sqlCreateDatabase**.

3. O trecho de código, digite **TutorialDB** para o nome do banco de dados.

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
   > Você pode personalizar as associações de teclas de atalho para os comandos de extensão mssql. Ver [personalizar atalhos].

## <a name="create-a-table"></a>Criar uma tabela

1. Remove o conteúdo da janela do editor.

2. Pressione **F1** para exibir a paleta de comandos.

3. Tipo de **sql** na paleta de comandos para exibir comandos SQL ou do tipo **sqluse** para **banco de dados do MS SQL: Use** comando.

4. Clique em **banco de dados do MS SQL: Use**e selecione o **TutorialDB** banco de dados. Isso altera o contexto para o novo banco de dados criado na seção anterior.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. No editor, digite **sql** para exibir os trechos de código e, em seguida, selecione **sqlCreateTable** e pressione **insira**.

4. O trecho de código, digite **funcionários** para o nome da tabela.

5. Pressione **guia**e, em seguida, digite **dbo** para o nome do esquema.

   > [!NOTE]
   > Depois de adicionar o trecho de código, você deve digitar os nomes de tabela e esquema sem alterar o foco para fora do editor de código do VS.

6. Altere o nome da coluna **Column1** à **nome** e **Column2** para **local**.

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
   > Enquanto você digita, use a Ajuda do T-SQL IntelliSense.
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. Pressione **CTRL + SHIFT + E** para executar os comandos. Os dois resultam de exibição de conjuntos na **resultados** janela. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>Exibir e salvar o resultado

1. No **modo de exibição** menu, selecione **Editor de ativar/desativar grupo Layout** para alternar para layout vertical ou horizontal de divisão.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. Clique o **resultados** e **mensagens** cabeçalho do painel para recolher e expandir o painel.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > Você pode personalizar o comportamento padrão da extensão mssql. Ver [personalizar opções de extensão].

2. Clique no ícone de grade de maximizar a segunda grade de resultados para aumentar o zoom.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > O ícone de maximizar exibe quando o script T-SQL tem dois ou mais grades de resultados.

3. Abra o menu de contexto de grade com o botão direito do mouse em uma grade. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. Selecione **Selecionar tudo**.

5. Abra o menu de contexto de grade e selecione **Salvar como JSON** para salvar o resultado em um arquivo. JSON.

6. Especifique um nome de arquivo para o arquivo JSON. Neste tutorial, digite **employees.json**.

7. Verifique se o arquivo JSON é salvo e aberto no Visual Studio Code.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>Próximas etapas

Em um cenário do mundo real, você pode criar um script que você precisa salvar e executar posterior (para administração ou como parte de um projeto de desenvolvimento maior). Nesse caso, você pode salvar o script com um **. SQL** extensão.

Se você for novo no T-SQL, consulte [Tutorial: gravando instruções Transact-SQL] e o [referência de Transact-SQL (mecanismo de banco de dados)].

Para obter mais informações sobre o uso ou que contribuem para a extensão mssql, consulte [wiki do projeto de extensão mssql].

Para obter mais informações sobre como usar o VS Code, consulte o [documentação do Visual Studio Code](https://code.visualstudio.com/docs).

[**mssql** extensão para código VS]:https://aka.ms/mssql-marketplace
[Baixar e instalar o VS Code]:https://code.visualstudio.com/Download
[Instruções do.Net Core]:https://www.microsoft.com/net/core
[Gerenciar perfis de conexão]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[recomendações de solução de problemas de conexão]:./sql-server-linux-troubleshooting-guide.md#connection
[Personalizar atalhos]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Tutorial: Gravando instruções Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[Referência de Transact-SQL (mecanismo de banco de dados)]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Tempo de execução C Universal do Windows 10]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[Personalizar opções de extensão]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[wiki do projeto de extensão mssql]: https://github.com/Microsoft/vscode-mssql/wiki
