---
title: "Implantar pacotes no Servidor do Integration Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c26ce7f4-7b34-4c9a-8649-ba767d30c827
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Implantar pacotes no Servidor do Integration Services
  O recurso de implantação de pacotes incremental introduzido no [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] permite que você implante um ou mais pacotes para um projeto novo ou existente, sem implantar o projeto inteiro.  
  
##  <a name="DeployWizard"></a> Implantar pacotes usando o Assistente de implantação do Integration Services  
  
1.  No prompt de comando, execute **isdeploymentwizard.exe** de **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn**. Em computadores de 64 bits, há também uma versão de 32 bits da ferramenta em **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**.  
  
2.  Na página **Selecionar fonte**, mude para **Modelo de implantação do pacote**. Em seguida, selecione a pasta que contém pacotes de código-fonte e configure os pacotes.  
  
3.  Conclua o assistente. Siga as etapas restantes descritas em [Modelo de Implantação do Pacote](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel).  
  
##  <a name="SSMS"></a> Implantar pacotes usando o SQL Server Management Studio  
  
1.  No SQL Server Management Studio, expanda o nó **Catálogos do Integration Services** > **SSISDB** no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse na pasta **Projetos** e clique em **Implantar Projetos**.  
  
3.  Se você vir a página **Introdução** clique em **Avançar** para continuar.  
  
4.  Na página **Selecionar fonte**, mude para **Modelo de implantação do pacote**. Em seguida, selecione a pasta que contém pacotes de código-fonte e configure os pacotes.  
  
5.  Conclua o assistente. Siga as etapas restantes descritas em [Modelo de Implantação do Pacote](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel).  
  
##  <a name="SSDT"></a> Implantar pacotes usando o SQL Server Data Tools (Visual Studio)  
  
1.  No Visual Studio, com um projeto do Integration Services aberto, selecione o pacote ou pacotes que você quer implantar.  
  
2.  Clique com o botão direito do mouse e selecione **Implantar Pacote**. O Assistente de implantação é aberto com os pacotes selecionados configurados como pacotes de código-fonte.  
  
3.  Conclua o assistente. Siga as etapas restantes descritas em [Modelo de Implantação do Pacote](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel).  
  
##  <a name="StoredProcedure"></a> Implantar pacotes usando o procedimento armazenado deploy_packages  
 Você pode usar o procedimento armazenado **[catalog].[ deploy_packages]** para implantar um ou mais pacotes do SSIS no catálogo do SSIS. O exemplo de código a seguir demonstra o uso desse procedimento armazenado para implantar pacotes em um servidor SSIS. Para obter mais informações, consulte [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md).  
  
```  
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
##  <a name="MOMApi"></a> Implantar pacotes usando a API do Modelo de objeto de gerenciamento  
 O exemplo de código a seguir demonstra o uso da API do Modelo de objeto de gerenciamento para implantar pacotes no servidor.  
  
```  
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```  
  
  