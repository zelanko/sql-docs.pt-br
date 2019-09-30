---
title: Implantar um projeto do SSIS com código .NET (C#) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b943d8e169b589f45c612dccc710e174759ca0ca
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295645"
---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>Implantar um projeto do SSIS com o código C# em um aplicativo .NET

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este guia de início rápido demonstra como gravar código C# para se conectar a um servidor de banco de dados e implantar um projeto do SSIS.

Você pode usar o Visual Studio, o Visual Studio Code ou outra ferramenta de sua preferência para criar um aplicativo C#.

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você tem o Visual Studio ou Visual Studio Code instalado. Baixe a Community Edition gratuita do Visual Studio ou o Visual Studio Code gratuito de [Downloads do Visual Studio](https://www.visualstudio.com/downloads/).

Um servidor de Banco de Dados SQL do Azure escuta na porta 1433. Se estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para implantar um projeto do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

-   Banco de Dados SQL do Azure. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS no SQL Server em Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="for-azure-sql-database-get-the-connection-info"></a>Para o Banco de Dados SQL do Azure, obtenha as informações de conexão

Para implantar o projeto no Banco de Dados SQL do Azure, obtenha as informações de conexão necessárias para se conectar ao SSISDB (banco de dados de catálogo do SSIS). Você precisa das informações de logon e de nome do servidor totalmente qualificado nos procedimentos a seguir.

1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. Selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados do SSISDB na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor. Para ver a opção **Clique para copiar**, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do servidor de Banco de Dados SQL do Azure, navegue até a página do servidor de Banco de Dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.
5. Clique em **Mostrar cadeias de conexão de banco de dados**.
6. Examine a cadeia de conexão **ADO.NET** completa. Opcionalmente, seu código pode usar um `SqlConnectionStringBuilder` para recriar essa cadeia de conexão com os valores de parâmetro individuais que você fornece.

## <a name="create-a-new-visual-studio-project"></a>Criar um novo projeto do Visual Studio

1. No Visual Studio, escolha **Arquivo**, **Novo**, **Projeto**. 
2. Na caixa de diálogo **Novo Projeto**, expanda **Visual C#** .
3. Selecione **Aplicativo de Console** e digite *deploy_ssis_project* para o nome do projeto.
4. Clique em **OK** para criar e abrir o novo projeto no Visual Studio.

## <a name="add-references"></a>Adicionar referências
1. No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e selecione **Adicionar Referência**. A caixa de diálogo **Gerenciador de Referências** é aberta.
2. Na caixa de diálogo **Gerenciador de Referências**, expanda **Assemblies** e selecione **Extensões**.
3. Selecione as duas referências a seguir a serem adicionadas:
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. Clique no botão **Procurar** para adicionar uma referência a **Microsoft.SqlServer.Management.IntegrationServices**. (Esse assembly é instalado apenas no GAC (cache de assembly global).) A caixa de diálogo **selecionar os arquivos a referenciar** é aberta.
5. Na caixa de diálogo **Selecionar os arquivos a referenciar**, navegue até a pasta do GAC que contém o assembly. Normalmente, essa pasta é `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`.
6. Selecione o assembly (ou seja, o arquivo. dll) na pasta e clique em **Adicionar**.
7. Clique em **OK** para fechar a caixa de diálogo **Gerenciador de Referências** e adicione as três referências. Para verificar se as referências estão lá, verifique a lista **Referências** no Gerenciador de Soluções.

## <a name="add-the-c-code"></a>Adicione o código C# 
1. Abra **Program.cs**.

2. Substitua o conteúdo de **Program.cs** pelo código a seguir. Adicione os valores apropriados para seu servidor, banco de dados, usuário e senha.

> [!NOTE]
> O exemplo a seguir usa a Autenticação do Windows. Para usar a autenticação do SQL Server, substitua o argumento `Integrated Security=SSPI;` com `User ID=<user name>;Password=<password>;`. Se você estiver se conectando a um servidor de Banco de Dados SQL do Azure, não poderá usar a autenticação do Windows.

```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System;
using System.Data.SqlClient;
using System.IO;

namespace deploy_ssis_project
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string targetFolderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string projectFilePath = @"C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Create the target folder
            CatalogFolder folder = new CatalogFolder(catalog,
                targetFolderName, "Folder description");
            folder.Create();

            Console.WriteLine("Deploying " + projectName + " project.");

            byte[] projectFile = File.ReadAllBytes(projectFilePath);
            folder.DeployProject(projectName, projectFile);

            Console.WriteLine("Done.");
        }
    }
}
```

## <a name="run-the-code"></a>Executar o código

1. Para executar o aplicativo, pressione **F5**.
2. No SSMS, verifique se que o projeto foi implantado.

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS por meio do prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
- Execute um pacote implantado. Para executar um pacote, você pode escolher uma entre várias ferramentas e linguagens. Para saber mais, veja os tópicos a seguir:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
