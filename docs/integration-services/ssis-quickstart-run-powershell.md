---
title: Executar um pacote do SSIS com o PowerShell | Microsoft Docs
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
ms.openlocfilehash: e8dc5d5ef9aaebced036db796e1518bcf929dfef
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="run-an-ssis-package-with-powershell"></a>Executar um pacote do SSIS com o PowerShell
Este tutorial de início rápido demonstra como usar um script do PowerShell para se conectar a um servidor de banco de dados e executar um pacote do SSIS.

## <a name="powershell-script"></a>Script do PowerShell
Forneça os valores adequados para as variáveis na parte superior do script a seguir e, em seguida, execute o script para executar o pacote do SSIS.

> [!NOTE]
> O exemplo a seguir usa a Autenticação do Windows. Para usar a autenticação do SQL Server, substitua o argumento `Integrated Security=SSPI;` com `User ID=<user name>;Password=<password>;`.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

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

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
