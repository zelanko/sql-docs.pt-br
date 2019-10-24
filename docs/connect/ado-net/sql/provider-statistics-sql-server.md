---
title: Estatísticas do provedor para SQL Server
description: Descreve o suporte para obter SQL Server estatísticas de tempo de execução.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 092cf63e62bce01e2a771ce4e5f7f46e1073e91a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452067"
---
# <a name="provider-statistics-for-sql-server"></a>Estatísticas do provedor para SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

A partir do .NET Framework versão 2,0 e do .NET Core versão 1,0, o Provedor de Dados do Microsoft SqlClient para SQL Server dá suporte a estatísticas de tempo de execução. Você deve habilitar as estatísticas definindo a propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlConnection> como `True` depois de ter um objeto de conexão válido criado. Depois que as estatísticas são habilitadas, você pode examiná-las como um "instantâneo no tempo" recuperando uma referência de <xref:System.Collections.IDictionary> por meio do método <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlConnection>. Você enumera por meio da lista como um conjunto de entradas de dicionário de pares de nome/valor. Esses pares de nome/valor não são ordenados. A qualquer momento, você pode chamar o método <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlConnection> para redefinir os contadores. Se a coleta de estatísticas não tiver sido habilitada, uma exceção não será gerada. Além disso, se <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> for chamado sem <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> ter sido chamado primeiro, os valores recuperados serão os valores iniciais para cada entrada. Se você habilitar estatísticas, executar seu aplicativo por um tempo e, em seguida, desabilitar estatísticas, os valores recuperados refletirão os valores coletados até o ponto em que as estatísticas foram desabilitadas. Todos os valores estatísticos coletados estão em uma base por conexão.  
  
## <a name="statistical-values-available"></a>Valores estatísticos disponíveis  
Atualmente, há 18 itens diferentes disponíveis no provedor de Microsoft SQL Server. O número de itens disponíveis pode ser acessado por meio da propriedade **Count** da referência da interface <xref:System.Collections.IDictionary> retornada pelo <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>. Todos os contadores para estatísticas do provedor usam o tipo de common language runtime <xref:System.Int64> (**long** no C# e no Visual Basic), que tem 64 bits de largura. O valor máximo do tipo de dados **int64**, conforme definido pelo campo **int64.MaxValue**, é ((2^63)-1)). Quando os valores para os contadores atingem esse valor máximo, eles não devem mais ser considerados precisos. Isso significa que **int64.MaxValue**-1((2^63)-2) é efetivamente o maior valor válido para qualquer estatística.  
  
> [!NOTE]
>  Um dicionário é usado para retornar estatísticas do provedor porque o número, os nomes e a ordem das estatísticas retornadas podem ser alterados no futuro. Os aplicativos não devem depender de um valor específico encontrado no dicionário, mas devem verificar se o valor está lá e ramificar de acordo.  
  
A tabela a seguir descreve os valores estatísticos atuais disponíveis. Observe que os nomes de chave para os valores individuais não são localizados entre as versões regionais do Microsoft .NET Framework e do .NET Core.  
  
|Nome da Chave|Descrição|  
|--------------|-----------------|  
|`BuffersReceived`|Retorna o número de pacotes TDS recebidos pelo provedor de SQL Server depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`BuffersSent`|Retorna o número de pacotes TDS enviados a SQL Server pelo provedor após as estatísticas terem sido habilitadas. Comandos grandes podem exigir vários buffers. Por exemplo, se um comando grande for enviado para o servidor e ele exigir seis pacotes, `ServerRoundtrips` será incrementado em um e `BuffersSent` será incrementado em seis.|  
|`BytesReceived`|Retorna o número de bytes de dados nos pacotes TDS recebidos pelo provedor de SQL Server depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`BytesSent`|Retorna o número de bytes de dados enviados a SQL Server em pacotes TDS depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`ConnectionTime`|A quantidade de tempo (em milissegundos) que a conexão foi aberta após a habilitação das estatísticas (tempo total de conexão se as estatísticas tiverem sido habilitadas antes de abrir a conexão).|  
|`CursorOpens`|Retorna o número de vezes que um cursor foi aberto por meio da conexão depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.<br /><br /> Observe que os resultados somente leitura/somente encaminhamento retornados por instruções SELECT não são considerados cursores e, portanto, não afetam esse contador.|  
|`ExecutionTime`|Retorna a quantidade cumulativa de tempo (em milissegundos) que o provedor gastou processando depois que as estatísticas tiverem sido habilitadas, incluindo o tempo gasto aguardando respostas do servidor, bem como o tempo gasto na execução do código no próprio provedor.<br /><br /> As classes que incluem o código de tempo são:<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> Para manter os membros críticos ao desempenho o menor possível, os seguintes membros não são cronometrados:<br /><br /> SqlDataReader<br /><br /> Este operador [] (todas as sobrecargas)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|Retorna o número total de instruções de inserção, exclusão e atualização executadas por meio da conexão depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`IduRows`|Retorna o número total de linhas afetadas por instruções de inserção, exclusão e atualização executadas por meio da conexão depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`NetworkServerTime`|Retorna a quantidade cumulativa de tempo (em milissegundos) que o provedor gastou esperando por respostas do servidor depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`PreparedExecs`|Retorna o número de comandos preparados executados por meio da conexão depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`Prepares`|Retorna o número de instruções preparadas por meio da conexão quando o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
|`SelectCount`|Retorna o número de instruções SELECT executadas por meio da conexão depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas. Isso inclui instruções FETCH para recuperar linhas de cursores e a contagem de instruções SELECT é atualizada quando o final de um <xref:Microsoft.Data.SqlClient.SqlDataReader> é atingido.|  
|`SelectRows`|Retorna o número de linhas selecionado depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas. Esse contador reflete todas as linhas geradas pelas instruções SQL, mesmo aquelas que não foram realmente consumidas pelo chamador. Por exemplo, fechar um leitor de dados antes de ler o conjunto de resultados inteiro não afetaria a contagem. Isso inclui as linhas recuperadas de cursores por meio de instruções FETCH.|  
|`ServerRoundtrips`|Retorna o número de vezes que a conexão enviou comandos para o servidor e recebeu uma resposta depois que o aplicativo for iniciado usando o provedor e tiver habilitado estatísticas.|  
|`SumResultSets`|Retorna o número de conjuntos de resultados que foram usados depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas. Por exemplo, isso inclui qualquer conjunto de resultados retornado ao cliente. Para cursores, cada operação de busca ou de busca de bloco é considerada um conjunto de resultados independente.|  
|`Transactions`|Retorna o número de transações de usuário iniciadas depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas, incluindo reversões. Se uma conexão estiver sendo executada com a confirmação automática ativada, cada comando será considerado uma transação.<br /><br /> Esse contador incrementa a contagem de transações assim que uma instrução BEGIN TRAN é executada, independentemente de a transação ser confirmada ou revertida mais tarde.|  
|`UnpreparedExecs`|Retorna o número de instruções não preparadas executadas por meio da conexão depois que o aplicativo é iniciado usando o provedor e tem estatísticas habilitadas.|  
  
### <a name="retrieving-a-value"></a>Recuperando um valor  
O aplicativo de console a seguir mostra como habilitar estatísticas em uma conexão, recuperar quatro valores de estatística individuais e gravá-los na janela do console.  
  
> [!NOTE]
>  O exemplo a seguir usa o banco de dados de exemplo **AdventureWorks** incluído com o SQL Server. A cadeia de conexão fornecida no código de exemplo pressupõe que o banco de dados está instalado e disponível no computador local. Modifique a cadeia de conexão conforme necessário para o seu ambiente.  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>Recuperando todos os valores  
O aplicativo de console a seguir mostra como habilitar estatísticas em uma conexão, recuperar todos os valores de estatística disponíveis usando o enumerador e gravá-los na janela do console.  
  
> [!NOTE]
>  O exemplo a seguir usa o banco de dados de exemplo **AdventureWorks** incluído com o SQL Server. A cadeia de conexão fornecida no código de exemplo pressupõe que o banco de dados está instalado e disponível no computador local. Modifique a cadeia de conexão conforme necessário para o seu ambiente.  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
