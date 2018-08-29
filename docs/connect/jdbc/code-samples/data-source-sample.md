---
title: Exemplo de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 166cc1aa7764a310d7cc6741afcd3e4dce3f2f62
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785220"
---
# <a name="data-source-sample"></a>Exemplo de fonte de dados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] demonstra como se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um objeto de fonte de dados. Ele também demonstra como recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um procedimento armazenado.

O arquivo de código desta amostra chama-se ConnectDataSource.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo mssql-jdbc.jar. Também será necessário ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo define várias propriedades de conexão usando métodos setter do objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) e, em seguida, chama o método [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) do objeto SQLServerDataSource para retornar um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).

Em seguida, o código de exemplo usa o método [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) do objeto SQLServerConnection para criar um objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) e, então, o método [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) é chamado para executar o procedimento armazenado.

Por fim, o exemplo usa o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) retornado do método executeQuery para iterar pelos resultados retornados pelo procedimento armazenado.

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class ConnectDataSource {

    public static void main(String[] args) {

        // Create datasource.
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setUser("<user>");
        ds.setPassword("<password>");
        ds.setServerName("<server>");
        ds.setPortNumber(Integer.parseInt("<port>"));
        ds.setDatabaseName("AdventureWorks");

        try (Connection con = ds.getConnection();
                CallableStatement cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");) {
            // Execute a stored procedure that returns some data.
            cstmt.setInt(1, 50);
            ResultSet rs = cstmt.executeQuery();

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println("EMPLOYEE: " + rs.getString("LastName") + ", " + rs.getString("FirstName"));
                System.out.println("MANAGER: " + rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));
                System.out.println();
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

[Conectando e recuperando dados](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)
