---
title: 'Etapa 4: conectar-se de forma resiliente ao SQL com ADO.NET | Microsoft Docs'
description: Descreve como conectar o reciliently ao SQL
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: rothja
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 62ec2eb775ef5fba76b402d1871afe6c87bcc606
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451807"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Etapa 4: Conectar-se de forma resiliente ao SQL com ADO.NET

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Download ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- Artigo anterior:&nbsp;&nbsp;&nbsp;[Etapa 3: prova de conceito da conexão ao SQL usando ADO.NET](step-3-connect-sql-ado-net.md)  

  
Este tópico fornece um exemplo de código do C# que demonstra a lógica de repetição personalizada. A lógica de repetição fornece confiabilidade. A lógica de repetição é projetada para processar normalmente erros temporários ou *falhas transitórias* que tendem a desaparecer se o programa aguardar vários segundos e novas tentativas.  
  
As fontes de falhas transitórias incluem:  
  
- Uma breve falha da rede que dá suporte à Internet.  
- Um sistema de nuvem pode estar equilibrando a carga de seus recursos no momento em que a consulta foi enviada.  
  
  
As classes do ADO.NET para conexão ao Microsoft SQL Server local também podem se conectar ao Banco de Dados SQL do Azure. No entanto, por si só, as classes ADO.NET não podem fornecer toda a robustez e a confiabilidade necessárias no uso em produção. O programa cliente pode encontrar falhas transitórias das quais ele deve se recuperar de forma silenciosa e tranqüila e continuar por conta própria.  
  
## <a name="step-1-identify-transient-errors"></a>Etapa 1: identificar erros transitórios  
  
Seu programa deve distinguir entre erros transitórios versus erros persistentes. Erros transitórios são condições de erro que podem ser apagadas em um curto período de tempo, como problemas de rede transitórios.  Um exemplo de um erro persistente seria, se o seu programa tiver um erro de ortografia do nome do banco de dados de destino, nesse caso, o "nenhum banco de dados encontrado" persistiria e não terá chance de se limpar em um curto período de tempo.  
  
A lista de números de erro categorizados como falhas transitórias está disponível em [mensagens de erro para aplicativos cliente do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Etapa 2: criar e executar o aplicativo de exemplo  
  
Este exemplo pressupõe que .NET Framework 4.5.1 ou posterior esteja instalado.  O C# exemplo de código consiste em um arquivo chamado Program.cs. Seu código é fornecido na próxima seção.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Etapa 2. a: capturar e compilar o exemplo de código  
  
Você pode compilar o exemplo com as seguintes etapas:  
  
1. No [Visual Studio Community Edition gratuito](https://www.visualstudio.com/products/visual-studio-community-vs), crie um novo projeto do modelo de C# aplicativo de console.  
    - Arquivo > Novo > projeto > instalado > modelos > Visual C# > Windows > área de trabalho clássica > aplicativo de console  
    - Nomeie o projeto **RetryAdo2**.  
2. Abra o painel de Gerenciador de Soluções.  
    - Consulte o nome do seu projeto.  
    - Consulte o nome do arquivo Program.cs.  
3. Abra o arquivo Program.cs.  
4. Substitua totalmente o conteúdo do arquivo Program.cs pelo código no bloco de código a seguir.  
5. Clique no menu Compilar > Compilar solução.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Etapa 2. b: copiar e colar código de exemplo  
  
Cole esse código em seu arquivo **Program.cs** .  
  
Em seguida, você deve editar as cadeias de caracteres para nome do servidor, senha e assim por diante. Você pode encontrar essas cadeias de caracteres no método chamado **GetSqlConnectionStringBuilder**.  
  
Observação: a cadeia de conexão para o nome do servidor é voltada para o banco de dados SQL do Azure, pois inclui o prefixo de quatro caracteres do **TCP:** . Mas você pode ajustar a cadeia de caracteres do servidor para se conectar ao seu Microsoft SQL Server.  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
using TD = System.Threading;  
    
namespace RetryAdo2  
{  
  public class Program  
  {  
    static public int Main(string[] args)  
    {  
      bool succeeded = false;  
      int totalNumberOfTimesToTry = 4;  
      int retryIntervalSeconds = 10;  
    
      for (int tries = 1;  
        tries <= totalNumberOfTimesToTry;  
        tries++)  
      {  
        try  
        {  
          if (tries > 1)  
          {  
            Console.WriteLine  
              ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
              tries, totalNumberOfTimesToTry  
              );  
            TD.Thread.Sleep(1000 * retryIntervalSeconds);  
            retryIntervalSeconds = Convert.ToInt32  
              (retryIntervalSeconds * 1.5);  
          }  
          AccessDatabase();  
          succeeded = true;  
          break;  
        }  
    
        catch (QC.SqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (TestSqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (Exception Exc)  
        {  
          Console.WriteLine(Exc);  
          succeeded = false;  
          break;  
        }  
      }  
    
      if (succeeded == true)  
      {  
        return 0;  
      }  
      else  
      {  
        Console.WriteLine("ERROR: Unable to access the database!");  
        return 1;  
      }  
    }  
    
    /// <summary>  
    /// Connects to the database, reads,  
    /// prints results to the console.  
    /// </summary>  
    static public void AccessDatabase()  
    {  
      //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
    
      using (var sqlConnection = new QC.SqlConnection  
          (GetSqlConnectionString()))  
      {  
        using (var dbCommand = sqlConnection.CreateCommand())  
        {  
          dbCommand.CommandText = @"  
SELECT TOP 3  
    ob.name,  
    CAST(ob.object_id as nvarchar(32)) as [object_id]  
  FROM sys.objects as ob  
  WHERE ob.type='IT'  
  ORDER BY ob.name;";  
    
          sqlConnection.Open();  
          var dataReader = dbCommand.ExecuteReader();  
    
          while (dataReader.Read())  
          {  
            Console.WriteLine("{0}\t{1}",  
              dataReader.GetString(0),  
              dataReader.GetString(1));  
          }  
        }  
      }  
    }  
    
    /// <summary>  
    /// You must edit the four 'my' string values.  
    /// </summary>  
    /// <returns>An ADO.NET connection string.</returns>  
    static private string GetSqlConnectionString()  
    {  
      // Prepare the connection string to Azure SQL Database.  
      var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
    
      // Change these values to your values.  
      sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
      sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
    
      sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
      sqlConnectionSB.Password = "MyPassword";  
      sqlConnectionSB.IntegratedSecurity = false;  
    
      // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
      sqlConnectionSB.ConnectRetryCount = 3;  
      sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
    
      // Leave these values as they are.  
      sqlConnectionSB.IntegratedSecurity = false;  
      sqlConnectionSB.Encrypt = true;  
      sqlConnectionSB.ConnectTimeout = 30;  
    
      return sqlConnectionSB.ToString();  
    }  
    
    static public CG.List<int> TransientErrorNumbers =  
      new CG.List<int> { 4060, 40197, 40501, 40613,  
      49918, 49919, 49920, 11001 };  
  }  
    
  /// <summary>  
  /// For testing retry logic, you can have method  
  /// AccessDatabase start by throwing a new  
  /// TestSqlException with a Number that does  
  /// or does not match a transient error number  
  /// present in TransientErrorNumbers.  
  /// </summary>  
  internal class TestSqlException : ApplicationException  
  {  
    internal TestSqlException(int testErrorNumber)  
    { this.Number = testErrorNumber; }  
    
    internal int Number  
    { get; set; }  
  }  
}  
```  
  
###  <a name="step-2c-run-the-program"></a>Etapa 2. c: executar o programa  
  
  
O executável **RetryAdo2. exe** não insere parâmetros. Para executar o. exe:  
  
1. Abra uma janela do console na qual você compilou o binário RetryAdo2. exe.  
2. Execute RetryAdo2. exe, sem parâmetros de entrada.  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Etapa 3: maneiras de testar sua lógica de repetição  
  
Há várias maneiras pelas quais você pode simular um erro transitório para testar sua lógica de repetição.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Etapa 3. a: lançar uma exceção de teste  
  
O exemplo de código inclui:  
  
- Uma pequena segunda classe denominada **TestSqlException**, com uma propriedade chamada **Number**.  
- `//throw new TestSqlException(4060);`, que você pode remover o comentário.  
  
Se você remover o comentário da instrução throw e recompile, a próxima execução de **RetryAdo2. exe** produzirá algo semelhante ao seguinte.  
  
```  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>> RetryAdo2.exe  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 2 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 3 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 4 of 4 max...  
4060: transient occurred. (TESTING.)  
ERROR: Unable to access the database!  
  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Etapa 3. b: testar novamente com um erro persistente  
  
Para provar que o código manipula erros persistentes corretamente, execute novamente o teste anterior, exceto que não use o número de um erro transitório real como 4060. Em vez disso, use o número insentido de 7654321. O programa deve tratar isso como um erro persistente e deve ignorar qualquer repetição.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Etapa 3. c: desconectar da rede  
  
1. Desconecte o computador cliente da rede.  
    - Para um desktop, desconecte o cabo de rede.  
    - Para um laptop, pressione a função combinação de chaves para desligar o adaptador de rede.  
2. Inicie o RetryAdo2. exe e aguarde o console exibir o primeiro erro transitório, provavelmente 11001.  
3. Reconecte-se à rede, enquanto o RetryAdo2. exe continua a ser executado.  
4. Observe o êxito do relatório do console em uma nova tentativa subsequente.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Etapa 2. d: errar temporariamente o nome do servidor  
  
1. Adicione temporariamente 40615 como outro número de erro a **TransientErrorNumbers**e recompile.  
2. Defina um ponto de interrupção na linha: `new QC.SqlConnectionStringBuilder()`.  
3. Use o recurso *Editar e continuar* para errar intencionalmente o nome do servidor, algumas linhas abaixo.  
    - Deixe o programa ser executado e retorne ao ponto de interrupção.  
    - O erro 40615 ocorre.  
4. Corrija o erro de ortografia.  
5. Deixe o programa ser executado e concluído com êxito.  
6. Remova 40615 e recompile.  
  
## <a name="next-steps"></a>Próximas etapas  
  
Para explorar outros melhores practicies e diretrizes de design, visite [conectar-se ao banco de dados SQL: links, práticas recomendadas e diretrizes de design](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
