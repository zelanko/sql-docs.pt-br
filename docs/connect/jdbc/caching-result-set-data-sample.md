---
title: Exemplo de dados do conjunto de resultados em cache | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 226256514187740e7254407d5581cb2d59f5c714
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="caching-result-set-data-sample"></a>Exemplo de armazenamento de dados do conjunto de resultados em cache
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como recuperar um grande conjunto de dados de um banco de dados e, em seguida, controlar o número de linhas de dados que são armazenados em cache no cliente usando o [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método o [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
> [!NOTE]  
>  Limitar o número de linhas armazenadas em cache no cliente é diferente de limitar o número total de linhas que um conjunto de resultados pode conter. Para controlar o número total de linhas que estão contidos em um conjunto de resultados, use o [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) método do [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto, que é herdado por ambos os [ SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) objetos.  
  
 Para definir um limite no número de linhas armazenadas em cache no cliente, você primeiro deve usar um cursor do lado do servidor quando você cria um dos objetos de instrução declarando especificamente o tipo de cursor a ser usado ao criar o objeto de instrução. Por exemplo, o driver JDBC fornece o tipo de cursor TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, que é um somente avanço, somente leitura cursor do lado do servidor para uso com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados.  
  
> [!NOTE]  
>  Uma alternativa ao uso de tipo de cursor específico do SQL Server é usar a propriedade de cadeia de conexão selectMethod, definindo seu valor como "cursor". Para obter mais informações sobre os tipos de cursor com suporte pelo driver JDBC, consulte [Noções básicas sobre tipos de Cursor](../../connect/jdbc/understanding-cursor-types.md).  
  
 Depois de executar a consulta contida no objeto de instrução e os dados são retornados ao cliente como resultado conjunto, você pode chamar o método setFetchSize para controlar a quantidade de dados é recuperado do banco de dados ao mesmo tempo. Por exemplo, se você tiver uma tabela com 100 linhas de dados e definir o tamanho da busca como 10, apenas 10 linhas de dados serão armazenadas em cache no cliente em qualquer momento determinado. Embora esse procedimento reduza a velocidade de processamento dos dados, ele tem a vantagem de usar menos memória no cliente, o que pode ser especialmente útil quando for necessário processar grandes quantidades de dados.  
  
 O arquivo de código desse exemplo chama-se cacheRS.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Também será necessário o acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar e sqljdbc4.jar a serem usados, dependendo das configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Em seguida, ele usa uma instrução SQL com o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto, especifica o tipo de cursor do lado do servidor e, em seguida, executa a instrução SQL e coloca os dados retornados em um objeto SQLServerResultSet.  
  
 Em seguida, o código de exemplo chama o método de timerTest personalizado, passando como argumentos o tamanho da busca para uso e o conjunto de resultados. O método timerTest, em seguida, define o tamanho da busca do resultado definido usando o método setFetchSize, define a hora de início do teste e itera por meio do conjunto de resultados com um `While` loop. Assim que o `While` loop é finalizado, o código define a hora de parada do teste e, em seguida, exibe o resultado do teste, incluindo o tamanho da busca, o número de linhas processadas, e o tempo necessário para executar o teste.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
  
public class cacheRS {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
            "databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns a large  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Sales.SalesOrderDetail;";  
         stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, +  
               SQLServerResultSet.CONCUR_READ_ONLY);  
  
         // Perform a fetch for every row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1, rs);  
         rs.close();  
  
         // Perform a fetch for every tenth row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(10, rs);  
         rs.close();  
  
         // Perform a fetch for every 100th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(100, rs);  
         rs.close();  
  
         // Perform a fetch for every 1000th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1000, rs);  
         rs.close();  
  
         // Perform a fetch for every 128th row (the default) in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(0, rs);  
         rs.close();  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
  
   private static void timerTest(int fetchSize, ResultSet rs) {  
      try {  
  
         // Declare the variables for tracking the row count and elapsed time.  
         int rowCount = 0;  
         long startTime = 0;  
         long stopTime = 0;  
         long runTime = 0;  
  
         // Set the fetch size then iterate through the result set to  
         // cache the data locally.  
         rs.setFetchSize(fetchSize);  
         startTime = System.currentTimeMillis();  
         while (rs.next()) {  
            rowCount++;  
         }  
         stopTime = System.currentTimeMillis();  
         runTime = stopTime - startTime;  
  
         // Display the results of the timer test.  
         System.out.println("FETCH SIZE: " + rs.getFetchSize());  
         System.out.println("ROWS PROCESSED: " + rowCount);  
         System.out.println("TIME TO EXECUTE: " + runTime);  
         System.out.println();  
  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)  
  
  
