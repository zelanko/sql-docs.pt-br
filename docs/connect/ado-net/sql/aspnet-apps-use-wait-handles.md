---
title: Aplicativos ASP.NET usando identificadores de espera
description: Fornece um exemplo que demonstra como executar vários comandos simultâneos de uma página do ASP.NET, usando identificadores de espera para gerenciar a operação na conclusão de todos os comandos.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: f7d242410b5f7aadd74494bb33a7572afe23be54
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452329"
---
# <a name="aspnet-applications-using-wait-handles"></a>Aplicativos ASP.NET usando identificadores de espera

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Os modelos de retorno de chamada e sondagem para lidar com operações assíncronas são úteis quando seu aplicativo está processando apenas uma operação assíncrona de cada vez. Os modelos de espera fornecem uma maneira mais flexível de processar várias operações assíncronas. Há dois modelos de espera, nomeados para os métodos de <xref:System.Threading.WaitHandle> usados para implementá-los: o modelo de espera (qualquer) e o modelo de espera (todos).  
  
Para usar um modelo de espera, você precisa usar a propriedade <xref:System.IAsyncResult.AsyncWaitHandle%2A> do objeto <xref:System.IAsyncResult> retornado pelos métodos <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> ou <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>. Os métodos <xref:System.Threading.WaitHandle.WaitAny%2A> e <xref:System.Threading.WaitHandle.WaitAll%2A> exigem que você envie os objetos <xref:System.Threading.WaitHandle> como um argumento, agrupados juntos em uma matriz.  
  
Ambos os métodos de espera monitoram as operações assíncronas, aguardando a conclusão. O método <xref:System.Threading.WaitHandle.WaitAny%2A> aguarda que qualquer uma das operações seja concluída ou atingiu o tempo limite. Quando você souber que uma operação específica foi concluída, poderá processar seus resultados e continuar aguardando a conclusão da próxima operação ou o tempo limite. O método <xref:System.Threading.WaitHandle.WaitAll%2A> aguarda que todos os processos na matriz de instâncias de <xref:System.Threading.WaitHandle> sejam concluídos ou expiram antes de continuar.  
  
O benefício dos modelos de espera é mais surpreendente quando você precisa executar várias operações de algum comprimento em servidores diferentes, ou quando o servidor é eficiente o suficiente para processar todas as consultas ao mesmo tempo. Nos exemplos apresentados aqui, três consultas emulam processos longos adicionando comandos WAITFOR de comprimentos variados a consultas SELECT irrelevante.  
  
## <a name="example-wait-any-model"></a>Exemplo: modelo de espera (qualquer)  
O exemplo a seguir ilustra o modelo de espera (qualquer). Depois que três processos assíncronos são iniciados, o método <xref:System.Threading.WaitHandle.WaitAny%2A> é chamado para aguardar a conclusão de qualquer um deles. À medida que cada processo é concluído, o método <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> é chamado e o objeto de <xref:Microsoft.Data.SqlClient.SqlDataReader> resultante é lido. Neste ponto, um aplicativo do mundo real provavelmente usará o <xref:Microsoft.Data.SqlClient.SqlDataReader> para popular uma parte da página. Neste exemplo simples, a hora em que o processo foi concluído é adicionada a uma caixa de texto correspondente ao processo. Em conjunto, os horários nas caixas de texto ilustram o ponto: o código é executado cada vez que um processo é concluído.  
  
Para configurar este exemplo, crie um novo projeto de site do ASP.NET. Coloque um controle de <xref:System.Web.UI.WebControls.Button> e quatro controles de <xref:System.Web.UI.WebControls.TextBox> na página (aceitando o nome padrão de cada controle).  
  
Adicione o código a seguir à classe do formulário, modificando a cadeia de conexão conforme necessário para o seu ambiente.  
  
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
  
## <a name="example-wait-all-model"></a>Exemplo: modelo de espera (todos)  
O exemplo a seguir ilustra o modelo de espera (todos). Depois que três processos assíncronos são iniciados, o método <xref:System.Threading.WaitHandle.WaitAll%2A> é chamado para aguardar a conclusão dos processos ou o tempo limite.  
  
Como o exemplo do modelo de espera (qualquer), a hora em que o processo foi concluído é adicionada a uma caixa de texto correspondente ao processo. Novamente, os horários nas caixas de texto ilustram o ponto: o código após o método <xref:System.Threading.WaitHandle.WaitAny%2A> é executado somente após a conclusão de todos os processos.  
  
Para configurar este exemplo, crie um novo projeto de site do ASP.NET. Coloque um controle de <xref:System.Web.UI.WebControls.Button> e quatro controles de <xref:System.Web.UI.WebControls.TextBox> na página (aceitando o nome padrão de cada controle).  
  
Adicione o código a seguir à classe do formulário, modificando a cadeia de conexão conforme necessário para o seu ambiente.  
  
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
