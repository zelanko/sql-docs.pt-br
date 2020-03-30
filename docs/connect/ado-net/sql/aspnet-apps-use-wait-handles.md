---
title: Aplicativos ASP.NET usando identificadores de espera
description: Fornece um exemplo que demonstra como executar vários comandos simultâneos de uma página do ASP.NET, usando os identificadores de espera para gerenciar a operação na conclusão de todos os comandos.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 42d5c395526ff79e24243392bb3dbfa302c8a9e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897068"
---
# <a name="aspnet-applications-using-wait-handles"></a>Aplicativos ASP.NET usando identificadores de espera

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Os modelos de retorno de chamada e sondagem para lidar com operações assíncronas são úteis quando seu aplicativo está processando apenas uma operação assíncrona de cada vez. Os modelos Wait fornecem uma maneira mais flexível de processar várias operações assíncronas. Há dois modelos Wait, nomeados segundo os métodos <xref:System.Threading.WaitHandle> usados para implementá-los: o modelo Wait (Any) e o modelo Wait (All).  
  
Para usar um modelo Wait, você precisa usar a propriedade <xref:System.IAsyncResult.AsyncWaitHandle%2A> do objeto <xref:System.IAsyncResult> retornado pelos métodos <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> ou <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>. Os métodos <xref:System.Threading.WaitHandle.WaitAny%2A> e <xref:System.Threading.WaitHandle.WaitAll%2A> exigem que você envie os objetos <xref:System.Threading.WaitHandle> como um argumento, agrupados juntos em uma matriz.  
  
Ambos os métodos Wait monitoram as operações assíncronas, aguardando a conclusão. O método <xref:System.Threading.WaitHandle.WaitAny%2A> aguarda que uma das operações seja concluída ou atinja o próprio tempo limite. Quando souber que uma determinada operação está concluída, você poderá processar os resultados dela e depois continuar a aguardar que a próxima operação também seja concluída ou atinja o tempo limite. Antes de continuar, o método <xref:System.Threading.WaitHandle.WaitAll%2A> aguarda que todos os processos na matriz de instâncias de <xref:System.Threading.WaitHandle> sejam concluídos ou atinjam o tempo limite.  
  
O benefício dos modelos Wait é mais perceptível quando você precisa executar várias operações com duração considerável em servidores diferentes ou então quando o seu servidor é suficientemente poderoso para processar todas as consultas simultaneamente. Nos exemplos apresentados aqui, três consultas emulam processos longos adicionando comando WAITFOR de durações variáveis a consultas SELECT sem relevância.  
  
## <a name="example-wait-any-model"></a>Exemplo: Modelo Wait (Any)  
O exemplo a seguir ilustra o modelo Wait (Any). Depois que três processos assíncronos são iniciados, o método <xref:System.Threading.WaitHandle.WaitAny%2A> é chamado para aguardar a conclusão de qualquer um deles. À medida que cada processo é concluído, o método <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> é chamado e o objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> resultante é lido. Nesse ponto, um aplicativo do mundo real provavelmente usará o <xref:Microsoft.Data.SqlClient.SqlDataReader> para popular uma parte da página. Neste exemplo simples, a hora em que o processo foi concluído é adicionada a uma caixa de texto correspondente ao processo. Em conjunto, os horários nas caixas de texto ilustram o ponto: O código é executado cada vez que um processo é concluído.  
  
Para configurar este exemplo, crie um projeto de site do ASP.NET. Coloque um controle <xref:System.Web.UI.WebControls.Button> e quatro controles <xref:System.Web.UI.WebControls.TextBox> na página (aceitando o nome padrão de cada controle).  
  
Adicione o código a seguir à classe do formulário, modificando a cadeia de conexão conforme o necessário para o seu ambiente.  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
     //  To avoid storing the connection string in your code,              
     //  you can retrieve it from a configuration file.   
     //  If you have not included "Asynchronous Processing=true"   
     //  in the connection string, the command will not be able  
     //  to execute asynchronously.  
{  
     return "Data Source=(local);Integrated Security=SSPI;" +  
          "Initial Catalog=AdventureWorks;" +  
          "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
     //  In a real-world application, you might be connecting to   
     //   three different servers or databases. For the example,  
     //   we connect to only one.  
  
     SqlConnection connection1 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection2 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection3 =   
          new SqlConnection(GetConnectionString());  
     //  To keep the example simple, all three asynchronous   
     //  processes select a row from the same table. WAITFOR  
     //  commands are used to emulate long-running processes  
     //  that complete after different periods of time.  
  
     string commandText1 = "WAITFOR DELAY '0:0:01';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText2 = "WAITFOR DELAY '0:0:05';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText3 = "WAITFOR DELAY '0:0:10';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     try  
          //  For each process, open a connection and begin   
          //  execution. Use the IAsyncResult object returned by   
          //  BeginExecuteReader to add a WaitHandle for the   
          //  process to the array.  
     {  
          connection1.Open();  
          SqlCommand command1 =  
               new SqlCommand(commandText1, connection1);  
          IAsyncResult result1 = command1.BeginExecuteReader();  
          WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
  
          connection2.Open();  
          SqlCommand command2 =  
               new SqlCommand(commandText2, connection2);  
          IAsyncResult result2 = command2.BeginExecuteReader();  
          WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
  
          connection3.Open();  
          SqlCommand command3 =  
               new SqlCommand(commandText3, connection3);  
          IAsyncResult result3 = command3.BeginExecuteReader();  
          WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
          WaitHandle[] waitHandles = {  
               waitHandle1, waitHandle2, waitHandle3  
          };  
  
          int index;  
          for (int countWaits = 0; countWaits <= 2; countWaits++)  
          {  
               //  WaitAny waits for any of the processes to   
               //  complete. The return value is either the index   
               //  of the array element whose process just   
               //  completed, or the WaitTimeout value.  
  
               index = WaitHandle.WaitAny(waitHandles,   
                    60000, false);  
               //  This example doesn't actually do anything with   
               //  the data returned by the processes, but the   
               //  code opens readers for each just to demonstrate       
               //  the concept.  
               //  Instead of using the returned data to fill the   
               //  controls on the page, the example adds the time  
               //  the process was completed to the corresponding  
               //  text box.  
  
               switch (index)  
               {  
                    case 0:  
                         SqlDataReader reader1;  
                         reader1 =   
                              command1.EndExecuteReader(result1);  
                         if (reader1.Read())  
                         {  
                           TextBox1.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader1.Close();  
                         break;  
                    case 1:  
                         SqlDataReader reader2;  
                         reader2 =   
                              command2.EndExecuteReader(result2);  
                         if (reader2.Read())  
                         {  
                           TextBox2.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader2.Close();  
                         break;  
                    case 2:  
                         SqlDataReader reader3;  
                         reader3 =   
                              command3.EndExecuteReader(result3);  
                         if (reader3.Read())  
                         {  
                           TextBox3.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader3.Close();  
                         break;  
                    case WaitHandle.WaitTimeout:  
                         throw new Exception("Timeout");  
                         break;  
               }  
          }  
     }  
     catch (Exception ex)  
     {  
          TextBox4.Text = ex.ToString();  
     }  
     connection1.Close();  
     connection2.Close();  
     connection3.Close();  
}  
```  
  
## <a name="example-wait-all-model"></a>Exemplo: Modelo Wait (All)  
O exemplo a seguir ilustra o modelo Wait (All). Depois que três processos assíncronos são iniciados, o método <xref:System.Threading.WaitHandle.WaitAll%2A> é chamado para aguardar a conclusão dos processos ou que eles atinjam o próprio tempo limite.  
  
Assim como ocorre no exemplo do modelo Wait (Any), a hora em que o processo foi concluído é adicionada a uma caixa de texto correspondente ao processo. Novamente, os horários nas caixas de texto ilustram o ponto: O código após o método <xref:System.Threading.WaitHandle.WaitAny%2A> é executado somente após a conclusão de todos os processos.  
  
Para configurar este exemplo, crie um projeto de site do ASP.NET. Coloque um controle <xref:System.Web.UI.WebControls.Button> e quatro controles <xref:System.Web.UI.WebControls.TextBox> na página (aceitando o nome padrão de cada controle).  
  
Adicione o código a seguir à classe do formulário, modificando a cadeia de conexão conforme o necessário para o seu ambiente.  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
    //  To avoid storing the connection string in your code,              
    //  you can retrieve it from a configuration file.   
    //  If you have not included "Asynchronous Processing=true"   
    //  in the connection string, the command will not be able  
    //  to execute asynchronously.  
{  
    return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks;" +  
        "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
    //  In a real-world application, you might be connecting to   
    //   three different servers or databases. For the example,  
    //   we connect to only one.  
  
    SqlConnection connection1 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection2 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection3 =   
        new SqlConnection(GetConnectionString());  
    //  To keep the example simple, all three asynchronous   
    //  processes execute UPDATE queries that result in  
      //  no change to the data. WAITFOR  
    //  commands are used to emulate long-running processes  
    //  that complete after different periods of time.  
  
    string commandText1 =   
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint + 1 " +  
        "WHERE ReorderPoint Is Not Null;" +  
        "WAITFOR DELAY '0:0:01';" +  
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint - 1 " +  
        "WHERE ReorderPoint Is Not Null";  
  
    string commandText2 =   
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint + 1 " +  
      "WHERE ReorderPoint Is Not Null;" +  
      "WAITFOR DELAY '0:0:05';" +  
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint - 1 " +  
      "WHERE ReorderPoint Is Not Null";  
  
    string commandText3 =  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint + 1 " +  
       "WHERE ReorderPoint Is Not Null;" +  
       "WAITFOR DELAY '0:0:10';" +  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint - 1 " +  
       "WHERE ReorderPoint Is Not Null";  
    try  
        //  For each process, open a connection and begin   
        //  execution. Use the IAsyncResult object returned by   
        //  BeginExecuteReader to add a WaitHandle for the   
        //  process to the array.  
    {  
        connection1.Open();  
        SqlCommand command1 =  
            new SqlCommand(commandText1, connection1);  
        IAsyncResult result1 = command1.BeginExecuteNonQuery();  
        WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
        connection2.Open();  
  
        SqlCommand command2 =  
            new SqlCommand(commandText2, connection2);  
        IAsyncResult result2 = command2.BeginExecuteNonQuery();  
        WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
        connection3.Open();  
  
        SqlCommand command3 =  
            new SqlCommand(commandText3, connection3);  
        IAsyncResult result3 = command3.BeginExecuteNonQuery();  
        WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
        WaitHandle[] waitHandles = {  
            waitHandle1, waitHandle2, waitHandle3  
        };  
  
        bool result;  
        //  WaitAll waits for all of the processes to   
        //  complete. The return value is True if the processes  
        //  all completed successfully, False if any process  
        //  timed out.  
  
        result = WaitHandle.WaitAll(waitHandles, 60000, false);  
        if(result)  
        {  
            long rowCount1 =   
                command1.EndExecuteNonQuery(result1);  
            TextBox1.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
            long rowCount2 =   
                command2.EndExecuteNonQuery(result2);  
            TextBox2.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
  
            long rowCount3 =   
                command3.EndExecuteNonQuery(result3);  
            TextBox3.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
        }  
        else  
        {  
            throw new Exception("Timeout");  
        }  
    }  
  
    catch (Exception ex)  
    {  
        TextBox4.Text = ex.ToString();  
    }  
    connection1.Close();  
    connection2.Close();  
    connection3.Close();  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Operações assíncronas](asynchronous-operations.md)
