---
title: Adicionar conexões programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: building-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- connection managers [Integration Services], packages
- Integration Services packages, connections
- connections [Integration Services], packages
- SSIS packages, connections
- packages [Integration Services], connections
- intrinsic properties [Integration Services]
- SQL Server Integration Services packages, connections
- ConnectionManager class
- SSIS connection managers
- adding package connections
ms.assetid: d90716d1-4c65-466c-b82c-4aabbee1e3e5
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1908071386fccc88b94d9dc44ab239271a1c09ca
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="adding-connections-programmatically"></a>Adicionando conexões programaticamente
  A classe <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> representa conexões físicas com fontes de dados externas. A classe <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> isola os detalhes de implementação da conexão do tempo de execução. Isso permite que o tempo de execução interaja com cada gerenciador de conexões de uma maneira consistente e previsível. Gerenciadores de conexões contêm um conjunto de propriedades de estoque que todas as conexões têm em comum, como <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ID%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>. Porém, as propriedades <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> são, ordinariamente, as únicas propriedades necessárias para configurar um gerenciador de conexões. Ao contrário de outros paradigmas de programação em que as classes de conexão expõem métodos como **Open** ou **Connect** para estabelecer fisicamente uma conexão com a fonte de dados, o mecanismo de tempo de execução gerencia todas as conexões para o pacote enquanto ele é executado.  
  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Connections> é uma coleção dos gerenciadores de conexões que foram adicionados ao pacote e estão disponíveis para uso em tempo de execução. É possível adicionar mais gerenciadores de conexões à coleção usando o método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> da coleção e fornecendo uma cadeia de caracteres que indica o tipo de gerenciador de conexões. O método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> retorna a instância <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> que foi acrescentada ao pacote.  
  
## <a name="intrinsic-properties"></a>Propriedades intrínsecas  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> expõe um conjunto de propriedades que são comuns a todas as conexões. Porém, às vezes você precisa de acesso a propriedades que são exclusivas ao tipo de conexão específico. A coleção <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Properties%2A> da classe <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> fornece acesso a essas propriedades. As propriedades podem ser recuperadas da coleção usando o indexador ou o nome da propriedade e o método **GetValue**, sendo que os valores são definidos usando o método **SetValue**. As propriedades das propriedades do objeto de conexão subjacente também podem ser definidas adquirindo-se uma instância real do objeto e definindo suas propriedades diretamente. Para obter a conexão subjacente, use a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.InnerObject%2A> do gerenciador de conexões. A linha de código seguinte mostra uma linha C# que cria um gerenciador de conexões ADO.NET que tem a classe subjacente <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.ConnectionManagerAdoNetClass>.  
  
 `ConnectionManagerAdoNetClass cmado = cm.InnerObject as ConnectionManagerAdoNet;`  
  
 Isso converte o objeto do gerenciador de conexões gerenciado em seu objeto de conexão subjacente. Se você estiver usando C++, o método **QueryInterface** do objeto <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> será chamado e a interface do objeto de conexão subjacente será solicitado.  
  
 A tabela a seguir lista os gerenciadores de conexão incluídos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. e a cadeia de caracteres que é usada na instrução `package.Connections.Add("xxx")`. Para saber mais sobre gerenciadores de conexões, consulte [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
|Cadeia de caracteres|Gerenciador de conexões|  
|------------|------------------------|  
|"OLEDB"|Gerenciador de conexões para conexões OLE DB.|  
|"ODBC"|Gerenciador de conexões para conexões ODBC.|  
|"ADO"|Gerenciador de conexões para conexões ADO.|  
|"ADO.NET:SQL"|Gerenciador de conexões para conexões ADO.NET (provedor de dados SQL).|  
|"ADO.NET:OLEDB"|Gerenciador de conexões para conexões ADO.NET (provedor de dados OLE DB).|  
|"FLATFILE"|Gerenciador de conexões para conexões de arquivo simples.|  
|"FILE"|Gerenciador de conexões para conexões de arquivo.|  
|"MULTIFLATFILE"|Gerenciador de conexões para múltiplas conexões de arquivo simples.|  
|"MULTIFILE"|Gerenciador de conexões para múltiplas conexões de arquivo.|  
|"SQLMOBILE"|Gerenciador de conexões para conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.|  
|"MSOLAP100"|Gerenciador de conexões para conexões [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|"FTP"|Gerenciador de conexões para conexões FTP.|  
|"HTTP"|Gerenciador de conexões para conexões HTTP.|  
|"MSMQ"|Gerenciador de conexões para conexões do serviço de enfileiramento de mensagens (também conhecido como MSMQ).|  
|"SMTP"|Gerenciador de conexões para conexões SMTP.|  
|"WMI"|Gerenciador de conexões para conexões do Microsoft Windows Management Instrumentation (WMI).|  
  
 O exemplo de código a seguir demonstra como adicionar uma conexão OLE DB e FILE à coleção <xref:Microsoft.SqlServer.Dts.Runtime.Package.Connections%2A> de um <xref:Microsoft.SqlServer.Dts.Runtime.Package>. Em seguida, o exemplo define as propriedades <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A>.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      // Create a package, and retrieve its connections.  
      Package pkg = new Package();  
      Connections pkgConns = pkg.Connections;  
  
      // Add an OLE DB connection to the package, using the   
      // method defined in the AddConnection class.  
      CreateConnection myOLEDBConn = new CreateConnection();  
      myOLEDBConn.CreateOLEDBConnection(pkg);  
  
      // View the new connection in the package.  
      Console.WriteLine("Connection description: {0}",  
         pkg.Connections["SSIS Connection Manager for OLE DB"].Description);  
  
      // Add a second connection to the package.  
      CreateConnection myFileConn = new CreateConnection();  
      myFileConn.CreateFileConnection(pkg);  
  
      // View the second connection in the package.  
      Console.WriteLine("Connection description: {0}",  
        pkg.Connections["SSIS Connection Manager for Files"].Description);  
  
      Console.WriteLine();  
      Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count);  
  
      Console.Read();  
    }  
  }  
  // <summary>  
  // This class contains the definitions for multiple  
  // connection managers.  
  // </summary>  
  public class CreateConnection  
  {  
    // Private data.  
    private ConnectionManager ConMgr;  
  
    // Class definition for OLE DB Provider.  
    public void CreateOLEDBConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("OLEDB");  
      ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" +  
        "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" +  
        "Data Source=(local);";  
      ConMgr.Name = "SSIS Connection Manager for OLE DB";  
      ConMgr.Description = "OLE DB connection to the AdventureWorks database.";  
    }  
    public void CreateFileConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("File");  
      ConMgr.ConnectionString = @"\\<yourserver>\<yourfolder>\books.xml";  
      ConMgr.Name = "SSIS Connection Manager for Files";  
      ConMgr.Description = "Flat File connection";  
    }  
  }  
  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    ' Create a package, and retrieve its connections.  
    Dim pkg As New Package()  
    Dim pkgConns As Connections = pkg.Connections  
  
    ' Add an OLE DB connection to the package, using the   
    ' method defined in the AddConnection class.  
    Dim myOLEDBConn As New CreateConnection()  
    myOLEDBConn.CreateOLEDBConnection(pkg)  
  
    ' View the new connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for OLE DB").Description)  
  
    ' Add a second connection to the package.  
    Dim myFileConn As New CreateConnection()  
    myFileConn.CreateFileConnection(pkg)  
  
    ' View the second connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for Files").Description)  
  
    Console.WriteLine()  
    Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
' This class contains the definitions for multiple  
' connection managers.  
  
Public Class CreateConnection  
  ' Private data.  
  Private ConMgr As ConnectionManager  
  
  ' Class definition for OLE DB provider.  
  Public Sub CreateOLEDBConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("OLEDB")  
    ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" & _  
      "Data Source=(local);"  
    ConMgr.Name = "SSIS Connection Manager for OLE DB"  
    ConMgr.Description = "OLE DB connection to the AdventureWorks database."  
  End Sub  
  
  Public Sub CreateFileConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("File")  
    ConMgr.ConnectionString = "\\<yourserver>\<yourfolder>\books.xml"  
    ConMgr.Name = "SSIS Connection Manager for Files"  
    ConMgr.Description = "Flat File connection"  
  End Sub  
  
End Class  
```  
  
 **Saída de exemplo:**  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Number of connections in package: 2`  
  
## <a name="external-resources"></a>Recursos externos  
 Artigo técnico, [Connection Strings](http://go.microsoft.com/fwlink/?LinkId=220743) (Cadeias de conexão), em carlprothman.  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Criar Gerenciadores de Conexões](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
