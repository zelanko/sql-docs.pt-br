---
title: Recuperando dados UDT | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SqlDataReader object
- ADO.NET [CLR integration]
- binding UDTs [CLR integration]
- UDTs [CLR integration], ADO.NET
- assemblies [CLR integration], user-defined types
- query parameters [CLR integration]
- user-defined types [CLR integration], ADO.NET
- bytes [CLR integration]
ms.assetid: 6a98ac8c-0e69-4c03-83a4-2062cb782049
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 61e40a31c7a4ef0b7e00e5af235d033e6fe9d7a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921451"
---
# <a name="accessing-user-defined-types---retrieving-udt-data"></a>Acessando tipos definidos pelo usuário - recuperando dados UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para criar um tipo definido pelo usuário (UDT) no cliente, o assembly que foi registrado como UDT em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar disponível para o aplicativo cliente. O assembly UDT pode ser colocado no mesmo diretório que o aplicativo ou no Cache de Assembly Global (GAC). Também é possível definir uma referência para o assembly em seu projeto.  
  
## <a name="requirements-for-using-udts-in-adonet"></a>Requisitos para usar UDTs no ADO.NET  
 O assembly carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o assembly no cliente devem ser compatíveis para que o UDT seja criado no cliente. Para UDTs definidos com o **nativo** formato de serialização, os assemblies devem ser estruturalmente compatíveis. Para assemblies definidos com o **UserDefined** formato, o assembly deve estar disponível no cliente.  
  
 Não é necessário ter uma cópia do assembly UDT no cliente para recuperar os dados raw de uma coluna UDT em uma tabela.  
  
> [!NOTE]  
>  **SqlClient** pode falhar ao carregar um UDT no caso de versões incompatíveis do UDT ou outros problemas. Nesse caso, use os mecanismos de solução de problemas comuns para determinar porque o assembly que contém o UDT não pode ser localizado pelo aplicativo que fez a chamada. Para obter mais informações, consulte o tópico "Diagnosticando erros com Assistentes para Depuração Gerenciada" na documentação do .NET Framework.  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>Acessando UDTs com um SqlDataReader  
 Um **System.Data.SqlClient.SqlDataReader** pode ser usado no código do cliente para recuperar um conjunto de resultados que contém uma coluna UDT, que é exposta como uma instância do objeto.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra como usar o **principal** método para criar um novo **SqlDataReader** objeto. As ações a seguir ocorrem no exemplo de código:  
  
1.  O método Main cria um novo **SqlDataReader** do objeto e recupera os valores da tabela de pontos, que tem uma coluna UDT denominada Point.  
  
2.  O UDT de Point expõe as coordenadas X e Y definidas como inteiros.  
  
3.  O UDT define um **distância** método e uma **GetDistanceFromXY** método.  
  
4.  O código de exemplo recupera os valores da chave primária e das colunas UDT para demonstrar os recursos do UDT.  
  
5.  O código de exemplo chama o **Point.Distance** e **Point.GetDistanceFromXY** métodos.  
  
6.  Os resultados são exibidos na janela do console.  
  
> [!NOTE]  
>  O aplicativo já deve ter uma referência para o assembly UDT.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module ReadPoints  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the value of the UDT  
                Dim pnt As Point = CType(rdr(1), Point)  
  
             ' You can also use GetSqlValue and GetValue  
             ' Dim pnt As Point = CType(rdr.GetSqlValue(1), Point)  
             ' Dim pnt As Point = CType(rdr.GetValue(1), Point)  
  
                ' Print values  
                Console.WriteLine( _  
                 "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}", _  
                  id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance())  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
         & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
namespace Microsoft.Samples.SqlServer  
{  
class ReadPoints  
{  
static void Main()  
{  
  string connectionString = GetConnectionString();  
  using (SqlConnection cnn = new SqlConnection(connectionString))  
  {  
    cnn.Open();  
    SqlCommand cmd = new SqlCommand(  
       "SELECT ID, Pnt FROM dbo.Points", cnn);  
    SqlDataReader rdr = cmd.ExecuteReader();  
  
    while (rdr.Read())  
    {  
      // Retrieve the value of the Primary Key column  
      int id = rdr.GetInt32(0);  
  
        // Retrieve the value of the UDT  
        Point pnt = (Point)rdr[1];  
  
        // You can also use GetSqlValue and GetValue  
        // Point pnt = (Point)rdr.GetSqlValue(1);  
        // Point pnt = (Point)rdr.GetValue(1);  
  
        Console.WriteLine(  
        "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}",   
        id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance());  
    }  
  rdr.Close();  
  Console.WriteLine("done");  
  }  
  static private string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,   
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="binding-udts-as-bytes"></a>Associando UDTs como bytes  
 Em algumas situações, você pode desejar recuperar os dados raw da coluna UDT. Talvez o tipo não esteja disponível localmente ou você não queira instanciar uma instância uma instância do UDT. Você pode ler os bytes brutos em uma matriz de bytes usando o **GetBytes** método de um **SqlDataReader**. Esse método lê um fluxo de bytes do deslocamento de coluna especificado no buffer de uma matriz, começando com um deslocamento de buffer especificado. Outra opção é usar uma da **GetSqlBytes** ou **GetSqlBinary** métodos e ler todo o conteúdo em uma única operação. De qualquer maneira, o objeto UDT nunca é instanciado; assim, não é necessário definir uma referência para o UDT no assembly cliente.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra como recuperar o **ponto** dados como bytes brutos em uma matriz de bytes usando um **SqlDataReader**. O código usa um **StringBuilder** para converter os bytes brutos em uma representação de cadeia de caracteres a ser exibida na janela do console.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the raw bytes into a byte array  
                Dim buffer(31) As Byte  
                Dim byteCount As Integer = _  
                 CInt(rdr.GetBytes(1, 0, buffer, 0, 31))  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", buffer(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
        string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand("SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Retrieve the raw bytes into a byte array  
                byte[] buffer = new byte[32];  
                long byteCount = rdr.GetBytes(1, 0, buffer, 0, 32);  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", buffer[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
### <a name="example-using-getsqlbytes"></a>Exemplo de uso de GetSqlBytes  
 Este exemplo mostra como recuperar o **ponto** dados como bytes brutos em uma única operação usando o **GetSqlBytes** método. O código usa um **StringBuilder** para converter os bytes brutos em uma representação de cadeia de caracteres a ser exibida na janela do console.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Use SqlBytes to retrieve raw bytes  
                Dim sb As SqlBytes = rdr.GetSqlBytes(1)  
                Dim byteCount As Long = sb.Length  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", sb(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
         string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Use SqlBytes to retrieve raw bytes  
                SqlBytes sb = rdr.GetSqlBytes(1);  
                long byteCount = sb.Length;  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", sb[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="working-with-udt-parameters"></a>Trabalhando com parâmetros UDT  
 Os UDTs podem ser usados como parâmetros de entrada e de saída no código do ADO.NET.  
  
## <a name="using-udts-in-query-parameters"></a>Usando UDTs em parâmetros de consulta  
 Os UDTs podem ser usados como valores de parâmetro ao configurar um **SqlParameter** para um **System.Data.SqlClient.SqlCommand** objeto. O **SqlDbType.Udt** enumeração de um **SqlParameter** objeto é usado para indicar que o parâmetro é um UDT ao chamar o **adicionar** método para o  **Parâmetros** coleção. O **UdtTypeName** propriedade de um **SqlCommand** objeto é usado para especificar o nome totalmente qualificado do UDT no banco de dados usando o *object_name* sintaxe. Embora não seja necessário, o uso do nome totalmente qualificado elimina a ambiguidade do código.  
  
> [!NOTE]  
>  Uma cópia local do assembly UDT deve estar disponível para o projeto cliente.  
  
### <a name="example"></a>Exemplo  
 O código neste exemplo cria **SqlCommand** e **SqlParameter** objetos para inserir dados em uma coluna UDT em uma tabela. O código usa o **SqlDbType.Udt** enumeração para especificar o tipo de dados e o **UdtTypeName** propriedade o **SqlParameter** objeto para especificar o nome totalmente qualificado do UDT no banco de dados.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports system.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim ConnectionString As String = GetConnectionString()  
    Dim cnn As New SqlConnection(ConnectionString)  
    Using cnn  
      Dim cmd As SqlCommand = cnn.CreateCommand()  
      cmd.CommandText = "INSERT INTO dbo.Points (Pnt) VALUES (@Point)"  
      cmd.CommandType = CommandType.Text  
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      param.UdtTypeName = "TestPoint.dbo.Point"      param.Direction = ParameterDirection.Input      param.Value = New Point(5, 6)      cmd.Parameters.Add(param)  
  
      cnn.Open()  
      cmd.ExecuteNonQuery()  
      Console.WriteLine("done")  
    End Using  
  End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  string ConnectionString = GetConnectionString();  
     using (SqlConnection cnn = new SqlConnection(ConnectionString))  
     {  
       SqlCommand cmd = cnn.CreateCommand();  
       cmd.CommandText =   
         "INSERT INTO dbo.Points (Pnt) VALUES (@Point)";  
       cmd.CommandType = CommandType.Text;  
  
       SqlParameter param = new SqlParameter("@Point", SqlDbType.Udt);       param.UdtTypeName = "TestPoint.dbo.Point";       param.Direction = ParameterDirection.Input;       param.Value = new Point(5, 6);       cmd.Parameters.Add(param);  
  
       cnn.Open();  
       cmd.ExecuteNonQuery();  
       Console.WriteLine("done");  
     }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Acessando tipos definidos pelo usuário no ADO.NET](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
  
  
