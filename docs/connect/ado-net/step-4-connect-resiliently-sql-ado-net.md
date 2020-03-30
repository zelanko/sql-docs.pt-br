---
title: 'Etapa 4: Conectar-se de maneira resiliente ao SQL com ADO.NET | Microsoft Docs'
description: Descreve como conectar-se de maneira resiliente ao SQL
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e0a042c6c5e937c08e5bcc6402caa8338f22b332
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78895833"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Etapa 4: Conectar-se de forma resiliente ao SQL com ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

- Artigo anterior:&nbsp;&nbsp;&nbsp;[Etapa 3: Prova de conceito da conexão ao SQL usando o ADO.NET](step-3-connect-sql-ado-net.md)  

  
Este tópico fornece um exemplo de código do C# que demonstra a lógica de repetição personalizada. A lógica de repetição fornece confiabilidade. A lógica de repetição foi criada para processar normalmente erros transitórios ou *falhas transitórias* que tendem a desaparecer caso o programa aguarde vários segundos e tente novamente.  
  
As fontes de falhas transitórias incluem:  
  
- Uma breve falha da rede que dá suporte à Internet.  
- Um sistema de nuvem pode estar realizando balanceamento de carga dos próprios recursos no momento em que a consulta é enviada.  
  
  
As classes do ADO.NET para conexão ao Microsoft SQL Server local também podem se conectar ao Banco de Dados SQL do Azure. No entanto, por si só, as classes ADO.NET não podem fornecer toda a solidez e confiabilidade necessárias para o uso na produção. O programa cliente pode encontrar falhas transitórias das quais ele deve se recuperar silenciosamente e continuar por conta própria.  
  
## <a name="step-1-identify-transient-errors"></a>Etapa 1: Identificar erros transitórios  
  
O programa deve distinguir entre erros transitórios versus erros persistentes. Erros transitórios são condições de erro que podem desaparecer em um período curto de tempo, como problemas de rede transitórios.  Um exemplo de um erro persistente seria se o programa tivesse um erro de ortografia no nome do banco de dados de destino, nesse caso, o erro "Nenhum banco de dados encontrado" persistiria e não haveria chance de que esse erro desaparecesse em um período curto de tempo.  
  
A lista com os números dos erros que são categorizados como falhas transitórias está disponível em [Mensagens de erro para aplicativos cliente do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Etapa 2: Criar e executar o aplicativo de exemplo  
  
Este exemplo pressupõe que o .NET Framework 4.5.1 ou posterior esteja instalado.  O exemplo de código em C# consiste em um arquivo chamado Program.cs. Seu código é fornecido na próxima seção.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Etapa 2.a: Capturar e compilar o exemplo de código  
  
Você pode compilar o exemplo com as seguintes etapas:  
  
1. Na [edição gratuita do Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs), crie um novo projeto no modelo de Aplicativo do Console do C#.  
    - Arquivo > Novo > Projeto > Instalado > Modelos > Visual C# > Windows > Área de Trabalho Clássica > Aplicativo de Console  
    - Nomeie o projeto como **RetryAdo2**.  
2. Abra o painel do Gerenciador de Soluções.  
    - Veja o nome do seu projeto.  
    - Veja o nome do arquivo Program.cs.  
3. Abra o arquivo Program.cs.  
4. Substitua por completo o conteúdo do arquivo Program.cs pelo código no bloco de código a seguir.  
5. Clique no menu Compilar > Compilar Solução.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Etapa 2.b: Copiar e colar código de exemplo  
  
Cole este código em seu arquivo **Program.cs** .  
  
Em seguida, você deve editar as cadeias de caracteres de nome do servidor, senha e assim por diante. Você pode encontrar essas cadeias de caracteres no método chamado **GetSqlConnectionStringBuilder**.  
  
OBSERVAÇÃO:  A cadeia de conexão para o nome do servidor é voltada para o Banco de Dados SQL do Azure, pois inclui o prefixo de quatro caracteres de **tcp:** . Mas você pode ajustar a cadeia de caracteres do servidor para se conectar ao seu Microsoft SQL Server.  
  
  
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
  
###  <a name="step-2c-run-the-program"></a>Etapa 2.c: Execute o programa  
  
  
O executável **RetryAdo2.exe** não insere nenhum parâmetro. Para executar o .exe:  
  
1. Abra uma janela de console para onde você tiver compilado o binário RetryAdo2.exe.  
2. Execute o RetryAdo2.exe, sem nenhum parâmetro de entrada.  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Etapa 3: Maneiras de testar sua lógica de repetição  
  
Há diversas maneiras que você pode simular um erro transitório para testar sua lógica de repetição.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Etapa 3.a: Gerar uma exceção de teste  
  
O exemplo de código inclui:  
  
- Uma segunda classe pequena chamada **TestSqlException**, com uma propriedade chamada **Number**.  
- `//throw new TestSqlException(4060);` , do qual você pode remover a marca de comentário.  
  
Se você remover a marca de comentário da instrução throw e recompilar, a próxima execução de **RetryAdo2.exe** gerará algo semelhante ao mostrado a seguir.  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Etapa 3.b: Teste novamente com um erro persistente  
  
Para provar que o código lida com erros persistentes corretamente, execute novamente o teste anterior, mas não use o número de um erro transitório real como 4060. Em vez disso, use o número sem sentido 7654321. O programa deve tratar isso como um erro persistente e deve ignorar qualquer nova tentativa.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Etapa 3.c: Desconectar da rede  
  
1. Desconecte o computador cliente da rede.  
    - Para uma área de trabalho, desconecte o cabo de rede.  
    - Para um laptop, pressione a combinação de função das teclas para desativar o adaptador de rede.  
2. Inicie o RetryAdo2.exe e aguarde o console exibir o primeiro erro transitório, provavelmente 11001.  
3. Reconecte-se à rede, enquanto o RetryAdo2.exe continua em execução.  
4. Observe o console relatar o sucesso em uma nova tentativa subsequente.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Etapa 2.d: Temporariamente digitar incorretamente o nome do servidor  
  
1. Adicione temporariamente 40615 como outro número de erro para **TransientErrorNumbers**e recompile.  
2. Defina um ponto de interrupção na linha: `new QC.SqlConnectionStringBuilder()`.  
3. Use o recurso *Editar e Continuar* para propositalmente digitar o nome do servidor de maneira incorreta algumas linhas abaixo.  
    - Deixe o programa ser executado e voltar ao ponto de interrupção.  
    - O erro 40615 ocorre.  
4. Corrija o erro de ortografia.  
5. Deixe o programa ser executado e concluir com êxito.  
6. Remova o 40615 e recompile.  
  
## <a name="next-steps"></a>Próximas etapas  
  
Para explorar outras diretrizes de design e melhores práticas, visite [Como conectar-se ao Banco de Dados SQL: links, práticas recomendadas e diretrizes de design](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
