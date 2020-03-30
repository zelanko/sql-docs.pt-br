---
title: Como modificar exemplo de dados do conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 51e13941945a1be2d3ad1f02ce61fda98696f275
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027964"
---
# <a name="modifying-result-set-data-sample"></a>Modificando exemplo de dados de conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como recuperar um conjunto de dados atualizável de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em seguida, usando métodos do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), ele insere, modifica e, por fim, exclui uma linha de dados do conjunto de dados.

O arquivo de código desta amostra chama-se UpdateResultSet.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo mssql-jdbc.jar. Também será necessário ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o caminho de classe, confira [Como usar o JDBC Driver](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para saber mais sobre qual arquivo JAR escolher, confira os [requisitos do sistema para o JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Em seguida, usando uma instrução SQL com o objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), ele executa a instrução SQL e coloca os dados retornados em um objeto SQLServerResultSet atualizável.

Em seguida, o código de exemplo usa o método [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) para mover o cursor do conjunto de resultados para a linha de inserção, usa uma série de métodos [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) para inserir dados na nova linha e, depois, chama o método [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) para persistir a nova linha de dados novamente no banco de dados.

Depois de inserir a nova linha de dados, o código de exemplo usa uma instrução SQL para recuperar a linha previamente inserida e usa a combinação de métodos updateString e [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para atualizar a linha de dados e novamente persisti-la de volta no banco de dados.

Por fim, o código de exemplo recupera a linha de dados previamente atualizada e, em seguida, a exclui do banco de dados usando o método [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md).

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateResultSet {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);) {

            // Create and execute an SQL statement, retrieving an updateable result set.
            String SQL = "SELECT * FROM HumanResources.Department;";
            ResultSet rs = stmt.executeQuery(SQL);

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
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void displayRow(String title,
            ResultSet rs) throws SQLException {
        System.out.println(title);
        while (rs.next()) {
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));
            System.out.println();
        }
    }
}
```

## <a name="see-also"></a>Confira também

[Trabalhando com conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)
