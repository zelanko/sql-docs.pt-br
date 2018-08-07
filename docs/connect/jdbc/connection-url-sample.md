---
title: Exemplo de URL de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8150ae02c014d7460be10845e38d3e13be133d3
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452550"
---
# <a name="connection-url-sample"></a>Exemplo de URL de conexão

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando uma URL de conexão. Também demonstra como recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando uma instrução SQL.

O arquivo de código desta amostra chama-se ConnectURL.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo mssql-jdbc.jar. Também será necessário ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo define várias propriedades de conexão na URL de conexão e, em seguida, chama o método getConnection da classe DriverManager para retornar um objeto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Em seguida, o código de exemplo usa o método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) do objeto SQLServerConnection para criar um objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) e, depois, o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) é chamado para executar a instrução SQL.

Por fim, a amostra usa o objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) retornado do método executeQuery para iterar pelos resultados retornados pela instrução SQL.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectURL {
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT TOP 10 * FROM Person.Contact";
            ResultSet rs = stmt.executeQuery(SQL);

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println(rs.getString("FirstName") + " " + rs.getString("LastName"));
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>Consulte Também

[Conectando e recuperando dados](../../connect/jdbc/connecting-and-retrieving-data.md)
