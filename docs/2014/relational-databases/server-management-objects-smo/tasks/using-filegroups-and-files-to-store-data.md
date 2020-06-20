---
title: Usando grupos de arquivos e arquivo para armazenar dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
author: stevestein
ms.author: sstein
ms.openlocfilehash: d32daf928392d94fd4d62def6b667892abf0b686
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003449"
---
# <a name="using-filegroups-and-files-to-store-data"></a>Usando grupos de arquivos e arquivos para armazenar dados
  Arquivos de dados são usados para armazenar arquivos de bancos de dados. Os arquivos de dados são subdivididos em grupos de arquivos. O objeto <xref:Microsoft.SqlServer.Management.Smo.Database> tem uma propriedade <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> que referencia um objeto <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection>. Cada objeto <xref:Microsoft.SqlServer.Management.Smo.FileGroup> nessa coleção tem uma propriedade <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A>. Essa propriedade se refere a uma coleção <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> que contém todos os arquivos de dados pertencentes ao banco de dados. Um grupo de arquivos é usado especialmente para agrupar arquivos que são usados para armazenar um objeto de banco de dados. Um dos motivos que leva à difusão de um objeto de banco de dados por vários arquivos é que isso pode melhorar o desempenho, especialmente quando os arquivos são armazenados em unidades de disco diferentes.  
  
 Cada banco de dados que é criado automaticamente tem um grupo de arquivos nomeado "Primário" e um arquivo de dados com o mesmo nome do banco de dados. Outros arquivos e grupos podem ser adicionados às coleções.  
  
## <a name="examples"></a>Exemplos  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Adicionando FileGroups e DataFiles a um banco de dados no Visual Basic  
 O grupo de arquivos primário e o arquivo de dados são criados automaticamente com valores de propriedade padrão. O exemplo de código especifica alguns valores de propriedade a serem usados. Caso contrário, os valores de propriedade padrão são usados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>Adicionando FileGroups e DataFiles a um banco de dados no Visual C#  
 O grupo de arquivos primário e o arquivo de dados são criados automaticamente com valores de propriedade padrão. O exemplo de código especifica alguns valores de propriedade a serem usados. Caso contrário, os valores de propriedade padrão são usados.  
  
```csharp
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>Adicionando grupos de arquivos e arquivos de dados a um banco de dados no PowerShell  
 O grupo de arquivos primário e o arquivo de dados são criados automaticamente com valores de propriedade padrão. O exemplo de código especifica alguns valores de propriedade a serem usados. Caso contrário, os valores de propriedade padrão são usados.  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>Criando, alterando e removendo um arquivo de log no Visual Basic  
 O exemplo de código cria um objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, altera uma das propriedades e remove-o do banco de dados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>Criando, alterando e removendo um arquivo de log no Visual C#  
 O exemplo de código cria um objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, altera uma das propriedades e remove-o do banco de dados.  
  
```csharp
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.
            lf1.Drop();
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>Criando, alterando e removendo um arquivo de log no PowerShell  
 O exemplo de código cria um objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, altera uma das propriedades e remove-o do banco de dados.  
  
```powershell
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()
```  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [Arquivos e grupos de arquivos do banco de dados](../../databases/database-files-and-filegroups.md)  
