---
title: Gatilhos CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- inserted tables
- database objects [CLR integration], triggers
- common language runtime [SQL Server], triggers
- updated columns
- building database objects [CLR integration], triggers
- triggers [CLR integration]
- deleted tables
- EventData property
- SqlTriggerContext class
- transactions [CLR integration]
ms.assetid: 302a4e4a-3172-42b6-9cc0-4a971ab49c1c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87d822e97a75bbd08375980fe6a6f0341d8f9c60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755251"
---
# <a name="clr-triggers"></a>Gatilhos CLR
  Por causa da integração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com CLR (Common Language Runtime) do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], você pode usar qualquer linguagem do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para criar gatilhos CLR. Esta seção contém informações específicas para gatilhos implementados com a integração CLR. Para obter uma discussão completa sobre gatilhos, consulte [gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
## <a name="what-are-triggers"></a>O que são gatilhos?  
 Um gatilho é um tipo especial de procedimento armazenado executado automaticamente quando um evento de linguagem é executado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui dois tipos gerais de gatilhos: DML (linguagem de manipulação de dados) e DDL (linguagem de definição de dados). Os gatilhos do tipo DML podem ser usados quando as instruções `INSERT`, `UPDATE`ou `DELETE` modificarem dados em uma tabela especificada ou exibição. Já os gatilhos DDL acionam procedimentos armazenados em resposta a uma variedade de instruções DDL que são instruções iniciadas, principalmente, com `CREATE`, `ALTER`e `DROP`. Os gatilhos DDL podem ser usados para tarefas administrativas, como operações de auditoria e regulamentação de banco de dados.  
  
## <a name="unique-capabilities-of-clr-triggers"></a>Recursos exclusivos de gatilhos CLR  
 Os gatilhos gravados em [!INCLUDE[tsql](../../includes/tsql-md.md)] têm a capacidade de determinar quais colunas da exibição ou tabela acionada foram atualizadas com as funções `UPDATE(column)` e `COLUMNS_UPDATED()`.  
  
 Os gatilhos gravados em linguagem CLR diferem de outros objetos de integração CLR de várias maneiras. Os gatilhos CLR podem:  
  
-   Fazer referência a dados nas tabelas `INSERTED` e `DELETED`  
  
-   Determinar quais colunas foram modificadas como resultado de uma operação `UPDATE`  
  
-   Acessar informações sobre objetos de banco de dados afetados pela execução de instruções DDL.  
  
 Essas capacidades são fornecidas inerentemente na linguagem de consulta, ou pela classe `SqlTriggerContext`. Para obter informações sobre as vantagens da integração CLR e escolhendo entre o código gerenciado e [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [visão geral da integração CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="using-the-sqltriggercontext-class"></a>Usando a classe SqlTriggerContext  
 A classe `SqlTriggerContext` não pode ser criada publicamente e só pode ser obtida por meio do acesso à propriedade `SqlContext.TriggerContext` dentro do corpo de um gatilho CLR. A classe `SqlTriggerContext` pode ser obtida do `SqlContext` ativo chamando a propriedade `SqlContext.TriggerContext`:  
  
 `SqlTriggerContext myTriggerContext = SqlContext.TriggerContext;`  
  
 A classe `SqlTriggerContext` fornece informações de contexto sobre o gatilho. Essas informações contextuais incluem o tipo de ação que causou o acionamento do gatilho, quais colunas foram modificadas em uma operação UPDATE e, no caso de um gatilho DDL, uma estrutura XML `EventData` que descreve a operação de acionamento. Para obter mais informações, consulte [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql).  
  
### <a name="determining-the-trigger-action"></a>Determinando a ação do gatilho  
 Depois que você obtiver uma classe `SqlTriggerContext`, poderá usá-la para determinar o tipo de ação que acionou o gatilho. Essas informações estão disponíveis por meio da propriedade `TriggerAction` da classe `SqlTriggerContext`.  
  
 No caso dos gatilhos DML, a propriedade `TriggerAction` pode ter um dos seguintes valores:  
  
-   TriggerAction.Update (0x1)  
  
-   TriggerAction.Insert (0x2)  
  
-   TriggerAction.Delete(0x3)  
  
-   Para os gatilhos DDL, a lista de possíveis valores TriggerAction é consideravelmente mais longa. Consulte "TriggerAction Enumeration" no .NET Framework SDK para obter mais informações.  
  
### <a name="using-the-inserted-and-deleted-tables"></a>Usando as tabelas Inserted e Deleted  
 Duas tabelas especiais são usadas nas instruções de gatilho DML: a **inserido** tabela e o **excluído** tabela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria e gerencia automaticamente essas tabelas. Você pode usar essas tabelas temporárias para testar os efeitos de determinadas modificações de dados e definir condições para ações de gatilho DML; no entanto, você não pode alterar os dados diretamente nas tabelas.  
  
 Gatilhos CLR podem acessar o **inserido** e **excluído** tabelas por meio do provedor CLR em processo. Isso é feito obtendo-se um objeto `SqlCommand` do objeto SqlContext. Por exemplo:   
  
 C#  
  
```  
SqlConnection connection = new SqlConnection ("context connection = true");  
connection.Open();  
SqlCommand command = connection.CreateCommand();  
command.CommandText = "SELECT * from " + "inserted";  
```  
  
 Visual Basic  
  
```  
Dim connection As New SqlConnection("context connection=true")  
Dim command As SqlCommand  
connection.Open()  
command = connection.CreateCommand()  
command.CommandText = "SELECT * FROM " + "inserted"  
```  
  
### <a name="determining-updated-columns"></a>Determinando colunas atualizadas  
 Você pode determinar o número de colunas que foram modificadas por uma operação UPDATE usando a propriedade `ColumnCount` do objeto `SqlTriggerContext`. Você pode usar o método `IsUpdatedColumn` que considera o ordinal da coluna como um parâmetro de entrada, a fim de determinar se a coluna foi atualizada. Um valor `True` indica que a coluna foi atualizada.  
  
 Por exemplo, este snippet de código (do gatilho EmailAudit mais adiante neste tópico) lista todas as colunas atualizadas:  
  
 C#  
  
```  
reader = command.ExecuteReader();  
reader.Read();  
for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
{  
   pipe.Send("Updated column "  
      + reader.GetName(columnNumber) + "? "  
   + triggContext.IsUpdatedColumn(columnNumber).ToString());  
 }  
  
 reader.Close();  
```  
  
 Visual Basic  
  
```  
reader = command.ExecuteReader()  
reader.Read()  
Dim columnNumber As Integer  
  
For columnNumber=0 To triggContext.ColumnCount-1  
  
   pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
   "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
Next  
  
reader.Close()  
```  
  
### <a name="accessing-eventdata-for-clr-ddl-triggers"></a>Acessando EventData para gatilhos DDL CLR  
 Os gatilhos DDL, como os gatilhos regulares, disparam procedimentos armazenados em resposta a um evento. Mas, ao contrário dos gatilhos DML, não disparam em resposta a instruções UPDATE, INSERT ou DELETE em uma tabela ou exibição. Em vez disso, eles são acionados em resposta a uma variedade de instruções DDL que são instruções iniciadas, principalmente, com CREATE, ALTER e DROP. Os gatilhos DDL podem ser usados para tarefas administrativas, como operações de auditoria e monitoramento de operações de banco de dados e alterações de esquema.  
  
 Informações sobre um evento que aciona um gatilho DDL estão disponíveis na propriedade `EventData` da classe `SqlTriggerContext`. Essa propriedade contém um valor `xml`. O esquema xml inclui informações sobre:  
  
-   A hora do evento.  
  
-   O SPID (System Process ID) da conexão durante a qual o gatilho é executado.  
  
-   O tipo de evento que acionou o gatilho.  
  
 Assim, dependendo do tipo de evento, o esquema poderá conter ainda outras informações, como o banco de dados em que o evento ocorreu, o objeto em relação ao qual ele ocorreu e o comando [!INCLUDE[tsql](../../includes/tsql-md.md)] do evento.  
  
 No exemplo a seguir, o gatilho DDL retorna a propriedade bruta `EventData`.  
  
> [!NOTE]  
>  O envio de resultados e mensagens pelo objeto `SqlPipe` é mostrado aqui apenas para fins ilustrativos e, em geral, não é uma prática recomendada para o código de produção durante a programação de gatilhos CLR. Talvez dados inesperados sejam retornados, o que pode levar a erros de aplicativo.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   public static void DropTableTrigger()  
   {  
       SqlTriggerContext triggContext = SqlContext.TriggerContext;             
  
       switch(triggContext.TriggerAction)  
       {  
           case TriggerAction.DropTable:  
           SqlContext.Pipe.Send("Table dropped! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
  
           default:  
           SqlContext.Pipe.Send("Something happened! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
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
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    Public Shared Sub DropTableTrigger()  
        Dim triggContext As SqlTriggerContext  
        triggContext = SqlContext.TriggerContext  
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.DropTable  
              SqlContext.Pipe.Send("Table dropped! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
           Case Else  
              SqlContext.Pipe.Send("Something else happened! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
        End Select  
    End Sub  
End Class     
```  
  
 A seguinte saída de exemplo é o valor de propriedade `EventData` depois que um gatilho DDL foi acionado por um evento `CREATE TABLE`:  
  
 `<EVENT_INSTANCE><PostTime>2004-04-16T21:17:16.160</PostTime><SPID>58</SPID><EventType>CREATE_TABLE</EventType><ServerName>MACHINENAME</ServerName><LoginName>MYDOMAIN\myname</LoginName><UserName>MYDOMAIN\myname</UserName><DatabaseName>AdventureWorks</DatabaseName><SchemaName>dbo</SchemaName><ObjectName>UserName</ObjectName><ObjectType>TABLE</ObjectType><TSQLCommand><SetOptions ANSI_NULLS="ON" ANSI_NULL_DEFAULT="ON" ANSI_PADDING="ON" QUOTED_IDENTIFIER="ON" ENCRYPTED="FALSE" /><CommandText>create table dbo.UserName  
(  
 UserName varchar(50),  
 RealName varchar(50)  
)  
</CommandText></TSQLCommand></EVENT_INSTANCE>`  
  
 Além das informações acessíveis através da classe `SqlTriggerContext`, as consultas ainda podem fazer referência a `COLUMNS_UPDATED` e inserted/deleted dentro do texto de um comando executado em processo.  
  
## <a name="sample-clr-trigger"></a>Exemplo de gatilho CLR  
 Neste exemplo, considere o cenário no qual você permite que o usuário escolha o ID que desejar, mas você deseja saber quais usuários inseriram especificamente um endereço de email como ID. O gatilho a seguir detectaria essas informações e as registraria em uma tabela de auditoria.  
  
> [!NOTE]  
>  O envio de resultados e mensagens pelo objeto `SqlPipe` é mostrado aqui apenas para fins ilustrativos, não sendo, em geral, uma prática recomendada para o código de produção. Talvez dados inesperados sejam retornados, o que pode levar a erros de aplicativo  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   [SqlTrigger(Name = @"EmailAudit", Target = "[dbo].[Users]", Event = "FOR INSERT, UPDATE, DELETE")]  
   public static void EmailAudit()  
   {  
      string userName;  
      string realName;  
      SqlCommand command;  
      SqlTriggerContext triggContext = SqlContext.TriggerContext;  
      SqlPipe pipe = SqlContext.Pipe;  
      SqlDataReader reader;  
  
      switch (triggContext.TriggerAction)  
      {  
         case TriggerAction.Insert:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
            reader.Close();  
  
            if (IsValidEMailAddress(userName))  
            {  
               command = new SqlCommand(  
                  @"INSERT [dbo].[UserNameAudit] VALUES ('"  
                  + userName + @"', '" + realName + @"');",  
                  connection);  
               pipe.Send(command.CommandText);  
               command.ExecuteNonQuery();  
               pipe.Send("You inserted: " + userName);  
            }  
         }  
  
         break;  
  
         case TriggerAction.Update:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
  
            pipe.Send(@"You updated: '" + userName + @"' - '"  
               + realName + @"'");  
  
            for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
            {  
               pipe.Send("Updated column "  
                  + reader.GetName(columnNumber) + "? "  
                  + triggContext.IsUpdatedColumn(columnNumber).ToString());  
            }  
  
            reader.Close();  
         }  
  
         break;  
  
         case TriggerAction.Delete:  
            using (SqlConnection connection  
               = new SqlConnection(@"context connection=true"))  
               {  
                  connection.Open();  
                  command = new SqlCommand(@"SELECT * FROM DELETED;",  
                     connection);  
                  reader = command.ExecuteReader();  
  
                  if (reader.HasRows)  
                  {  
                     pipe.Send(@"You deleted the following rows:");  
                     while (reader.Read())  
                     {  
                        pipe.Send(@"'" + reader.GetString(0)  
                        + @"', '" + reader.GetString(1) + @"'");  
                     }  
  
                     reader.Close();  
  
                     //alternately, to just send a tabular resultset back:  
                     //pipe.ExecuteAndSend(command);  
                  }  
                  else  
                  {  
                     pipe.Send("No rows affected.");  
                  }  
               }  
  
               break;  
            }  
        }  
  
     public static bool IsValidEMailAddress(string email)  
     {  
         return Regex.IsMatch(email, @"^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$");  
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
Imports System.Text.RegularExpressions  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    <SqlTrigger(Name:="EmailAudit", Target:="[dbo].[Users]", Event:="FOR INSERT, UPDATE, DELETE")> _  
    Public Shared Sub EmailAudit()  
        Dim userName As String  
        Dim realName As String  
        Dim command As SqlCommand  
        Dim triggContext As SqlTriggerContext  
        Dim pipe As SqlPipe  
        Dim reader As SqlDataReader    
  
        triggContext = SqlContext.TriggerContext      
        pipe = SqlContext.Pipe    
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.Insert  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 reader.Close()  
  
                 If IsValidEmailAddress(userName) Then  
                     command = New SqlCommand("INSERT [dbo].[UserNameAudit] VALUES ('" & _  
                       userName & "', '" & realName & "');", connection)  
  
                    pipe.Send(command.CommandText)  
                    command.ExecuteNonQuery()  
                    pipe.Send("You inserted: " & userName)  
  
                 End If  
              End Using  
  
           Case TriggerAction.Update  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 pipe.Send("You updated: " & userName & " - " & realName)  
  
                 Dim columnNumber As Integer  
  
                 For columnNumber=0 To triggContext.ColumnCount-1  
  
                    pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
                      "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
                 Next  
  
                 reader.Close()  
              End Using  
  
           Case TriggerAction.Delete  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM DELETED;", connection)  
  
                 reader = command.ExecuteReader()  
  
                 If reader.HasRows Then  
                    pipe.Send("You deleted the following rows:")  
  
                    While reader.Read()  
  
                       pipe.Send( reader.GetString(0) & ", " & reader.GetString(1) )  
  
                    End While   
  
                    reader.Close()  
  
                    ' Alternately, just send a tabular resultset back:  
                    ' pipe.ExecuteAndSend(command)  
  
                 Else  
                   pipe.Send("No rows affected.")  
                 End If  
  
              End Using   
        End Select  
    End Sub  
  
    Public Shared Function IsValidEMailAddress(emailAddress As String) As Boolean  
  
       return Regex.IsMatch(emailAddress, "^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$")  
    End Function      
End Class  
```  
  
 Suponha que existam duas tabelas com as seguintes definições:  
  
```  
CREATE TABLE Users  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
);  
GO CREATE TABLE UserNameAudit  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
)  
```  
  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução que cria o gatilho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o seguinte e pressupõe que o assembly **SQLCLRTest** já está registrado no atual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
```  
CREATE TRIGGER EmailAudit  
ON Users  
FOR INSERT, UPDATE, DELETE  
AS  
EXTERNAL NAME SQLCLRTest.CLRTriggers.EmailAudit  
```  
  
## <a name="validating-and-canceling-invalid-transactions"></a>Validando e cancelando transações inválidas  
 O uso de gatilhos para validar e cancelar transações INSERT, UPDATE ou DELETE inválidas ou impedir alterações em seu esquema de banco de dados é comum. Para isso, incorpore a lógica de validação em seu gatilho e, em seguida, reverta a transação atual se a ação não corresponder aos critérios de validação.  
  
 Quando chamado em um gatilho, o método `Transaction.Rollback` ou um SqlCommand com o texto de comando "TRANSACTION ROLLBACK" lança uma exceção com uma mensagem de erro ambígua e deve ser encapsulado em um bloco try/catch. A mensagem de erro exibida é semelhante à seguinte:  
  
```  
Msg 6549, Level 16, State 1, Procedure trig_InsertValidator, Line 0  
A .NET Framework error occurred during execution of user defined routine or aggregate 'trig_InsertValidator':   
System.Data.SqlClient.SqlException: Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting... User transaction, if any, will be rolled back.  
```  
  
 Essa exceção é esperada e o bloco try/catch é necessário para que a execução do código continue. Quando o código de gatilho termina a execução, outra exceção é gerada  
  
```  
Msg 3991, Level 16, State 1, Procedure trig_InsertValidator, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate "trig_InsertValidator" has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting.  
The statement has been terminated.  
```  
  
 Essa exceção também é esperada, sendo necessário um bloco try/catch ao redor da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que executa a ação que aciona o gatilho para que a execução possa continuar. Apesar das duas exceções lançadas, a transação é revertida e as alterações não são confirmadas na tabela. A principal diferença entre gatilhos CLR e gatilhos [!INCLUDE[tsql](../../includes/tsql-md.md)] é que os gatilhos [!INCLUDE[tsql](../../includes/tsql-md.md)] podem continuar a operar depois que a transação é revertida.  
  
### <a name="example"></a>Exemplo  
 O gatilho a seguir executa uma validação simples de instruções INSERT em uma tabela. Se o valor inteiro inserido for igual a um, a transação será revertida e o valor não será inserido na tabela. Todos os outros valores inteiros são inseridos na tabela. Observe o bloco try/catch ao redor do método `Transaction.Rollback`. O script [!INCLUDE[tsql](../../includes/tsql-md.md)] cria uma tabela de teste, um assembly e um procedimento armazenado gerenciado. Observe que as duas instruções INSERT são encapsuladas em um bloco try/catch de forma que a exceção lançada quando a execução do gatilho termina é capturada.  
  
 C#  
  
```  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class Triggers  
{  
    // Enter existing table or view for the target and uncomment the attribute line  
    // [Microsoft.SqlServer.Server.SqlTrigger (Name="trig_InsertValidator", Target="Table1", Event="FOR INSERT")]  
    public static void trig_InsertValidator()  
    {  
        using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
        {  
            SqlCommand command;  
            SqlDataReader reader;  
            int value;  
  
            // Open the connection.  
            connection.Open();  
  
            // Get the inserted value.  
            command = new SqlCommand(@"SELECT * FROM INSERTED", connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            value = (int)reader[0];  
            reader.Close();  
  
            // Rollback the transaction if a value of 1 was inserted.  
            if (1 == value)  
            {  
                try  
                {  
                    // Get the current transaction and roll it back.  
                    Transaction trans = Transaction.Current;  
                    trans.Rollback();                      
                }  
                catch (SqlException ex)  
                {  
                    // Catch the expected exception.                      
                }  
            }  
            else  
            {  
                // Perform other actions here.  
            }  
  
            // Close the connection.  
            connection.Close();              
        }  
    }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class Triggers  
' Enter existing table or view for the target and uncomment the attribute line  
' <Microsoft.SqlServer.Server.SqlTrigger(Name:="trig_InsertValidator", Target:="Table1", Event:="FOR INSERT")> _  
Public Shared Sub  trig_InsertValidator ()  
    Using connection As New SqlConnection("context connection=true")  
  
        Dim command As SqlCommand  
        Dim reader As SqlDataReader  
        Dim value As Integer  
  
        ' Open the connection.  
        connection.Open()  
  
        ' Get the inserted value.  
        command = New SqlCommand("SELECT * FROM INSERTED", connection)  
        reader = command.ExecuteReader()  
        reader.Read()  
        value = CType(reader(0), Integer)  
        reader.Close()  
  
        ' Rollback the transaction if a value of 1 was inserted.  
        If value = 1 Then  
  
            Try  
                ' Get the current transaction and roll it back.  
                Dim trans As Transaction  
                trans = Transaction.Current  
                trans.Rollback()  
  
            Catch ex As SqlException  
  
                ' Catch the exception.                      
            End Try  
        Else  
  
            ' Perform other actions here.  
        End If  
  
        ' Close the connection.  
        connection.Close()  
    End Using  
End Sub  
End Class  
```  
  
 Transact-SQL  
  
```  
-- Create the test table, assembly, and trigger.  
CREATE TABLE Table1(c1 int);  
go  
  
CREATE ASSEMBLY ValidationTriggers from 'E:\programming\ ValidationTriggers.dll';  
go  
  
CREATE TRIGGER trig_InsertValidator  
ON Table1  
FOR INSERT  
AS EXTERNAL NAME ValidationTriggers.Triggers.trig_InsertValidator;  
go  
  
-- Use a Try/Catch block to catch the expected exception  
BEGIN TRY  
   INSERT INTO Table1 VALUES(42)  
   INSERT INTO Table1 VALUES(1)  
END TRY  
BEGIN CATCH  
  SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
END CATCH;  
  
-- Clean up.  
DROP TRIGGER trig_InsertValidator;  
DROP ASSEMBLY ValidationTriggers;  
DROP TABLE Table1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md)   
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [Criando objetos de banco de dados com o Common Language Runtime &#40;CLR&#41; integração](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
