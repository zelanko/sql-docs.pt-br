---
title: "Executar um projeto de SSIS com o código .NET (c#) | Microsoft Docs"
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
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 65a8db27af80e5cd7001e9a8777dde3c59e9c55e
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-c-code-in-a-net-app"></a>Executar um pacote do SSIS com o código c# em um aplicativo .NET
Este tutorial de início rápido demonstra como gravar o código c# para se conectar a um servidor de banco de dados e executar um pacote do SSIS.

Você pode usar o Visual Studio, o código do Visual Studio ou outra ferramenta de sua preferência para criar um aplicativo c#.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que o Visual Studio ou código do Visual Studio instalado. Baixe a edição Community gratuita do Visual Studio ou o livre código do Visual Studio, de [Downloads do Visual Studio](https://www.visualstudio.com/downloads/).

> [!NOTE]
> Um servidor de banco de dados de SQL do Azure escuta na porta 1433. Se você está tentando se conectar a um servidor de banco de dados de SQL Azure de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo para que você se conectar com êxito.

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>Obter as informações de conexão se implantado no banco de dados SQL

Se os pacotes são implantados em um banco de dados do SQL Azure, obtenha as informações de conexão que necessárias para se conectar ao banco de dados de catálogo do SSIS (SSISDB). Você precisa das informações de nome e logon do servidor totalmente qualificado nos procedimentos a seguir.

1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu à esquerda e clique em banco de dados do SSISDB no **bancos de dados SQL** página. 
3. Sobre o **visão geral** para seu banco de dados, examine o nome totalmente qualificado do servidor. Para ativar o **clique para copiar** opção, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do banco de dados SQL server, navegue até a página do servidor de banco de dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.
5. Clique em **Mostrar cadeias de conexão de banco de dados**.
6. Examine o completo **ADO.NET** cadeia de caracteres de conexão. O código de exemplo usa um `SqlConnectionStringBuilder` para recriar essa cadeia de caracteres de conexão com os valores de parâmetro individuais que você fornecer.

## <a name="create-a-new-visual-studio-project"></a>Criar um novo projeto do Visual Studio

1. No Visual Studio, escolha **arquivo**, **novo**, **projeto**. 
2. No **novo projeto** caixa de diálogo e expanda **Visual C#**.
3. Selecione **aplicativo de Console** e digite *run_ssis_project* para o nome do projeto.
4. Clique em **Okey** para criar e abrir o novo projeto no Visual Studio.

## <a name="add-references"></a>Adicionar referências
1. No Gerenciador de soluções, clique com botão direito do **referências** pasta e selecione **adicionar referência**. O **Gerenciador de referências** caixa de diálogo é aberta.
2. No **Gerenciador de referências** caixa de diálogo caixa, expanda **Assemblies** e selecione **extensões**.
3. Selecione as duas referências para adicionar a seguintes:
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. Clique o **procurar** botão para adicionar uma referência a **integrationservices**. (Esse assembly é instalado apenas no cache de assembly global (GAC).) O **selecionar os arquivos de referência** caixa de diálogo é aberta.
5. No **selecionar os arquivos de referência** caixa de diálogo, navegue até a pasta GAC que contém o assembly. Normalmente, essa pasta é `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`.
6. Selecione o assembly (ou seja, o arquivo. dll) na pasta e clique em **adicionar**.
7. Clique em **Okey** para fechar o **Gerenciador de referências** caixa de diálogo caixa e adicione as três referências. Para verificar se há referências, verifique o **referências** lista no Gerenciador de soluções.

## <a name="add-the-c-code"></a>Adicione o código c# 
1. Abra **Program.cs**.

2. Substitua o conteúdo do **Program.cs** com o código a seguir. Adicione os valores apropriados para seu servidor, banco de dados, usuário e senha.

> [!NOTE]
> O exemplo a seguir usa a autenticação do Windows. Para usar a autenticação do SQL Server, substitua o `Integrated Security=SSPI;` argumento com `User ID=<user name>;Password=<password>;`.


```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System.Data.SqlClient;

namespace run_ssis_package
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string folderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string packageName = "Package.dtsx";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Get the folder
            CatalogFolder folder = catalog.Folders[folderName];

            // Get the project
            ProjectInfo project = folder.Projects[projectName];

            // Get the package
            PackageInfo package = project.Packages[packageName];

            // Run the package
            package.Execute(false, null);

        }
    }
}
```

## <a name="run-the-code"></a>Execute o código

1. Para executar o aplicativo, pressione **F5**.
2. Verifique se o pacote foi executado conforme o esperado e, em seguida, feche a janela do aplicativo.

## <a name="next-steps"></a>Próximas etapas
- Considere a possibilidade de outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)

