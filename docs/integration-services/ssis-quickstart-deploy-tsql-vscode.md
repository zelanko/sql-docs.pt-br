---
title: Implantar um projeto do SSIS com Transact-SQL (VSCode) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f4e5d15cc4ef8c7b51f2fa79e0ff35e7f53d9df
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>Implantar um projeto do SSIS por meio do Visual Studio Code com o Transact-SQL
Este guia de início rápido demonstra como usar o Visual Studio Code para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, usar instruções do Transact-SQL para implantar um projeto do SSIS no Catálogo do SSIS.

> [!NOTE]
> O método descrito neste artigo não está disponível quando você se conecta a um servidor de Banco de Dados SQL do Azure com o VSCode. O procedimento armazenado `catalog.deploy_project` espera o caminho para o arquivo `.ispac` no sistema de arquivos local.

O Visual Studio Code é um editor de código para Windows, macOS e Linux que dá suporte a extensões, incluindo a extensão `mssql` para se conectar ao Microsoft SQL Server, o Banco de Dados SQL do Azure ou o SQL Data Warehouse do Azure. Para obter mais informações sobre o VSCode, consulte [Visual Studio Code](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você instalou a versão mais recente do Visual Studio Code e carregue a extensão `mssql`. Para baixar essas ferramentas, consulte as seguintes páginas:
-   [Baixar o Visual Studio Code](https://code.visualstudio.com/Download)
-   [extensão mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Definir o modo de linguagem para SQL no VSCode

Para habilitar comandos do `mssql` e T-SQL IntelliSense, defina o modo de linguagem para **SQL** no Visual Studio Code.

1. Abra o Visual Studio Code e, em seguida, abra uma nova janela. 

2. Clique em **Texto sem Formatação** no canto inferior direito da barra de status.
 
3. No menu suspenso **Selecionar modo de linguagem** que é aberto, selecione ou insira **SQL** e, em seguida, pressione **ENTER** para definir o modo de linguagem para SQL. 

## <a name="connect-to-the-ssis-catalog-database"></a>Conectar-se ao banco de dados de Catálogo do SSIS

Use o Visual Studio Code para estabelecer uma conexão com o Catálogo do SSIS.

> [!IMPORTANT]
> Antes de continuar, verifique se você tem suas informações de servidor, banco de dados e logon à disposição. Se você alterar o foco do Visual Studio Code depois de começar a inserir as informações de perfil de conexão, você precisará reiniciar a criação do perfil de conexão.

1. No VSCode, pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comandos.

2. Digite **sqlcon** e pressione **ENTER**.

3. Pressione **ENTER** para selecionar **Criar Perfil de Conexão**. Esta etapa cria um perfil de conexão para a instância do SQL Server.

4. Siga os prompts para especificar as propriedades de conexão para o novo perfil de conexão. Depois de especificar cada valor, pressione **ENTER** para continuar. 

   | Configuração       | Valor sugerido | Obter mais informações |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado |  |
   | **Nome do banco de dados** | **SSISDB** | O nome do banco de dados ao qual se conectar. |
   | **Autenticação** | Logon do SQL| Este guia de início rápido usa a autenticação do SQL. |
   | **User name** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Se você não deseja inserir a senha a cada vez, selecione Sim. |
   | **Inserir um nome para este perfil** | Um nome de perfil, assim como **mySSISServer** | Um nome de perfil salvo acelera sua conexão em logons subsequentes. | 

5. Pressione a tecla **ESC** para fechar a mensagem de informações que informa que o perfil está criado e conectado.

6. Verifique sua conexão na barra de status.

## <a name="run-the-t-sql-code"></a>Executar o código T-SQL
Execute o seguinte código Transact-SQL para implantar um projeto do SSIS.

1. Na janela **Editor**, digite a consulta a seguir na janela de consulta vazia.

2. Atualizar os valores de parâmetro no procedimento armazenado `catalog.deploy_project` para seu sistema.

3. Pressione **CTRL+SHIFT+E** para executar o código e implantar o projeto.

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary = (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS por meio do prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implantar um pacote do SSIS com o C#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher uma entre várias ferramentas e linguagens. Para saber mais, veja os tópicos a seguir:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
