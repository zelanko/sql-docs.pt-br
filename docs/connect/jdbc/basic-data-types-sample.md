---
title: "Exemplo de tipos de dados básicos | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59ac80cf-fc66-4493-933d-38e479c5f54d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 424b1442a554cc2e4e52b0bf11c50c276d2a32cf
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="basic-data-types-sample"></a>Exemplo de tipos de dados básicos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como usar métodos de getter de conjunto de resultados para recuperar básico [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] valores e como usar métodos de atualização de conjunto de resultados para atualizar esses valores de tipo de dados.  
  
 O arquivo de código deste exemplo chama-se basicDT.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\datatypes  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, será necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Você também precisará acessar o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
 Você também deve criar os seguintes dados de exemplo e tabela no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo:  
  
```  
use AdventureWorks  
CREATE TABLE DataTypesTable   
   (Col1 int IDENTITY,   
    Col2 char,  
    Col3 varchar(50),   
    Col4 bit,  
    Col5 decimal(18, 2),  
    Col6 money,  
    Col7 datetime,  
    Col8 date,  
    Col9 time,  
    Col10 datetime2,  
    Col11 datetimeoffset  
    );  
  
INSERT INTO DataTypesTable   
VALUES ('A', 'Some text.', 0, 15.25, 10.00, '01/01/2006 23:59:59.991', '01/01/2006', '23:59:59', '01/01/2006 23:59:59.12345', '01/01/2006 23:59:59.12345 -1:00')  
```  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece sqljdbc.jar e sqljdbc4.jar os arquivos de biblioteca de classes a serem usados dependendo das suas configurações preferidas do Java Runtime Environment (JRE). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] de banco de dados e, em seguida, recupera uma única linha de dados de teste datatypestable. O método displayRow personalizado é chamado para exibir todos os dados contidos no conjunto de resultados usando vários get\<tipo > métodos do [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
 Em seguida, o exemplo usa vários atualização\<tipo > métodos do SQLServerResultSet de classe para atualizar os dados contidos no conjunto de resultados e, em seguida, chama o [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) método para manter esses dados de volta para o banco de dados.  
  
 Por fim, o exemplo atualiza os dados contidos no resultado definido e, em seguida, chama o método de displayRow personalizado novamente para exibir os dados contidos no resultado definido.  
  
```java
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
import microsoft.sql.DateTimeOffset;  
  
public class basicDT {  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns some data  
         // and display it.  
         String SQL = "SELECT * FROM DataTypesTable";  
         stmt = con.createStatement(ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);           
         rs.next();  
         displayRow("ORIGINAL DATA", rs);  
  
         // Update the data in the result set.  
         rs.updateString(2, "B");  
         rs.updateString(3, "Some updated text.");  
         rs.updateBoolean(4, true);  
         rs.updateDouble(5, 77.89);  
         rs.updateDouble(6, 1000.01);  
         long timeInMillis = System.currentTimeMillis();  
         Timestamp ts = new Timestamp(timeInMillis);  
         rs.updateTimestamp(7, ts);  
         rs.updateDate(8, new Date(timeInMillis));  
         rs.updateTime(9, new Time(timeInMillis));  
         rs.updateTimestamp(10, ts);  
  
         //-480 indicates GMT - 8:00 hrs  
         ((SQLServerResultSet)rs).updateDateTimeOffset(11, DateTimeOffset.valueOf(ts, -480));  
  
         rs.updateRow();  
  
         // Get the updated data from the database and display it.  
         rs = stmt.executeQuery(SQL);  
         rs.next();  
         displayRow("UPDATED DATA", rs);  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null)   
         try {   
         rs.close();   
         }   
         catch(Exception e) {}  
  
         if (stmt != null)   
         try { stmt.close();   
         }   
         catch(Exception e) {}  
  
         if (con != null)   
         try {   
         con.close();   
         }   
         catch(Exception e) {}  
      }  
   }  
  
   private static void displayRow(String title, ResultSet rs) {  
      try {  
         System.out.println(title);  
         System.out.println(rs.getInt(1) + " , " +  // SQL integer type.  
               rs.getString(2) + " , " +            // SQL char type.  
               rs.getString(3) + " , " +            // SQL varchar type.  
               rs.getBoolean(4) + " , " +           // SQL bit type.  
               rs.getDouble(5) + " , " +            // SQL decimal type.  
               rs.getDouble(6) + " , " +            // SQL money type.  
               rs.getTimestamp(7) + " , " +            // SQL datetime type.  
               rs.getDate(8) + " , " +              // SQL date type.  
               rs.getTime(9) + " , " +              // SQL time type.  
               rs.getTimestamp(10) + " , " +            // SQL datetime2 type.  
               ((SQLServerResultSet)rs).getDateTimeOffset(11)); // SQL datetimeoffset type.   
  
         System.out.println();  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com tipos de dados &#40; JDBC &#41;](../../connect/jdbc/working-with-data-types-jdbc.md)  
  
  
