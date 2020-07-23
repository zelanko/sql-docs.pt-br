---
title: Implantar um projeto do SSIS com o PowerShell | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e2d9a8e6cc8d071ee6f4c4d7557a437d7806f3d1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921894"
---
# <a name="deploy-an-ssis-project-with-powershell"></a>Implantar um projeto do SSIS com o PowerShell

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Este guia de início rápido demonstra como usar um script do PowerShell para se conectar a um servidor de banco de dados e implantar um projeto do SSIS no Catálogo do SSIS.

## <a name="prerequisites"></a>Prerequisites

Um servidor do Banco de Dados SQL do Azure escuta na porta 1433. Se estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para implantar um projeto do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

-   Banco de Dados SQL do Azure. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS no SQL Server em Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="for-azure-sql-database-get-the-connection-info"></a>Para o Banco de Dados SQL do Azure, obtenha as informações de conexão

Para implantar o projeto no Banco de Dados SQL do Azure, obtenha as informações de conexão necessárias para se conectar ao SSISDB (banco de dados de catálogo do SSIS). Você precisa das informações de logon e de nome do servidor totalmente qualificado nos procedimentos a seguir.

1. Entre no [portal do Azure](https://portal.azure.com/).
2. Selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados do SSISDB na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor. Para ver a opção **Clique para copiar**, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do servidor de Banco de Dados SQL do Azure, navegue até a página do servidor de Banco de Dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.
5. Clique em **Mostrar cadeias de conexão de banco de dados**.
6. Examine a cadeia de conexão **ADO.NET** completa.

## <a name="supported-authentication-method"></a>Método de autenticação compatível

Confira [métodos de autenticação para implantação](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment).

## <a name="ssis-powershell-provider"></a>Provedor do PowerShell do SSIS
Forneça os valores adequados para as variáveis na parte superior do script a seguir e, em seguida, execute o script para implantar o projeto do SSIS.

> [!NOTE]
> O exemplo a seguir usa a Autenticação do Windows para implantar em um SQL Server local. Use o cmdlet `New-PSDive` para estabelecer uma conexão usando a autenticação do SQL Server. Se você estiver se conectando a um servidor de Banco de Dados SQL do Azure, não poderá usar a autenticação do Windows.

```powershell
# Variables
$TargetInstanceName = "localhost\default"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Get the Integration Services catalog
$catalog = Get-Item SQLSERVER:\SSIS\$TargetInstanceName\Catalogs\SSISDB\

# Create the target folder
New-Object "Microsoft.SqlServer.Management.IntegrationServices.CatalogFolder" ($catalog, 
$TargetFolderName,"Folder description") -OutVariable folder
$folder.Create()

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

# Verify packages were deployed.
dir "$($catalog.PSPath)\Folders\$TargetFolderName\Projects\$ProjectName\Packages" | 
SELECT Name, DisplayName, PackageId
```

## <a name="powershell-script"></a>Script do PowerShell
Forneça os valores adequados para as variáveis na parte superior do script a seguir e, em seguida, execute o script para implantar o projeto do SSIS.

> [!NOTE]
> O exemplo a seguir usa a Autenticação do Windows para implantar em um SQL Server local. Para usar a autenticação do SQL Server, substitua o argumento `Integrated Security=SSPI;` com `User ID=<user name>;Password=<password>;`. Se você estiver se conectando a um servidor de Banco de Dados SQL do Azure, não poderá usar a autenticação do Windows.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Create the target folder
$folder = New-Object $SSISNamespace".CatalogFolder" ($catalog, $TargetFolderName,
    "Folder description")
$folder.Create()

Write-Host "Deploying " $ProjectName " project ..."

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

Write-Host "Done."
```

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS por meio do prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com o C#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher uma entre várias ferramentas e linguagens. Para obter mais informações, confira os seguintes artigos:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
