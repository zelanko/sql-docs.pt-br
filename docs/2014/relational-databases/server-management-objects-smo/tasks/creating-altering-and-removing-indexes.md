---
title: Criando, alterando e removendo índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- indexes [SMO]
ms.assetid: ad1befa5-46e0-4895-b9d3-42852e07607b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f7f71e75d2afd12de9ff381bdc61b739eb192db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782472"
---
# <a name="creating-altering-and-removing-indexes"></a>Criando, alterando e removendo índices
  Na hierarquia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), os índices são representados pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Index>. As colunas indexadas são representadas por uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.IndexedColumn> representada pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Index.IndexedColumns%2A>.  
  
 Você pode criar um índice em uma coluna de XML especificando a propriedade <xref:Microsoft.SqlServer.Management.Smo.Index.IsXmlIndex%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Index>.  
  
## <a name="examples"></a>Exemplos  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-non-clustered-composite-index-in-visual-basic"></a>Criando um índice não clusterizado composto no Visual Basic  
 Este exemplo de código demonstra como criar um índice composto e não clusterizado. Para um índice composto, adicione mais de uma coluna ao índice. Defina a propriedade <xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> como `False` para um índice não clusterizado.  
  
```vb
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Public Class A  
    Public Shared Sub Main()  
        ' Connect to the local, default instance of SQL Server.   
        Dim srv As Server  
        srv = New Server()  
  
        ' Reference the AdventureWorks2012 database.   
        Dim db As Database  
        db = srv.Databases("AdventureWorks2012")  
  
        ' Declare a Table object and reference the HumanResources table.   
        Dim tb As Table  
        tb = db.Tables("Employee", "HumanResources")  
  
        ' Define an Index object variable by providing the parent table and index name in the constructor.   
        Dim idx As Index  
        idx = New Index(tb, "TestIndex")  
  
        ' Add indexed columns to the index.   
        Dim icol1 As IndexedColumn  
        icol1 = New IndexedColumn(idx, "BusinessEntityID", True)  
        idx.IndexedColumns.Add(icol1)  
        Dim icol2 As IndexedColumn  
        icol2 = New IndexedColumn(idx, "HireDate", True)  
        idx.IndexedColumns.Add(icol2)  
  
        ' Set the index properties.   
        idx.IndexKeyType = IndexKeyType.DriUniqueKey  
        idx.IsClustered = False  
        idx.FillFactor = 50  
  
        ' Create the index on the instance of SQL Server.   
        idx.Create()  
  
        ' Modify the page locks property.   
        idx.DisallowPageLocks = True  
  
        ' Run the Alter method to make the change on the instance of SQL Server.   
        idx.Alter()  
  
        ' Remove the index from the table.   
        idx.Drop()  
    End Sub  
End Class
```  
  
## <a name="creating-a-non-clustered-composite-index-in-visual-c"></a>Criando um índice não clusterizado composto no Visual C#  
 Este exemplo de código demonstra como criar um índice composto e não clusterizado. Para um índice composto, adicione mais de uma coluna ao índice. Defina a propriedade <xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> como `False` para um índice não clusterizado.  
  
```csharp
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.   
      Server srv;  
      srv = new Server();  
  
      // Reference the AdventureWorks2012 database.   
      Database db;  
      db = srv.Databases["AdventureWorks2012"];  
  
      // Declare a Table object and reference the HumanResources table.   
      Table tb;  
      tb = db.Tables["Employee", "HumanResources"];  
  
      // Define an Index object variable by providing the parent table and index name in the constructor.   
      Index idx;  
      idx = new Index(tb, "TestIndex");  
  
      // Add indexed columns to the index.   
      IndexedColumn icol1;  
      icol1 = new IndexedColumn(idx, "BusinessEntityID", true);  
      idx.IndexedColumns.Add(icol1);  
      IndexedColumn icol2;  
      icol2 = new IndexedColumn(idx, "HireDate", true);  
      idx.IndexedColumns.Add(icol2);  
  
      // Set the index properties.   
      idx.IndexKeyType = IndexKeyType.DriUniqueKey;  
      idx.IsClustered = false;  
      idx.FillFactor = 50;  
  
      // Create the index on the instance of SQL Server.   
      idx.Create();  
  
      // Modify the page locks property.   
      idx.DisallowPageLocks = true;  
  
      // Run the Alter method to make the change on the instance of SQL Server.   
      idx.Alter();  
  
      // Remove the index from the table.   
      idx.Drop();  
   }  
}
```  
  
## <a name="creating-a-non-clustered-composite-index-in-powershell"></a>Criando um índice composto não clusterizado no PowerShell  
 Este exemplo de código demonstra como criar um índice composto e não clusterizado. Para um índice composto, adicione mais de uma coluna ao índice. Defina a propriedade <xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> como `False` para um índice não clusterizado.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get a reference to the table  
$tb = Get-Item HumanResources.Employee  
  
#Define an Index object variable by providing the parent table and index name in the constructor.
$idx = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "TestIndex"  
  
#Add indexed columns to the index.
$icol1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "BusinessEntityId", $true  
$idx.IndexedColumns.Add($icol1)  
  
$icol2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "HireDate", $true  
$idx.IndexedColumns.Add($icol2)  
  
#Set the index properties.
$idx.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriUniqueKey
$idx.IsClustered = $false  
$idx.FillFactor = 50  
  
#Create the index on the instance of SQL Server.
$idx.Create()  
  
#Modify the page locks property.
$idx.DisallowPageLocks = $true
  
#Run the Alter method to make the change on the instance of SQL Server.
$idx.Alter()  
  
#Remove the index from the table.
$idx.Drop();  
```  
  
## <a name="creating-an-xml-index-in-visual-basic"></a>Criando um índice XML no Visual Basic  
 Este exemplo de código mostra como criar um índice XML em um tipo de dados XML. O tipo de dados de XML é uma coleção de esquemas XML chamada MySampleCollection que é criada em [Using XML Schemas](using-xml-schemas.md). Os índices XML têm algumas restrições; uma delas é que eles devem ser criados em uma tabela que já possui uma chave primária clusterizada.  
  
```vb
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
    Public Shared Sub Main()  
        ' Connect to the local, default instance of SQL Server.   
        Dim srv As Server  
        srv = New Server()  
        Dim db1 As Database = srv.Databases("TESTDB")  
        ' Define a Table object variable and add an XML type column.   
        Dim tb As New Table(db1, "XmlTable3")  
  
        Dim mySample As New XmlSchemaCollection(db1, "Sample4", "dbo")  
        mySample.Text = "<xsd:schema xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" targetNamespace=""NS2""> <xsd:element name=""elem1"" type=""xsd:integer""/></xsd:schema>"  
        mySample.Create()  
  
        Dim col11 As Column  
  
        ' This sample requires that an XML schema type called MySampleCollection exists on the database.   
        col11 = New Column(tb, "XMLValue", DataType.Xml("Sample4"))  
  
        ' Add another integer column that can be made into a unique, primary key.   
        tb.Columns.Add(col11)  
        Dim col21 As Column  
        col21 = New Column(tb, "Number", DataType.Int)  
        col21.Nullable = False  
        tb.Columns.Add(col21)  
  
        ' Create the table of the instance of SQL Server.   
        tb.Create()  
  
        ' Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
        Dim cp As Index  
        cp = New Index(tb, "clusprimindex3")  
        cp.IsClustered = True  
        cp.IndexKeyType = IndexKeyType.DriPrimaryKey  
        Dim cpcol As IndexedColumn  
        cpcol = New IndexedColumn(cp, "Number", True)  
        cp.IndexedColumns.Add(cpcol)  
        cp.Create()  
  
        ' Define and XML Index object variable by supplying the parent table and the XML index name arguments in the constructor.   
        Dim i As Index  
        i = New Index(tb, "xmlindex")  
        Dim ic As IndexedColumn  
        ic = New IndexedColumn(i, "XMLValue", True)  
        i.IndexedColumns.Add(ic)  
  
        ' Create the XML index on the instance of SQL Server.   
        i.Create()  
    End Sub  
End Class
```  
  
## <a name="creating-an-xml-index-in-visual-c"></a>Criando um índice de XML no Visual C#  
 Este exemplo de código mostra como criar um índice XML em um tipo de dados XML. O tipo de dados de XML é uma coleção de esquemas XML chamada MySampleCollection que é criada em [Using XML Schemas](using-xml-schemas.md). Os índices XML têm algumas restrições; uma delas é que eles devem ser criados em uma tabela que já possui uma chave primária clusterizada.  
  
```csharp
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.   
      Server srv;  
      srv = new Server();  
      Database db1 = srv.Databases["TESTDB"];  
      // Define a Table object variable and add an XML type column.   
      Table tb = new Table(db1, "XmlTable3");  
  
      XmlSchemaCollection mySample = new XmlSchemaCollection(db1, "Sample4", "dbo");  
      mySample.Text = "<xsd:schema xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" targetNamespace=\"NS2\"> <xsd:element name=\"elem1\" type=\"xsd:integer\"/></xsd:schema>";  
      mySample.Create();  
  
      Column col11;  
  
      // This sample requires that an XML schema type called MySampleCollection exists on the database.   
      col11 = new Column(tb, "XMLValue", DataType.Xml("Sample4"));  
  
      // Add another integer column that can be made into a unique, primary key.   
      tb.Columns.Add(col11);  
      Column col21;  
      col21 = new Column(tb, "Number", DataType.Int);  
      col21.Nullable = false;  
      tb.Columns.Add(col21);  
  
      // Create the table of the instance of SQL Server.   
      tb.Create();  
  
      // Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
      Index cp;  
      cp = new Index(tb, "clusprimindex3");  
      cp.IsClustered = true;  
      cp.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      IndexedColumn cpcol;  
      cpcol = new IndexedColumn(cp, "Number", true);  
      cp.IndexedColumns.Add(cpcol);  
      cp.Create();  
  
      // Define and XML Index object variable by supplying the parent table and the XML index name arguments in the constructor.   
      Index i;  
      i = new Index(tb, "xmlindex");  
      IndexedColumn ic;  
      ic = new IndexedColumn(i, "XMLValue", true);  
      i.IndexedColumns.Add(ic);  
  
      // Create the XML index on the instance of SQL Server.   
      i.Create();  
   }  
}
```  
  
## <a name="creating-an-xml-index-in-powershell"></a>Criando um índice XML no PowerShell  
 Este exemplo de código mostra como criar um índice XML em um tipo de dados XML. O tipo de dados de XML é uma coleção de esquemas XML chamada MySampleCollection que é criada em [Using XML Schemas](using-xml-schemas.md). Os índices XML têm algumas restrições; uma delas é que eles devem ser criados em uma tabela que já possui uma chave primária clusterizada.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to adventureworks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
#Define a Table object variable and add an XML type column.
#This sample requires that an XML schema type called MySampleCollection exists on the database.
#See sample on Creating an XML schema to do this  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "XmlTable"  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Xml("MySampleCollection")  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"XMLValue", $Type  
$tb.Columns.Add($col1)  
  
#Add another integer column that can be made into a unique, primary key.
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Number", $Type  
$col2.Nullable = $false  
$tb.Columns.Add($col2)  
  
#Create the table of the instance of SQL Server.
$tb.Create()  
  
#Create a unique, clustered, primary key index on the integer column. This is required for an XML index.
#Define an Index object variable by providing the parent table and index name in the constructor.
$cp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "clusprimindex"
$cp.IsClustered = $true;  
$cp.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriPrimaryKey;  
  
#Create and add an indexed column to the index.
$cpcol = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn -argumentlist $cp, "Number", $true  
$cp.IndexedColumns.Add($cpcol)  
$cp.Create()  
  
#Define and XML Index object variable by supplying the parent table and  
# the XML index name arguments in the constructor.
$i = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "xmlindex"
  
#Create and add an indexed column to the index.
$ic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn -argumentlist $i, "XMLValue", $true
$i.IndexedColumns.Add($ic)  
  
#Create the XML index on the instance of SQL Server  
$i.Create()  
```  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.Index>  
