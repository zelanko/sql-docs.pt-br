---
title: "Implantar um projeto do SSIS com Transact-SQL (código do VS) | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 2dc6de798ca76b43627a3c381fe628506c3e7480
ms.contentlocale: pt-br
ms.lasthandoff: 10/04/2017

---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>Implantar um projeto SSIS a partir do código do Visual Studio com o Transact-SQL
Este guia rápido demonstra como usar o código do Visual Studio para se conectar ao banco de dados de catálogo do SSIS e, em seguida, usar instruções Transact-SQL para implantar um projeto do SSIS no catálogo do SSIS.

> [!NOTE]
> O método descrito neste artigo não está disponível quando você se conectar a um servidor de banco de dados SQL com o código de VS. O `catalog.deploy_project` procedimento armazenado espera o caminho para o `.ispac` arquivo no sistema de arquivos local (no local).

Código do Visual Studio é um editor de código para Windows, macOS e Linux que oferece suporte a extensões, incluindo o `mssql` extensão para se conectar ao Microsoft SQL Server, o banco de dados do SQL Azure ou Azure SQL Data Warehouse. Para obter mais informações sobre código VS, consulte [código do Visual Studio](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de ter instalado a versão mais recente do código do Visual Studio e carregar o `mssql` extensão. Para baixar essas ferramentas, consulte as seguintes páginas:
-   [Baixar o Visual Studio Code](https://code.visualstudio.com/Download)
-   [extensão MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Definir o modo de idioma para o SQL no código VS

Para habilitar `mssql` comandos e T-SQL IntelliSense, defina o modo de linguagem para **SQL** no código do Visual Studio.

1. Abra o código do Visual Studio e, em seguida, abra uma nova janela. 

2. Clique em **texto sem formatação** no canto inferior direito da barra de status.
 
3. No **modo Selecionar idioma** menu suspenso que é aberta, selecione ou insira **SQL**e, em seguida, pressione **ENTER** para definir o modo de idioma para o SQL. 

## <a name="connect-to-the-ssis-catalog-database"></a>Conecte-se ao banco de dados de catálogo do SSIS

Use o código do Visual Studio para estabelecer uma conexão para o catálogo do SSIS.

> [!IMPORTANT]
> Antes de continuar, certifique-se de que você tenha seu servidor, banco de dados e informações de logon prontas. Se você alterar o foco de código do Visual Studio depois de você começar a inserir as informações de perfil de conexão, você precisa reiniciar criando o perfil de conexão.

1. No código VS, pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comando.

2. Tipo **sqlcon** e pressione **ENTER**.

3. Pressione **ENTER** para selecionar **criar perfil de Conexão**. Esta etapa cria um perfil de conexão para a instância do SQL Server.

4. Siga os prompts para especificar as propriedades de conexão para o novo perfil de conexão. Depois de especificar cada valor, pressione **ENTER** para continuar. 

   | Configuração       | Valor sugerido | Obter mais informações |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome totalmente qualificado do servidor |  |
   | **Nome do banco de dados** | **SSISDB** | O nome do banco de dados ao qual se conectar. |
   | **Autenticação** | Logon do SQL| Este guia de início rápido usa a autenticação do SQL. |
   | **Nome de usuário** | A conta de administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon SQL)** | A senha para sua conta de administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou não | Se você não deseja inserir a senha de cada vez, selecione Sim. |
   | **Insira um nome para este perfil** | Nome de um perfil, como **mySSISServer** | Um nome de perfil salvo acelera sua conexão em logons subsequentes. | 

5. Pressione a **ESC** tecla para fechar a mensagem de informações que informa que o perfil é criado e conectado.

6. Verifique se sua conexão na barra de status.

## <a name="run-the-t-sql-code"></a>Execute o código T-SQL
Execute o seguinte código de Transact-SQL para implantar um projeto do SSIS.

1. No **Editor** janela, digite a consulta a seguir na janela de consulta vazia.

2. Atualizar os valores de parâmetro no `catalog.deploy_project` procedimento armazenado para seu sistema.

3. Pressione **CTRL + SHIFT + E** para executar o código e implantar o projeto.

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
- Considere a possibilidade de outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com o SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS no prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implantar um pacote do SSIS com c#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher entre várias ferramentas e linguagens. Para obter mais informações, consulte os seguintes artigos:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com c#](./ssis-quickstart-run-dotnet.md) 

