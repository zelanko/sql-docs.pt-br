---
title: Resultado de modificação do conjunto de dados de exemplo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b2f8566607ec119aaa61a29468c7fca6388b5e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32831937"
---
# <a name="modifying-result-set-data-sample"></a>Exemplo de modificação de dados do conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como recuperar um conjunto de dados atualizável um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados. Em seguida, usando métodos do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) do objeto, que insere, modifica e finalmente exclui uma linha de dados do conjunto de dados.  
  
 O arquivo de código desse exemplo chama-se updateRS.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Também será necessário o acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar e sqljdbc4.jar a serem usados, dependendo das configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Em seguida, usando uma instrução SQL com o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) do objeto, ele executa a instrução SQL e coloca os dados retornados em um objeto SQLServerResultSet atualizável.  
  
 Em seguida, o código de exemplo usa o [moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) método para mover o conjunto de resultados cursor para a linha de inserção, usa uma série de [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) métodos para inserir dados na nova linha e, em seguida, chama o [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) método para manter a nova linha de dados no banco de dados.  
  
 Depois de inserir a nova linha de dados, o código de exemplo usa uma instrução SQL para recuperar a linha previamente inserida e, em seguida, usa a combinação de updateString e [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) métodos para atualizar a linha de dados e novamente persisti-los de volta para o banco de dados.  
  
 Finalmente, o código de exemplo recupera a linha previamente atualizada dos dados e, em seguida, exclui o banco de dados usando o [deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) método.  
  
```java
import java.sql.*;  
  
public class updateRS {  
  
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
  
         // Create and execute an SQL statement, retrieving an updateable result set.  
         String SQL = "SELECT * FROM HumanResources.Department;";  
         stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);  
  
         // Insert a row of data.  
         rs.moveToInsertRow();  
         rs.updateString("Name", "Accounting");  
         rs.updateString("GroupName", "Executive General and Administration");  
         rs.updateString("ModifiedDate", "08/01/2006");  
         rs.insertRow();  
  
         // Retrieve the inserted row of data and display it.  
         SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";  
         rs = stmt.executeQuery(SQL);  
         displayRow("ADDED ROW", rs);  
  
         // Update the row of data.  
         rs.first();  
         rs.updateString("GroupName", "Finance");  
         rs.updateRow();  
  
         // Retrieve the updated row of data and display it.  
         rs = stmt.executeQuery(SQL);  
         displayRow("UPDATED ROW", rs);  
  
         // Delete the row of data.  
         rs.first();  
         rs.deleteRow();  
         System.out.println("ROW DELETED");  
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
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));  
            System.out.println();  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com conjuntos de resultados](../../../connect/jdbc/working-with-result-sets.md)  
  
  
