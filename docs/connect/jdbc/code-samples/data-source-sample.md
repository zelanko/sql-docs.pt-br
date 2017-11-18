---
title: Exemplo de fonte de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9cda7cac56de964c97b2f60d416cbb83ff4e2b80
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-sample"></a>Exemplo de fonte de dados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como se conectar a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados usando um objeto de fonte de dados. Ele também demonstra como recuperar dados de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados usando um procedimento armazenado.  
  
 O arquivo de código desse exemplo chama-se connectDS.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\connections  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, será necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Você também precisará acessar o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece sqljdbc.jar e sqljdbc4.jar os arquivos de biblioteca de classes a serem usados dependendo das suas configurações preferidas do Java Runtime Environment (JRE). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo define várias propriedades de conexão usando métodos setter do [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto e, em seguida, chama o [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) método o O objeto SQLServerDataSource para retornar um [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
 Em seguida, o código de exemplo usa o [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método do objeto SQLServerConnection para criar um [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto e, em seguida, o [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) método é chamado para executar o procedimento armazenado.  
  
 Por fim, o exemplo usa o [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto retornado do método executeQuery para iterar pelos resultados retornados pelo procedimento armazenado.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class connectDS {  
  
   public static void main(String[] args) {  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      CallableStatement cstmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.   
         SQLServerDataSource ds = new SQLServerDataSource();  
         ds.setUser("UserName");  
         ds.setPassword("*****");  
         ds.setServerName("localhost");  
         ds.setPortNumber(1433);   
         ds.setDatabaseName("AdventureWorks");  
         con = ds.getConnection();  
  
         // Execute a stored procedure that returns some data.  
         cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");  
         cstmt.setInt(1, 50);  
         rs = cstmt.executeQuery();  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println("EMPLOYEE: " + rs.getString("LastName") +   
               ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER: " + rs.getString("ManagerLastName") +   
               ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (cstmt != null) try { cstmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
         System.exit(1);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conectando e recuperando dados](../../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  

