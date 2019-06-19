---
title: Executar um pacote do SSIS com o Transact-SQL (VSCode) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b7e2f45d7204790d9d6db2ce58d94ddc7a4bfacc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65717347"
---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Executar um pacote do SSIS no Visual Studio Code com o Transact-SQL

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este guia de início rápido demonstra como usar o Visual Studio Code para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, usar instruções do Transact-SQL para executar um pacote SSIS armazenado no Catálogo do SSIS.

O Visual Studio Code é um editor de código para Windows, macOS e Linux que dá suporte a extensões, incluindo a extensão `mssql` para se conectar ao Microsoft SQL Server, o Banco de Dados SQL do Azure ou o SQL Data Warehouse do Azure. Para obter mais informações sobre o VSCode, consulte [Visual Studio Code](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você instalou a versão mais recente do Visual Studio Code e carregue a extensão `mssql`. Para baixar essas ferramentas, consulte as seguintes páginas:
-   [Baixar o Visual Studio Code](https://code.visualstudio.com/Download)
-   [extensão mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para executar um pacote do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

-   Banco de Dados SQL do Azure. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para executar um pacote do SSIS no Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="set-language-mode-to-sql-in-vs-code"></a>Definir o modo de linguagem para SQL no VSCode

Para habilitar comandos do `mssql` e T-SQL IntelliSense, defina o modo de linguagem para **SQL** no Visual Studio Code.

1. Abra o Visual Studio Code e, em seguida, abra uma nova janela. 

2. Clique em **Texto sem Formatação** no canto inferior direito da barra de status.

3. No menu suspenso **Selecionar modo de linguagem** que é aberto, selecione ou insira **SQL** e, em seguida, pressione **ENTER** para definir o modo de linguagem para SQL. 

## <a name="for-azure-sql-database-get-the-connection-info"></a>Para o Banco de Dados SQL do Azure, obtenha as informações de conexão

Para executar o pacote no Banco de Dados SQL do Azure, obtenha as informações de conexão necessárias para se conectar ao SSISDB (banco de dados de catálogo do SSIS). Você precisa das informações de logon e de nome do servidor totalmente qualificado nos procedimentos a seguir.

1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. Selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados do SSISDB na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor. Para ver a opção **Clique para copiar**, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do servidor de Banco de Dados SQL do Azure, navegue até a página do servidor de Banco de Dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.

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
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Se estiver se conectando a um servidor de Banco de Dados SQL do Azure, o nome estará neste formato: `<server_name>.database.windows.net`. |
   | **Nome do banco de dados** | **SSISDB** | O nome do banco de dados ao qual se conectar. |
   | **Autenticação** | Logon do SQL | Com a autenticação do SQL Server, você pode se conectar ao SQL Server ou ao Banco de Dados SQL do Azure. Se você estiver se conectando a um servidor de Banco de Dados SQL do Azure, não poderá usar a autenticação do Windows. |
   | **User name** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha (logon do SQL)** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |
   | **Salvar senha?** | Sim ou Não | Se você não deseja inserir a senha a cada vez, selecione Sim. |
   | **Inserir um nome para este perfil** | Um nome de perfil, assim como **mySSISServer** | Um nome de perfil salvo acelera sua conexão em logons subsequentes. | 

5. Pressione a tecla **ESC** para fechar a mensagem de informações que informa que o perfil está criado e conectado.

6. Verifique sua conexão na barra de status.

## <a name="run-the-t-sql-code"></a>Executar o código T-SQL
Execute o seguinte código Transact-SQL para executar um pacote do SSIS.

1. Na janela **Editor**, digite a consulta a seguir na janela de consulta vazia. (Esse código é o código gerado pela opção **Script** na caixa de diálogo **Executar Pacote** no SSMS.)

2. Atualizar os valores de parâmetro no procedimento armazenado `catalog.create_execution` para seu sistema.

3. Pressione **CTRL+SHIFT+E** para executar o código e executar o pacote.

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
