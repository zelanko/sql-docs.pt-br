---
title: Funções valorizadas em tabela clr | Microsoft Docs
description: Uma função valorizada em tabela retorna uma tabela. Na integração SQL Server CLR, você pode escrever funções valorizadas em tabela em código gerenciado.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
author: rothja
ms.author: jroth
ms.openlocfilehash: 42391504a8c48248e47b5f09e8feb31b613bbfca
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488449"
---
# <a name="clr-table-valued-functions"></a>Funções com valor de tabela CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Uma função com valor de tabela é uma função definida pelo usuário que retorna uma tabela.  
  
 A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estende a funcionalidade das funções com valor de tabela permitindo definir uma função com valor de tabela em qualquer idioma gerenciado. Os dados são retornados de uma função valorizada à tabela através de um objeto **IEnumerable** ou **IEnumerator.**  
  
> [!NOTE]  
>  Para funções valorizadas em tabela, as colunas do tipo de tabela de retorno não podem incluir colunas de carimbo de tempo ou colunas de tipo de dados de seqüência não-Unicode (como **char,** **varchar**e **texto).** Não tem suporte para a restrição NOT NULL.  
  
 Para obter mais informações sobre funções valorizadas pela tabela CLR, confira a introdução da tabela [SQL Server CLR da MSSQLTips às funções valorizadas da tabela ClR do Servidor SQL!](https://www.mssqltips.com/sqlservertip/2582/introduction-to-sql-server-clr-table-valued-functions/)  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Diferenças entre as funções com valor de tabela Transact-SQL e CLR  
 As funções com valor de tabela do [!INCLUDE[tsql](../../includes/tsql-md.md)] materializam os resultados chamando a função em uma tabela intermediária. Como elas usam uma tabela intermediária, podem dar suporte a restrições e índices exclusivos nos resultados. Esses recursos podem ser extremamente úteis quando resultados grandes são retornados.  
  
 Em contrapartida, as funções com valor de tabela do CLR representam uma alternativa de streaming. Não há nenhum requisito de que todo o conjunto de resultados deva ser materializado em uma única tabela. O objeto **IEnumerable** retornado pela função gerenciada é diretamente chamado pelo plano de execução da consulta que chama a função de valor de tabela, e os resultados são consumidos de forma incremental. Este modelo de streaming garante que os resultados possam ser consumidos imediatamente depois que a primeira linha estiver disponível, em vez de aguardar até que toda a tabela seja populada. Ele também será a melhor alternativa, se você tiver uma grande quantidade de linhas retornadas, pois elas não precisam ser totalmente materializadas na memória. Por exemplo, uma função com valor de tabela gerenciada pode ser usada para analisar um arquivo de texto e retornar todas as linhas como uma linha.  
  
## <a name="implementing-table-valued-functions"></a>Implementando funções com valor de tabela  
 Implemente as funções com valor de tabela como métodos em uma classe em um assembly do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Seu código de função avaliado em tabela deve implementar a interface **IEnumerable.** A interface **IEnumerable** é definida no Quadro .NET. Os tipos que representam matrizes e coleções no .NET Framework já implementam a interface **IEnumerable.** Isso facilita a gravação de funções com valor de tabela que convertem uma coleção ou uma matriz em um conjunto de resultados.  
  
## <a name="table-valued-parameters"></a>Parâmetros com valor de tabela  
 Os parâmetros com valor de tabela são tipos de tabela definidos pelo usuário, transmitidos em um procedimento ou função e fornecem uma maneira eficiente de passar várias linhas de dados para o servidor. Os parâmetros com valor de tabela fornecem funcionalidade semelhante para matrizes de parâmetros, mas oferecem maior flexibilidade e integração maior com o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles também fornecem o potencial para melhor desempenho. Os parâmetros com valor de tabela também ajudam a reduzir o número de viagens de ida e volta para o servidor. Em vez de enviar várias solicitações ao servidor, como com uma lista de parâmetros escalares, os dados podem ser enviados ao servidor como um parâmetro com valor de tabela. Um tipo de tabela definido pelo usuário não pode ser passado como um parâmetro com valor de tabela para, ou ser retornado de, um procedimento armazenado ou uma função gerenciada(o) que é executada(o) no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre parâmetros com valor de tabela, consulte [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="output-parameters-and-table-valued-functions"></a>Parâmetros de saída e funções com valor de tabela  
 As informações podem ser retornadas de funções com valor de tabela que usam parâmetros de saída. O parâmetro correspondente na função com valor de tabela do código de implementação deve usar um parâmetro de passagem por referência como o argumento. Observe que o Visual Basic não suporta parâmetros de saída da mesma maneira que o Visual C#. Você deve especificar o parâmetro \<por referência e aplicar o atributo Out()> para representar um parâmetro de saída, como no seguinte:  
  
```vb  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>Definindo uma função com valor de tabela no Transact-SQL  
 A sintaxe para definir uma função de valor [!INCLUDE[tsql](../../includes/tsql-md.md)] de tabela CLR é semelhante à de uma função de valor de tabela, com a adição da cláusula **NOME EXTERNO.** Por exemplo:  
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 As funções com valor de tabela são usadas para representar dados em formato relacional para processamento posterior em consultas como:  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 As funções com valor de tabela podem retornar uma tabela quando:  
  
-   Criadas a partir de argumentos de entrada escalar. Por exemplo, uma função com valor de tabela que usa uma cadeia de caracteres de números delimitada por vírgulas e converte-os em uma tabela.  
  
-   Geradas de dados externos. Por exemplo, uma função com valor de tabela que lê o log de eventos e o expõe como uma tabela.  
  
 **Nota** Uma função valorizada em tabela só [!INCLUDE[tsql](../../includes/tsql-md.md)] pode executar o acesso a dados através de uma consulta no método **InitMethod,** e não no método **FillRow.** O **InitMethod** deve ser marcado com a propriedade **sqlFunction.DataAccess.Read** se uma [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta for realizada.  
  
## <a name="a-sample-table-valued-function"></a>Um exemplo de função com valor de tabela  
 A função com valor de tabela a seguir retorna informações do log de eventos do sistema. A função adota um único argumento de cadeia de caracteres que contém o nome do log de eventos a ser lido.  
  
###### <a name="sample-code"></a>Exemplo de código  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>Declarando e usando a função com valor de tabela de exemplo  
 Depois que a função com valor de tabela de exemplo foi compilada, ela pode ser declarada no [!INCLUDE[tsql](../../includes/tsql-md.md)] da seguinte maneira:  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 Não há suporte para objetos de banco de dados do Visual C++ compilados com /clr:pure para a execução no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Por exemplo, esses objetos de banco de dados incluem funções com valor de tabela.  
  
 Para testar o exemplo, tente o seguinte código [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>Exemplo: Retornando os resultados de uma consulta do SQL Server  
 O exemplo a seguir mostra uma função com valor de tabela que consulta um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este exemplo usa o banco de dados AdventureWorks Light do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Veja [https://www.codeplex.com/sqlserversamples](https://go.microsoft.com/fwlink/?LinkId=87843) mais informações sobre como baixar adventureworks.  
  
 Nomeie seu arquivo de código-fonte como FindInvalidEmails.cs ou FindInvalidEmails.vb.  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 Compile o código-fonte em uma DLL e copie a DLL no diretório raiz de sua unidade C.  Em seguida, execute a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
  
