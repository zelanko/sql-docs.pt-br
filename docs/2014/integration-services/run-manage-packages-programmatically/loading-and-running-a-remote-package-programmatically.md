---
title: Carregando e executando um pacote remoto de forma programática | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- remote packages [Integration Services]
ms.assetid: 9f6ef376-3408-46bf-b5fa-fc7b18c689c9
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: df53d355babd082cba4b67404c91b7d4c33bec28
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37186683"
---
# <a name="loading-and-running-a-remote-package-programmatically"></a>Carregando e executando um pacote remoto programaticamente
  Para executar pacotes remotos de um computador local que não tenha o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado, inicie-os de forma que eles sejam executados no computador remoto em que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está instalado. Para isso, o computador local deve usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, um serviço Web ou um componente remoto para iniciar os pacotes no computador remoto. Se você tentar iniciar os pacotes remotos diretamente do computador local, eles serão carregados e tentarão executar do computador local. Se o computador local não tiver o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado, os pacotes não serão executados.  
  
> [!NOTE]  
>  Não é possível executar pacotes fora do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] em um computador cliente que não tem o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado e os termos do licenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] talvez não permitam a instalação do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em computadores adicionais. O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um componente de servidor e não é redistribuível a computadores cliente.  
  
 Alternadamente, você pode executar um pacote remoto de um computador local que tenha o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado. Para obter mais informações, consulte [Carregando e executando um pacote local de forma programática](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md).  
  
##  <a name="top"></a> Executando um pacote remoto no computador remoto  
 Como mencionado acima, há vários modos com os quais você pode executar um pacote remoto em um servidor remoto:  
  
-   [Usar o SQL Server Agent para executar o pacote remoto de forma programática](#agent)  
  
-   [Usar um serviço Web ou componente remoto para executar o pacote remoto de forma programática](#service)  
  
 Quase todos os métodos que são usados neste tópico para carregar e salvar pacotes requerem uma referência ao assembly `Microsoft.SqlServer.ManagedDTS`. A exceção é a abordagem do ADO.NET demonstrada neste tópico para executar o **sp_start_job** procedimento armazenado, que exige apenas uma referência ao `System.Data`. Depois que você acrescentar a referência ao assembly `Microsoft.SqlServer.ManagedDTS` em um projeto novo, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> com uma instrução `using` ou `Imports`.  
  
###  <a name="agent"></a> Usando o SQL Server Agent para executar um pacote remoto de forma programática no servidor  
 O exemplo do código seguinte demonstra como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent programaticamente para executar um pacote remoto no servidor. O exemplo de código chama o procedimento armazenado do sistema, **sp_start_job**, que inicia um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O trabalho que o procedimento lança é chamado `RunSSISPackage`, e esse trabalho está no computador remoto. O trabalho `RunSSISPackage` executa o pacote no computador remoto.  
  
> [!NOTE]  
>  O valor retornado do procedimento armazenado **sp_start_job** indica se ele pôde iniciar o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com êxito. O valor de retorno não indica se o pacote teve sucesso ou falhou.  
  
 Para obter informações sobre como solucionar problemas de pacotes executados nos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte o artigo da Microsoft, [Um pacote do SSIS não é executado quando chamado em uma etapa de trabalho do SQL Server Agent](http://support.microsoft.com/kb/918760).  
  
### <a name="sample-code"></a>Código de exemplo  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
  
    Dim jobConnection As SqlConnection  
    Dim jobCommand As SqlCommand  
    Dim jobReturnValue As SqlParameter  
    Dim jobParameter As SqlParameter  
    Dim jobResult As Integer  
  
    jobConnection = New SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI")  
    jobCommand = New SqlCommand("sp_start_job", jobConnection)  
    jobCommand.CommandType = CommandType.StoredProcedure  
  
    jobReturnValue = New SqlParameter("@RETURN_VALUE", SqlDbType.Int)  
    jobReturnValue.Direction = ParameterDirection.ReturnValue  
    jobCommand.Parameters.Add(jobReturnValue)  
  
    jobParameter = New SqlParameter("@job_name", SqlDbType.VarChar)  
    jobParameter.Direction = ParameterDirection.Input  
    jobCommand.Parameters.Add(jobParameter)  
    jobParameter.Value = "RunSSISPackage"  
  
    jobConnection.Open()  
    jobCommand.ExecuteNonQuery()  
    jobResult = DirectCast(jobCommand.Parameters("@RETURN_VALUE").Value, Integer)  
    jobConnection.Close()  
  
    Select Case jobResult  
      Case 0  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.")  
      Case Else  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.")  
    End Select  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace LaunchSSISPackageAgent_CS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      SqlConnection jobConnection;  
      SqlCommand jobCommand;  
      SqlParameter jobReturnValue;  
      SqlParameter jobParameter;  
      int jobResult;  
  
      jobConnection = new SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI");  
      jobCommand = new SqlCommand("sp_start_job", jobConnection);  
      jobCommand.CommandType = CommandType.StoredProcedure;  
  
      jobReturnValue = new SqlParameter("@RETURN_VALUE", SqlDbType.Int);  
      jobReturnValue.Direction = ParameterDirection.ReturnValue;  
      jobCommand.Parameters.Add(jobReturnValue);  
  
      jobParameter = new SqlParameter("@job_name", SqlDbType.VarChar);  
      jobParameter.Direction = ParameterDirection.Input;  
      jobCommand.Parameters.Add(jobParameter);  
      jobParameter.Value = "RunSSISPackage";  
  
      jobConnection.Open();  
      jobCommand.ExecuteNonQuery();  
      jobResult = (Int32)jobCommand.Parameters["@RETURN_VALUE"].Value;  
      jobConnection.Close();  
  
      switch (jobResult)  
      {  
        case 0:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.");  
          break;  
        default:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.");  
          break;  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
 
  
###  <a name="service"></a> Usando um serviço Web ou componente remoto para executar um pacote remoto de forma programática  
 A solução anterior para executar pacotes programaticamente no servidor não requer nenhum código personalizado no servidor. Porém, você pode preferir uma solução que não confie no SQL Server Agent para executar pacotes. O exemplo seguinte demonstra um serviço Web que pode ser criado no servidor para iniciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] localmente, e um aplicativo de teste que pode ser usado para chamar o serviço Web de um computador cliente. Se preferir criar um componente remoto em vez de um serviço Web, use a mesma lógica de código com poucas alterações em um componente remoto. Porém, um componente remoto pode requerer configurações mais extensas que um serviço Web.  
  
> [!IMPORTANT]  
>  Com suas configurações padrão de autenticação e autorização, um serviço Web geralmente não tem permissões suficientes para acessar o SQL Server ou o sistema de arquivos para carregar e executar pacotes. Talvez você precise atribuir permissões apropriadas ao serviço Web definindo suas configurações de autenticação e autorização no arquivo **web.config** e atribuindo permissões de banco de dados e sistema de arquivos, conforme necessário. Uma discussão completa sobre permissões de Web, banco de dados e sistema de arquivos estão além do escopo deste tópico.  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para funcionar com o Repositório de Pacotes do SSIS dão suporte apenas a “.”, localhost ou ao nome do servidor local. Você não pode usar "(local)".  
  
### <a name="sample-code"></a>Código de exemplo  
 Os exemplos de código seguintes mostram como criar e testar o serviço Web.  
  
#### <a name="creating-the-web-service"></a>Criando o serviço Web  
 Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode ser carregado diretamente de um arquivo, diretamente de um SQL Server ou do Armazenamento de Pacotes SSIS, que gerencia o armazenamento de pacotes no SQL Server e em pastas especiais de sistema de arquivos. Esse exemplo suporta todas as opções disponíveis usando uma construção `Select Case` ou `switch` para selecionar a sintaxe apropriada para iniciar o pacote e concatenar os argumentos de entrada adequadamente. O método LaunchPackage do serviço Web retorna o resultado da execução do pacote como um valor inteiro em vez de um valor <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>, de forma que os computadores cliente não requeiram uma referência a qualquer assembly do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
###### <a name="to-create-a-web-service-to-run-packages-on-the-server-programmatically"></a>Para criar um serviço Web para executar pacotes programaticamente no servidor  
  
1.  Abra o Visual Studio e crie um projeto de serviço Web na linguagem de programação de sua preferência. O código de exemplo usa o nome LaunchSSISPackageService para o projeto.  
  
2.  Adicione uma referência ao `Microsoft.SqlServer.ManagedDTS` e adicione uma `Imports` ou `using` instrução ao arquivo de código para o **SQLServer** namespace.  
  
3.  Cole o código de exemplo para o método LaunchPackage do serviço Web na classe. (O exemplo mostra os conteúdos inteiros da janela de código).  
  
4.  Construa e teste o serviço Web fornecendo um conjunto de valores válidos para os argumentos de entrada do método LaunchPackage que aponte para um pacote existente. Por exemplo, se o pacote package1.dtsx estiver armazenado no servidor em C:\Meus Pacotes, passe "arquivo" como valor de sourceType, "C:\Meus Pacotes" como valor de sourceLocation e "package1" (sem a extensão) como o valor de packageName.  
  
```vb  
Imports System.Web  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.IO  
  
<WebService(Namespace:="http://dtsue/")> _  
<WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _  
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _  
Public Class LaunchSSISPackageService  
  Inherits System.Web.Services.WebService  
  
  ' LaunchPackage Method Parameters:  
  ' 1. sourceType: file, sql, dts  
  ' 2. sourceLocation: file system folder, (none), logical folder  
  ' 3. packageName: for file system, ".dtsx" extension is appended  
  
  <WebMethod()> _  
  Public Function LaunchPackage( _  
    ByVal sourceType As String, _  
    ByVal sourceLocation As String, _  
    ByVal packageName As String) As Integer 'DTSExecResult  
  
    Dim packagePath As String  
    Dim myPackage As Package  
    Dim integrationServices As New Application  
  
    ' Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName)  
  
    Select Case sourceType  
      Case "file"  
        ' Package is stored as a file.  
        ' Add extension if not present.  
        If String.IsNullOrEmpty(Path.GetExtension(packagePath)) Then  
          packagePath = String.Concat(packagePath, ".dtsx")  
        End If  
        If File.Exists(packagePath) Then  
          myPackage = integrationServices.LoadPackage(packagePath, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid file location: " & packagePath)  
        End If  
      Case "sql"  
        ' Package is stored in MSDB.  
        ' Combine logical path and package name.  
        If integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty) Then  
          myPackage = integrationServices.LoadFromSqlServer( _  
            packageName, "(local)", String.Empty, String.Empty, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case "dts"  
        ' Package is managed by SSIS Package Store.  
        ' Default logical paths are File System and MSDB.  
        If integrationServices.ExistsOnDtsServer(packagePath, ".") Then  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case Else  
        Throw New ApplicationException( _  
          "Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.")  
    End Select  
  
    Return myPackage.Execute()  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.IO;  
  
[WebService(Namespace = "http://dtsue/")]  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
public class LaunchSSISPackageServiceCS : System.Web.Services.WebService  
{  
  public LaunchSSISPackageServiceCS()  
  {  
    }  
  
  // LaunchPackage Method Parameters:  
  // 1. sourceType: file, sql, dts  
  // 2. sourceLocation: file system folder, (none), logical folder  
  // 3. packageName: for file system, ".dtsx" extension is appended  
  
  [WebMethod]  
  public int LaunchPackage(string sourceType, string sourceLocation, string packageName)  
  {   
  
    string packagePath;  
    Package myPackage;  
    Application integrationServices = new Application();  
  
    // Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName);  
  
    switch(sourceType)  
    {  
      case "file":  
        // Package is stored as a file.  
        // Add extension if not present.  
        if (String.IsNullOrEmpty(Path.GetExtension(packagePath)))  
        {  
          packagePath = String.Concat(packagePath, ".dtsx");  
        }  
        if (File.Exists(packagePath))  
        {  
          myPackage = integrationServices.LoadPackage(packagePath, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid file location: "+packagePath);  
        }  
        break;  
      case "sql":  
        // Package is stored in MSDB.  
        // Combine logical path and package name.  
        if (integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty))  
        {  
          myPackage = integrationServices.LoadFromSqlServer(packageName, "(local)", String.Empty, String.Empty, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      case "dts":  
        // Package is managed by SSIS Package Store.  
        // Default logical paths are File System and MSDB.  
        if (integrationServices.ExistsOnDtsServer(packagePath, "."))  
        {  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      default:  
        throw new ApplicationException("Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.");  
    }  
  
    return (Int32)myPackage.Execute();  
  
  }  
  
}  
```  
  
#### <a name="testing-the-web-service"></a>Testando o serviço Web  
 O aplicativo de console do exemplo seguinte usa o serviço Web para executar um pacote. O método LaunchPackage do serviço Web retorna o resultado da execução do pacote como um inteiro, em vez de um valor <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>, de forma que os computadores cliente não exijam uma referência a nenhum assembly do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O exemplo cria uma enumeração privada cujos valores espelham os valores <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> para informar os resultados da execução.  
  
###### <a name="to-create-a-console-application-to-test-the-web-service"></a>Para criar um aplicativo de console para testar o serviço Web  
  
1.  No Visual Studio, adicione um aplicativo de console novo usando a linguagem de programação de sua preferência para a mesma solução que contém o projeto de serviço Web. O código de exemplo usa o nome LaunchSSISPackageTest para o projeto.  
  
2.  Defina o aplicativo de console novo como o projeto de inicialização na solução.  
  
3.  Adicione uma referência Web ao projeto de serviço Web. Se necessário, ajuste a declaração variável no código de exemplo para o nome que você atribui ao objeto de proxy de serviço Web.  
  
4.  Cole o código de exemplo para a rotina principal e a enumeração privada no código. (O exemplo mostra os conteúdos inteiros da janela de código).  
  
5.  Edite a linha de código, que chama o método LaunchPackage para fornecer um conjunto de valores válidos para os argumentos de entrada, que aponte para um pacote existente. Por exemplo, se package1.dtsx estiver armazenado no servidor em C:\Meus Pacotes, passe "arquivo" como valor de `sourceType`, "C:\Meus Pacotes" como valor de `sourceLocation` e "package1" (sem a extensão) como o valor de `packageName`.  
  
```vb  
Module LaunchSSISPackageTest  
  
  Sub Main()  
  
    Dim launchPackageService As New LaunchSSISPackageService.LaunchSSISPackageService  
    Dim packageResult As Integer  
  
    Try  
      packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage")  
    Catch ex As Exception  
      ' The type of exception returned by a Web service is:  
      '  System.Web.Services.Protocols.SoapException  
      Console.WriteLine("The following exception occurred: " & ex.Message)  
    End Try  
  
    Console.WriteLine(CType(packageResult, PackageExecutionResult).ToString)  
    Console.ReadKey()  
  
  End Sub  
  
  Private Enum PackageExecutionResult  
    PackageSucceeded  
    PackageFailed  
    PackageCompleted  
    PackageWasCancelled  
  End Enum  
  
End Module  
```  
  
```csharp  
using System;  
  
namespace LaunchSSISPackageSvcTestCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS launchPackageService = new LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS();  
      int packageResult = 0;  
  
      try  
      {  
        packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage");  
      }  
      catch (Exception ex)  
      {  
        // The type of exception returned by a Web service is:  
        //  System.Web.Services.Protocols.SoapException  
        Console.WriteLine("The following exception occurred: " + ex.Message);  
      }  
  
      Console.WriteLine(((PackageExecutionResult)packageResult).ToString());  
      Console.ReadKey();  
  
    }  
  
    private enum PackageExecutionResult  
    {  
      PackageSucceeded,  
      PackageFailed,  
      PackageCompleted,  
      PackageWasCancelled  
    };  
  
  }  
}  
```  
  

  
## <a name="external-resources"></a>Recursos externos  
  
-   Vídeo [Como automatizar a execução de pacote do SSIS usando o SQL Server Agent (vídeo do SQL Server)](http://technet.microsoft.com/sqlserver/ff686764.aspx), em technet.microsoft.com  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Compreender as diferenças entre execução local e remota](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Carregando e executando um pacote local de forma programática](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Carregar a saída de um pacote local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
