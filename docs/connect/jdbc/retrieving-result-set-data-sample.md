---
title: Como recuperar o exemplo de dados do conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ac13eff3840434e67321aeb0e151e377d4b929f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027778"
---
# <a name="retrieving-result-set-data-sample"></a>Recuperando exemplo de dados do conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como recuperar um conjunto de dados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, exibi-los.

O arquivo de código desta amostra chama-se RetrieveResultSet.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo mssql-jdbc.jar. Também será necessário ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o caminho de classe, confira [Como usar o JDBC Driver](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para saber mais sobre qual arquivo JAR escolher, confira os [requisitos do sistema para o JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Em seguida, usando uma instrução SQL com o objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), ele executa a instrução SQL e coloca os dados retornados em um objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).

A seguir, o código de exemplo chama o método personalizado displayRow para iterar pelas linhas de dados do conjunto de resultados e usa o método [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) para exibir alguns dos dados.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class RetrieveResultSet {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            createTable(stmt);
            String SQL = "SELECT * FROM Production.Product;";
            ResultSet rs = stmt.executeQuery(SQL);
            displayRow("PRODUCTS", rs);
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
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));
        }
    }

    private static void createTable(Statement stmt) throws SQLException {
        stmt.execute("if exists (select * from sys.objects where name = 'Product_JDBC_Sample')"
                + "drop table Product_JDBC_Sample");

        String sql = "CREATE TABLE [Product_JDBC_Sample](" + "[ProductID] [int] IDENTITY(1,1) NOT NULL,"
                + "[Name] [varchar](30) NOT NULL," + "[ProductNumber] [nvarchar](25) NOT NULL,"
                + "[MakeFlag] [bit] NOT NULL," + "[FinishedGoodsFlag] [bit] NOT NULL," + "[Color] [nvarchar](15) NULL,"
                + "[SafetyStockLevel] [smallint] NOT NULL," + "[ReorderPoint] [smallint] NOT NULL,"
                + "[StandardCost] [money] NOT NULL," + "[ListPrice] [money] NOT NULL," + "[Size] [nvarchar](5) NULL,"
                + "[SizeUnitMeasureCode] [nchar](3) NULL," + "[WeightUnitMeasureCode] [nchar](3) NULL,"
                + "[Weight] [decimal](8, 2) NULL," + "[DaysToManufacture] [int] NOT NULL,"
                + "[ProductLine] [nchar](2) NULL," + "[Class] [nchar](2) NULL," + "[Style] [nchar](2) NULL,"
                + "[ProductSubcategoryID] [int] NULL," + "[ProductModelID] [int] NULL,"
                + "[SellStartDate] [datetime] NOT NULL," + "[SellEndDate] [datetime] NULL,"
                + "[DiscontinuedDate] [datetime] NULL," + "[rowguid] [uniqueidentifier] ROWGUIDCOL  NOT NULL,"
                + "[ModifiedDate] [datetime] NOT NULL,)";

        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('Adjustable Time','AR-5381','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('ML Bottom Bracket','BB-8107','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('Mountain-500 Black, 44','BK-M18B-44','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);
    }
}

```

## <a name="see-also"></a>Confira também

[Trabalhando com conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)
