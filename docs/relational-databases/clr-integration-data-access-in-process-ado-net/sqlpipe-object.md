---
title: Objeto SqlPipe | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eeeb65173b29ab5e0e441789d1c0033a2a59b369
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlpipe-object"></a>Objeto SqlPipe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], era muito comum gravar um procedimento armazenado (ou um procedimento armazenado estendido) para enviar resultados ou parâmetros de saída ao cliente que fez a chamada.  
  
 Em um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , qualquer instrução **SELECT** que retorna zero ou mais linhas envia os resultados ao "pipe" do chamador conectado.  
  
 No caso dos objetos de banco de dados CLR (common language runtime) executados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível enviar resultados ao pipe conectado usando os métodos **Send** do objeto **SqlPipe** . Acesse a propriedade **Pipe** do objeto **SqlContext** para obter o objeto **SqlPipe** . A classe **SqlPipe** é conceitualmente semelhante à classe **Response** localizada no ASP.NET. Para obter mais informações, consulte a documentação de referência da classe SqlPipe no .NET Framework SDK (Software Development Kit).  
  
## <a name="returning-tabular-results-and-messages"></a>Retornando resultados tabulares e mensagens  
 A **SqlPipe** tem um método **Send** com três sobrecargas. São eles:  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 O método **Send** envia dados diretamente ao cliente ou chamador. Em geral, é o cliente que consome a saída de **SqlPipe**, mas no caso de procedimentos armazenados aninhados CLR, o consumidor de saída também pode ser um procedimento armazenado. Por exemplo, Procedure1 chama SqlCommand.ExecuteReader () com o texto de comando "EXEC Procedure2". Procedure2 também é um procedimento armazenado gerenciado. Se Procedure2 chamar SqlPipe.Send (SqlDataRecord) agora, a linha será enviada ao leitor de Procedure1, não ao cliente.  
  
 A classe **Send** envia uma mensagem de cadeia de caracteres que aparece no cliente como uma mensagem de informações, equivalente a PRINT em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ele também pode enviar um conjunto de resultados de uma única linha usando **SqlDataRecord**ou um conjunto de resultados de várias linhas usando **SqlDataReader**.  
  
 O objeto **SqlPipe** também tem um método **ExecuteAndSend** . Esse método pode ser usado para executar um comando (transmitido como um objeto **SqlCommand** ) e enviar resultados diretamente ao chamador. Em caso de erros no comando enviado, as exceções são enviadas ao pipe, mas uma cópia também é enviada ao código gerenciado que efetuou a chamada. Se o código que efetuou a chamada não retornar a exceção, ele propagará a pilha no código [!INCLUDE[tsql](../../includes/tsql-md.md)] e aparecerá duas vezes na saída. Caso o código que efetuou a chamada retorne a exceção, o consumidor de pipe ainda verá o erro, mas não haverá erro duplicado.  
  
 Ele só pode obter um **SqlCommand** que esteja associado à conexão de contexto; ele não pode retornar um comando associado à conexão sem-contexto.  
  
## <a name="returning-custom-result-sets"></a>Retornando conjuntos de resultados personalizados  
 Os procedimentos armazenados gerenciados podem enviar conjuntos de resultados que não vêm de um **SqlDataReader**. O método **SendResultsStart** , junto com **SendResultsRow** e **SendResultsEnd**, permite procedimentos armazenados para enviar conjuntos de resultados personalizados ao cliente.  
  
 **SendResultsStart** usa um **SqlDataRecord** como uma entrada. Ele marca o começo de um conjunto de resultados e usa os metadados de registro para criar os metadados que descrevem o conjunto de resultados. Ele não envia o valor do registro com **SendResultsStart**. Todas as linhas subsequentes, enviadas com **SendResultsRow**, devem corresponder àquela definição de metadados.  
  
> [!NOTE]  
>  Depois de chamar o método **SendResultsStart** apenas **SendResultsRow** e **SendResultsEnd** podem ser chamados. Chamar qualquer outro método na mesma instância de **SqlPipe** resulta em um **InvalidOperationException**. **SendResultsEnd** define **SqlPipe** de volta ao estado original no qual outros métodos podem ser chamados.  
  
### <a name="example"></a>Exemplo  
 O procedimento armazenado **uspGetProductLine** retorna o nome, o número do produto, a cor e o preço de tabela de todos os produtos de uma linha de produtos específica. Esse procedimento armazenado aceita correspondências exatas para *prodLine*.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir executa o procedimento **uspGetProduct** que retorna uma lista de produtos de bicicleta.  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto SqlDataRecord](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [Procedimentos armazenados CLR](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Extensões específicas em processo do SQL Server para o ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
