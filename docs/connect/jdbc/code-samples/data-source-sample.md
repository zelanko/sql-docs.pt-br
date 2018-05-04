---
title: Exemplo de fonte de dados | Microsoft Docs
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
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f900b1b91bb3d9114c4f7da2e4450da45fd9ec21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-sample"></a>Exemplo de fonte de dados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] demonstra como se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando um objeto de fonte de dados. Ele também demonstra como recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando um procedimento armazenado.  
  
 O arquivo de código desse exemplo chama-se connectDS.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\connections  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, será necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Também será necessário o acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar e sqljdbc4.jar a serem usados, dependendo das configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo define várias propriedades de conexão usando métodos setter do objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) e, em seguida, chama o método [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) do objeto SQLServerDataSource para retornar um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
 Em seguida, o código de exemplo usa o método [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) do objeto SQLServerConnection para criar um objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) e, então, o método [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) é chamado para executar o procedimento armazenado.  
  
 Por fim, o exemplo usa o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) retornado do método executeQuery para iterar pelos resultados retornados pelo procedimento armazenado.  
  
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
  
  
