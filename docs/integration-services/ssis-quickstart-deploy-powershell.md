---
title: Implantar um projeto do SSIS com o PowerShell | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 37fe358eb7e11cb878ebd9b0c8356ac2295ca7e9
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-powershell"></a>Implantar um projeto do SSIS com o PowerShell
Este tutorial de início rápido demonstra como usar um script do PowerShell para se conectar a um servidor de banco de dados e implantar um projeto do SSIS no catálogo do SSIS.

## <a name="powershell-script"></a>Script do PowerShell
Forneça os valores adequados para as variáveis na parte superior do script a seguir e, em seguida, execute o script para implantar o projeto do SSIS.

> [!NOTE]
> O exemplo a seguir usa a autenticação do Windows. Para usar a autenticação do SQL Server, substitua o `Integrated Security=SSPI;` argumento com `User ID=<user name>;Password=<password>;`.

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
- Considere a possibilidade de outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com o SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS no prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com c#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher entre várias ferramentas e linguagens. Para obter mais informações, consulte os seguintes artigos:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com c#](./ssis-quickstart-run-dotnet.md) 

