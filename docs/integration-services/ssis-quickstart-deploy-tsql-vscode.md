---
title: Implantar um projeto do SSIS com Transact-SQL (VSCode) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: befa64e6c79a1f1e4fe0604014dbb7c583bf830e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74947168"
---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>Implantar um projeto do SSIS por meio do Visual Studio Code com o Transact-SQL

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este guia de início rápido demonstra como usar o Visual Studio Code para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, usar instruções do Transact-SQL para implantar um projeto do SSIS no Catálogo do SSIS.

O Visual Studio Code é um editor de código para Windows, macOS e Linux que dá suporte a extensões, incluindo a extensão `mssql` para se conectar ao Microsoft SQL Server, o Banco de Dados SQL do Azure ou o SQL Data Warehouse do Azure. Para obter mais informações sobre o VSCode, consulte [Visual Studio Code](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você instalou a versão mais recente do Visual Studio Code e carregue a extensão `mssql`. Para baixar essas ferramentas, consulte as seguintes páginas:
-   [Baixar o Visual Studio Code](https://code.visualstudio.com/Download)
-   [extensão mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para implantar um projeto do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS para o Banco de Dados SQL do Azure. O procedimento armazenado `catalog.deploy_project` espera o caminho para o arquivo `.ispac` no sistema de arquivos local. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS no SQL Server em Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="set-language-mode-to-sql-in-vs-code"></a>Definir o modo de linguagem para SQL no VSCode

Para habilitar comandos do `mssql` e T-SQL IntelliSense, defina o modo de linguagem para **SQL** no Visual Studio Code.

1. Abra o Visual Studio Code e, em seguida, abra uma nova janela. 

2. Clique em **Texto sem Formatação** no canto inferior direito da barra de status.
 
3. No menu suspenso **Selecionar modo de linguagem** que é aberto, selecione ou insira **SQL** e, em seguida, pressione **ENTER** para definir o modo de linguagem para SQL. 

## <a name="supported-authentication-method"></a>Método de autenticação compatível

Confira [métodos de autenticação para implantação](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment).

## <a name="connect-to-the-ssis-catalog-database"></a>Conectar-se ao banco de dados de Catálogo do SSIS

Use o Visual Studio Code para estabelecer uma conexão com o Catálogo do SSIS.

1. No VSCode, pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a paleta de comandos.

2. Digite **sqlcon** e pressione **ENTER**.

3. Pressione **ENTER** para selecionar **Criar Perfil de Conexão**. Esta etapa cria um perfil de conexão para a instância do SQL Server.

4. Siga os prompts para especificar as propriedades de conexão para o novo perfil de conexão. Depois de especificar cada valor, pressione **ENTER** para continuar. 

   | Configuração       | Valor sugerido | Obter mais informações |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | O nome do servidor totalmente qualificado |  |
   | **Nome do banco de dados** | **SSISDB** | O nome do banco de dados ao qual conectar. |
   | **Autenticação** | Logon do SQL | |
   | **Nome de usuário** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (Logon do SQL)** | A senha para sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou não | Se você não deseja inserir a senha a cada vez, selecione Sim. |
   | **Inserir um nome para este perfil** | Um nome de perfil, assim como **mySSISServer** | Um nome de perfil salvo acelera sua conexão em logons subsequentes. | 

5. Pressione a tecla **ESC** para fechar a mensagem de informações que informa que o perfil foi criado e está conectado.

6. Verifique se sua conexão na barra de status.

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
- Execute um pacote implantado. Para executar um pacote, você pode escolher uma entre várias ferramentas e linguagens. Para obter mais informações, confira os seguintes artigos:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
