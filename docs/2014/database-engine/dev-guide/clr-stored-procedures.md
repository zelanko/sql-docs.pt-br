---
title: Procedimentos armazenados CLR | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration], stored procedures
- stored procedures [CLR integration]
- common language runtime [SQL Server], stored procedures
- building database objects [CLR integration], stored procedures
- output parameters [CLR integration]
- tabular results
ms.assetid: bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f509b2a2544c67c9113bc700b7d98bfd4a24024
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753809"
---
# <a name="clr-stored-procedures"></a>Procedimentos armazenados CLR
  Os procedimentos armazenados são rotinas que não podem ser usadas em expressões escalares. Diferentemente das funções escalares, eles podem retornar resultados tabulares e mensagens para o cliente, invocar instruções DDL (linguagem de definição de dados) e DML (linguagem de manipulação de dados) e retornar parâmetros de saída. Para obter informações sobre as vantagens da integração CLR e escolhendo entre o código gerenciado e [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [visão geral da integração CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-stored-procedures"></a>Requisitos dos procedimentos armazenados CLR  
 No common language runtime (CLR), procedimentos armazenados são implementados como métodos estáticos públicos em uma classe em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] assembly. O método estático pode ser declarado como nulo ou retornar um valor inteiro. Se retornar um valor inteiro, o inteiro retornado será tratado como o código de retorno do procedimento. Por exemplo:  
  
 `EXECUTE @return_status = procedure_name`  
  
 O @return_status variável conterá o valor retornado pelo método. Se o método for declarado nulo, o código de retorno será 0.  
  
 Se o método assumir parâmetros, o número de parâmetros na implementação [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deverá ser o mesmo daqueles usados na declaração [!INCLUDE[tsql](../../includes/tsql-md.md)] do procedimento armazenado.  
  
 Os parâmetros passados para um procedimento armazenado CLR podem ser de qualquer um dos tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativos que tenham um equivalente em código gerenciado. Para que a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] crie o procedimento, esses tipos devem ser especificados com o equivalente do tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo mais apropriado. Para obter mais informações sobre conversões de tipo, consulte [Mapeando dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela  
 Os TVPs (parâmetros com valor de tabela), ou seja, tipos de tabela definidos pelo usuário transmitidos para um procedimento ou uma função, oferecem uma maneira eficiente de passar várias linhas de dados para o servidor. Os TVPs proporcionam funcionalidade semelhante para matrizes de parâmetro, porém com maior flexibilidade e integração com [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles também fornecem o potencial para melhor desempenho. Os TVPs também ajudam a reduzir o número de viagens de ida e volta para o servidor. Em vez de enviar várias solicitações ao servidor, como com uma lista de parâmetros escalares, os dados podem ser enviados ao servidor como um TVP. Um tipo de tabela definido pelo usuário não pode ser passado como um parâmetro com valor de tabela para, ou ser retornado de, um procedimento armazenado ou uma função gerenciada(o) que é executada(o) no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre TVPs, consulte [usar parâmetros &#40;mecanismo de banco de dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="returning-results-from-clr-stored-procedures"></a>Retornando resultados de procedimentos armazenados CLR  
 As informações podem ser retornadas dos procedimentos armazenados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] de várias maneiras. Isso inclui parâmetros de saída, resultados tabulares e mensagens.  
  
### <a name="output-parameters-and-clr-stored-procedures"></a>Parâmetros OUTPUT e procedimentos armazenados CLR  
 Assim como nos procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)], as informações podem ser retornadas dos procedimentos armazenados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que usam parâmetros OUTPUT. A sintaxe de DML [!INCLUDE[tsql](../../includes/tsql-md.md)] usada para criar procedimentos armazenados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] é a mesma usada para criar procedimentos armazenados escritos em [!INCLUDE[tsql](../../includes/tsql-md.md)]. O parâmetro correspondente no código de implementação da classe do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve usar um parâmetro de passagem-por-referência como argumento. Observe que o Visual Basic não suporta parâmetros de saída da mesma maneira que o Visual C#. Você deve especificar o parâmetro por referência e aplicar o \<out () > atributo para representar um parâmetro de saída, da seguinte maneira:  
  
```  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub PriceSum ( <Out()> ByRef value As SqlInt32)  
```  
  
 A seguir está um procedimento armazenado que retorna informações por um parâmetro OUTPUT:  
  
 C#  
  
```  
using System;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void PriceSum(out SqlInt32 value)  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         value = 0;  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT Price FROM Products", connection);  
         SqlDataReader reader = command.ExecuteReader();  
  
         using (reader)  
         {  
            while( reader.Read() )  
            {  
               value += reader.GetSqlInt32(0);  
            }  
         }           
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Runtime.InteropServices  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Executes a query and iterates over the results to perform a summation.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
  
        Using connection As New SqlConnection("context connection=true")  
           value = 0  
           Connection.Open()  
           Dim command As New SqlCommand("SELECT Price FROM Products", connection)  
           Dim reader As SqlDataReader  
           reader = command.ExecuteReader()  
  
           Using reader  
              While reader.Read()  
                 value += reader.GetSqlInt32(0)  
              End While  
           End Using  
        End Using          
    End Sub  
End Class  
```  
  
 Depois que o assembly que contém o CLR acima armazenados procedimento foi compilado e criado no servidor, o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] é usado para criar o procedimento no banco de dados e especifica *soma* como um parâmetro de saída.  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
-- if StoredProcedures class was inside a namespace, called MyNS,  
-- you would use:  
-- AS EXTERNAL NAME TestStoredProc.[MyNS.StoredProcedures].PriceSum  
```  
  
 Observe que *soma* é declarado como um `int` tipo de dados do SQL Server e que o *valor* definido no procedimento armazenado CLR do parâmetro é especificado como um `SqlInt32` tipo de dados CLR. Quando um programa de chamada de procedimento armazenado CLR, é executada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte automaticamente o `SqlInt32` tipo de dados CLR a um `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  Para obter mais informações sobre qual CLR, tipos de dados podem e não podem ser convertidos, consulte [Mapeando dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
### <a name="returning-tabular-results-and-messages"></a>Retornando resultados tabulares e mensagens  
 O retorno dos resultados tabulares e mensagens para o cliente é executado através do objeto `SqlPipe`, que é obtido usando a propriedade `Pipe` da classe `SqlContext`. O objeto `SqlPipe` tem um método `Send`. Chamando o método `Send`, você pode transmitir dados pelo pipe para o aplicativo de chamada.  
  
 Há várias sobrecargas do método `SqlPipe.Send`, incluindo uma que envia um `SqlDataReader` e outra que simplesmente envia uma cadeia de caracteres de texto.  
  
###### <a name="returning-messages"></a>Retornando mensagens  
 Use `SqlPipe.Send(string)` para enviar mensagens para o aplicativo cliente. O texto da mensagem é limitado a 8000 caracteres. Se a mensagem ultrapassar os 8000 caracteres, ela será truncada.  
  
###### <a name="returning-tabular-results"></a>Retornando resultados tabulares  
 Para enviar os resultados de uma consulta diretamente para o cliente, use uma das sobrecargas do método `Execute` no objeto `SqlPipe`. Essa é a maneira mais eficiente de retornar os resultados para o cliente, porque os dados são transferidos para os buffers de rede sem ser copiados para a memória gerenciada. Por exemplo:  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the results to the client directly.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void ExecuteToClient()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version", connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub ExecuteToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 Para enviar os resultados de uma consulta que foi executada anteriormente através do provedor interno ao processo (ou pré-processar os dados usando uma implementação personalizada de `SqlDataReader`), use a sobrecarga do método `Send` que assume um `SqlDataReader`. Esse método é ligeiramente mais lento do que o método direto descrito anteriormente, mas oferece maior flexibilidade para manipular os dados antes de serem enviados para o cliente.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the resulting reader to the client  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendReaderToClient()  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("select @@version", connection);  
         SqlDataReader r = command.ExecuteReader();  
         SqlContext.Pipe.Send(r);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendReaderToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class  
```  
  
 Para criar um conjunto de resultados dinâmicos, preenchê-lo e enviá-lo para o cliente, você pode criar registros da conexão atual e enviá-los usando `SqlPipe.Send`.  
  
```csharp  
using System.Data;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
using System.Data.SqlTypes;  
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Create a result set on the fly and send it to the client.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendTransientResultSet()  
   {  
      // Create a record object that represents an individual row, including it's metadata.  
      SqlDataRecord record = new SqlDataRecord(new SqlMetaData("stringcol", SqlDbType.NVarChar, 128));  
  
      // Populate the record.  
      record.SetSqlString(0, "Hello World!");  
  
      // Send the record to the client.  
      SqlContext.Pipe.Send(record);  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendTransientResultSet()  
        ' Create a record object that represents an individual row, including it's metadata.  
        Dim record As New SqlDataRecord(New SqlMetaData("stringcol", SqlDbType.NVarChar, 128) )  
  
        ' Populate the record.  
        record.SetSqlString(0, "Hello World!")  
  
        ' Send the record to the client.  
        SqlContext.Pipe.Send(record)          
    End Sub  
End Class   
```  
  
 A seguir está um exemplo de envio de um resultado tabular e uma mensagem através de `SqlPipe`.  
  
```csharp  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void HelloWorld()  
   {  
      SqlContext.Pipe.Send("Hello world! It's now " + System.DateTime.Now.ToString()+"\n");  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT ProductNumber FROM ProductMaster", connection);  
         SqlDataReader reader = command.ExecuteReader();  
         SqlContext.Pipe.Send(reader);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub HelloWorld()  
        SqlContext.Pipe.Send("Hello world! It's now " & System.DateTime.Now.ToString() & "\n")  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT ProductNumber FROM ProductMaster", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class   
```  
  
 O primeiro `Send` envia uma mensagem para o cliente, enquanto o segundo envia um resultado tabular que usa `SqlDataReader`.  
  
 Observe que esses exemplos são meramente para fins ilustrativos. As funções CLR são mais apropriadas do que instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] simples para aplicativos com uso intenso de cálculos. Um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] quase equivalente ao exemplo anterior é:  
  
```  
CREATE PROCEDURE HelloWorld() AS  
BEGIN  
PRINT('Hello world!')  
SELECT ProductNumber FROM ProductMaster  
END;  
```  
  
> [!NOTE]  
>  Mensagens e conjuntos de resultados são recuperados de maneira diferente no aplicativo cliente. Por exemplo, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conjuntos de resultados aparecem na **resultados** exibição e as mensagens aparecem na **mensagens** painel.  
  
 Se o código Visual C# anterior for salvo em um arquivo MyFirstUdp.cs e compilado com:  
  
```  
csc /t:library /out:MyFirstUdp.dll MyFirstUdp.cs   
```  
  
 Ou então, se o código Visual Basic anterior for salvo em um arquivo MyFirstUdp.vb e compilado com:  
  
```  
vbc /t:library /out:MyFirstUdp.dll MyFirstUdp.vb   
```  
  
> [!NOTE]  
>  A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os objetos de banco de dados de Visual C++ (como os procedimentos armazenados) compilados com `/clr:pure` não são suportados para execução.  
  
 O assembly resultante pode ser registrado, e o ponto de entrada invocado, com o DDL a seguir:  
  
```  
CREATE ASSEMBLY MyFirstUdp FROM 'C:\Programming\MyFirstUdp.dll';  
CREATE PROCEDURE HelloWorld  
AS EXTERNAL NAME MyFirstUdp.StoredProcedures.HelloWorld;  
EXEC HelloWorld;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Gatilhos CLR](../../../2014/database-engine/dev-guide/clr-triggers.md)  
  
  
