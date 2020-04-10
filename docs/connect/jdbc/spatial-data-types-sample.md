---
title: Exemplo de tipos de dados espaciais para o Driver MSSQL JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07f05ee878f1f818e7bf500d053ef5a306477d27
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909392"
---
# <a name="spatial-data-types-sample"></a>Exemplo de tipos de dados espaciais

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esse aplicativo de exemplo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como criar, inserir e recuperar tipos de dados espaciais (Geometry e Geography).
  
O arquivo de código desta amostra chama-se SpatialDataTypes.java e pode ser encontrado no seguinte local:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes  
```

## <a name="requirements"></a>Requisitos  

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo mssql-jdbc.jar. Para obter mais informações sobre como definir o caminho de classe, confira [Como usar o JDBC Driver](../../connect/jdbc/using-the-jdbc-driver.md).  

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para saber mais sobre qual arquivo JAR escolher, confira os [requisitos do sistema para o JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo cria uma tabela chamada SpatialDataTypesTable_JDBC_Sample que contém as colunas 'Geometry' e 'Geography'.

Primeiro o exemplo cria objetos 'Geometry' e 'Geography' de um WKT (Texto Bem Conhecido) que representa um PONTO. Ele usa um SQLServerPreparedStatement com uma consulta parametrizada para mapear os dados para cada coluna de maneira condizente.

Por fim, o exemplo insere os dados na tabela e os recupera. Os dados são exibidos na forma de WKT.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import com.microsoft.sqlserver.jdbc.Geography;
import com.microsoft.sqlserver.jdbc.Geometry;
import com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement;
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class SpatialDataTypes {

    private static String tableName = "SpatialDataTypesTable_JDBC_Sample";

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";
        // Establish the connection.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            dropAndCreateTable(stmt);

            // TODO: Implement Sample code
            String geoWKT = "POINT(3 40 5 6)";
            Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
            Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);

            try (SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) con
                    .prepareStatement("insert into " + tableName + " values (?, ?)");) {
                pstmt.setGeometry(1, geomWKT);
                pstmt.setGeography(2, geogWKT);
                pstmt.execute();

                SQLServerResultSet rs = (SQLServerResultSet) stmt.executeQuery("select * from " + tableName);
                rs.next();

                System.out.println("Geometry data: " + rs.getGeometry(1));
                System.out.println("Geography data: " + rs.getGeography(2));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void dropAndCreateTable(Statement stmt) throws SQLException {
        stmt.executeUpdate("if object_id('" + tableName + "','U') is not null" + " drop table " + tableName);

        stmt.executeUpdate("Create table " + tableName + " (c1 geometry, c2 geography)");
    }
}
```

## <a name="see-also"></a>Confira também  

[Trabalhar com tipos de dados JDBC](../../connect/jdbc/working-with-data-types-jdbc.md)  
  
