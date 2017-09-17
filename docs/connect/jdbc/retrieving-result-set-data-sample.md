---
title: Exemplo de dados do conjunto de recuperar resultados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a2399dd259a9b06e2410c88c07991feb400b9080
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-result-set-data-sample"></a>Exemplo de recuperação de dados do conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como recuperar um conjunto de dados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de banco de dados e, em seguida, exibir os dados.  
  
 O arquivo de código deste exemplo chama-se retrieveRS.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Você também precisará acessar o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece sqljdbc.jar e sqljdbc4.jar os arquivos de biblioteca de classes a serem usados dependendo das suas configurações preferidas do Java Runtime Environment (JRE). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Em seguida, usando uma instrução SQL com o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) do objeto, ele executa a instrução SQL e coloca os dados retornados em uma [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
 Em seguida, o código de exemplo chama o método displayRow personalizado para iterar pelas linhas de dados que estão contidas no conjunto de resultados e usa o [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) método para exibir alguns dos dados que ele contém.  
  
```java
import java.sql.*;  
  
public class retrieveRS {  
  
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
  
         // Create and execute an SQL statement that returns a  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Production.Product;";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
         displayRow("PRODUCTS", rs);  
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
  
   private static void displayRow(String title, ResultSet rs) {  
      try {  
         System.out.println(title);  
         while (rs.next()) {  
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)  
  
  
