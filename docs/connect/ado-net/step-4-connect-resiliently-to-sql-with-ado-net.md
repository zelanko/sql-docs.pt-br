---
title: 'Etapa 4: Conectar atenda com flexibilidade ao SQL com ADO.NET | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0803a976c2b9e02918937d7e08a617ed73fe28d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288945"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Etapa 4: Conectar atenda com flexibilidade ao SQL com o ADO.NET

- Artigo anterior:&nbsp;&nbsp;&nbsp;[etapa 3: prova de conceito se conectar ao SQL usando o ADO.NET](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
Este tópico fornece um exemplo de código c# que demonstra a lógica de repetição personalizada. A lógica de repetição fornece confiabilidade. A lógica de repetição é projetada para processar normalmente erros temporários ou *falhas transitórias* que tendem a desaparecer se o programa esperar alguns segundos e tentar novamente.  
  
Fontes de falhas transitórias incluem:  
  
- Uma breve falha da rede que dá suporte à Internet.  
- Um sistema de nuvem pode ser o balanceamento de carga seus recursos no momento que você consulta enviado.  
  
  
As classes ADO.NET para conectar-se ao Microsoft SQL Server local também podem se conectar ao banco de dados do SQL Azure. No entanto, por si mesmos ADO.NET classes não podem fornecer todos os a robustez e a confiabilidade necessária em uso em produção. O programa cliente pode encontrar falhas transitórias, do qual ele deve silenciosamente recuperar e continuar por conta própria.  
  
## <a name="step-1-identify-transient-errors"></a>Etapa 1: Identificar erros transitórios  
  
O programa deve distinguir entre erros transitórios versus erros persistentes. Falhas transitórias de condições de erro que podem limpar em um curto período de tempo, como problemas de rede transitório.  Um exemplo de um erro persistente seria se o programa tiver um erro de ortografia do nome do banco de dados de destino, nesse caso, o erro "Banco de dados inexistente encontrado" persistir e sem chance de limpar em um curto período de tempo.  
  
A lista de números de erro que são categorizados como falhas transitórias está disponível em [mensagens de erro para aplicativos de cliente do banco de dados SQL](http://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Etapa 2: Criar e executar o aplicativo de exemplo  
  
Este exemplo supõe que .NET Framework 4.5.1 ou posterior está instalado.  O exemplo de código do c# consiste em um arquivo chamado Program.cs. Seu código é fornecido na próxima seção.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Etapa 2: capturar e compilar o exemplo de código  
  
Você pode compilar o exemplo com as seguintes etapas:  
  
1. No [Visual Studio Community edition gratuito](https://www.visualstudio.com/products/visual-studio-community-vs), criar um novo projeto de modelo de aplicativo de Console c#.  
    - Arquivo > Novo > projeto > instalado > Modelos > Visual C# > Windows > área de trabalho clássica > aplicativo de Console  
    - Nomeie o projeto **RetryAdo2**.  
2. Abra o painel do Gerenciador de soluções.  
    - Ver o nome do seu projeto.  
    - Ver o nome do arquivo Program.cs.  
3. Abra o arquivo Program.cs.  
4. Totalmente substitua o conteúdo do arquivo Program.cs pelo código no bloco de código a seguir.  
5. Clique no menu Build > Compilar solução.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Etapa 2.b: código de exemplo de copiar e colar  
  
Cole este código no seu **Program.cs** arquivo.  
  
Em seguida, você deve editar as cadeias de caracteres de nome do servidor, senha e assim por diante. Você pode encontrar essas cadeias de caracteres no método chamado **GetSqlConnectionStringBuilder**.  
  
Observação: A cadeia de caracteres de conexão para o nome do servidor é voltada para o banco de dados SQL Azure, porque ela inclui o prefixo de quatro caracteres do **tcp:**. Mas você pode ajustar a cadeia de caracteres do servidor para se conectar ao Microsoft SQL Server.  
  
  
```CSharp  
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
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
  
###  <a name="step-2c-run-the-program"></a>Etapa 2.c: executar o programa  
  
  
O **RetryAdo2.exe** executável entradas sem parâmetros. Para executar o .exe:  
  
1. Abra uma janela do console onde você ter compilado o binário RetryAdo2.exe.  
2. Execute RetryAdo2.exe, sem nenhum parâmetro de entrada.  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Etapa 3: Maneiras para testar sua lógica de repetição  
  
Há uma variedade de formas, você pode simular um erro transitório para testar sua lógica de repetição.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Etapa 3.a: gerar uma exceção de teste  
  
O exemplo de código inclui:  
  
- Uma pequena classe segundo denominada **TestSqlException**, que é uma propriedade chamada **número**.  
- `//throw new TestSqlException(4060);` , que você pode remover o comentário.  
  
Se você remover o comentário a instrução throw e recompile, a próxima execução do **RetryAdo2.exe** gera algo semelhante ao seguinte.  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Etapa 3.b: testar novamente com um erro persistente  
  
Para mostrar o código de identificadores de erros persistentes corretamente, execute novamente o teste anterior, exceto não usa o número de um erro transitório real como 4060. Em vez disso, use o número sem sentido 7654321. O programa deve tratar isso como um erro persistente e deve ignorar qualquer nova tentativa.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Etapa 3.c: desconectar da rede  
  
1. Desconecte o computador da rede.  
    - Para uma área de trabalho, desconecte o cabo de rede.  
    - Para um laptop, pressione a combinação de função de chaves para desativar o adaptador de rede.  
2. Iniciar RetryAdo2.exe e aguarde até que o console exibir o primeiro erro transitório, provavelmente 11001.  
3. Reconectar-se à rede, enquanto RetryAdo2.exe continua em execução.  
4. Assista o sucesso de relatório do console em uma nova tentativa subsequente.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Etapa 2.d: temporariamente errar o nome do servidor  
  
1. Adicione temporariamente 40615 como outro número de erro para **TransientErrorNumbers**e recompilar.  
2. Definir um ponto de interrupção na linha: `new QC.SqlConnectionStringBuilder()`.  
3. Use o *editar e continuar* recurso propositadamente errar o nome do servidor, duas linhas a seguir.  
    - Deixe o programa executar e volte para o ponto de interrupção.  
    - O erro 40615 ocorre.  
4. Corrija os erros de ortografia.  
5. Deixe o programa executar e concluir com êxito.  
6. Remover 40615 e recompilar.  
  
## <a name="next-steps"></a>Próximas etapas  
  
Para explorar outros practicies recomendadas e diretrizes de design, visite [se conectar ao banco de dados SQL: Links, práticas recomendadas e diretrizes de Design](http://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
