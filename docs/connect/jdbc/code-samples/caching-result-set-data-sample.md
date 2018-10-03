---
title: Exemplo de dados de conjunto de resultados em cache | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ed4174dcd164163307259100e752d277f9b200c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823974"
---
# <a name="caching-result-set-data-sample"></a>Exemplo de armazenamento de dados do conjunto de resultados em cache

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] demonstra como recuperar um conjunto grande de dados de um banco de dados e, em seguida, controlar o número de linhas de dados armazenadas em cache no cliente, usando o método [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
> [!NOTE]  
> Limitar o número de linhas armazenadas em cache no cliente é diferente de limitar o número total de linhas que um conjunto de resultados pode conter. Para controlar o número total de linhas contidas em um conjunto de resultados, use o método [setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), herdado pelos objetos [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
Para definir um limite no número de linhas armazenadas em cache no cliente, primeiro use um cursor do lado do servidor ao criar um dos objetos Statement declarando especificamente o tipo de cursor a ser usado ao criar o objeto Statement. Por exemplo, o driver JDBC fornece o tipo de cursor TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, que é um cursor somente de avanço rápido, somente leitura, do lado do servidor, para uso com bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Uma alternativa ao uso de tipo de cursor específico do SQL Server é usar a propriedade de cadeia de conexão selectMethod, definindo seu valor como "cursor". Para obter mais informações sobre os tipos de cursor com suporte pelo driver JDBC, consulte [Noções básicas sobre tipos de Cursor](../../../connect/jdbc/understanding-cursor-types.md).  
  
Depois de executar a consulta no objeto Statement e os dados forem retornados ao cliente como um conjunto de resultados, você poderá chamar o método setFetchSize para controlar a quantidade de dados recuperados do banco de dados de uma só vez. Por exemplo, se você tiver uma tabela com 100 linhas de dados e definir o tamanho do fetch como 10, apenas 10 linhas de dados serão armazenadas em cache no cliente a qualquer momento. Embora esse procedimento reduza a velocidade de processamento dos dados, ele tem a vantagem de usar menos memória no cliente, o que pode ser especialmente útil quando for necessário processar grandes quantidades de dados.  
  
O arquivo de código desta amostra chama-se CacheResultSet.java e pode ser encontrado no seguinte local:  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets  
```

## <a name="requirements"></a>Requisitos  

Para executar este aplicativo de exemplo, é necessário definir o classpath para incluir o arquivo mssql-jdbc.jar. Também será necessário ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  

## <a name="example"></a>Exemplo  

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Em seguida, ele usa uma instrução SQL com o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), especifica o tipo de cursor do lado do servidor e, depois, executa a instrução SQL e coloca os dados retornados em um objeto SQLServerResultSet.  
  
A seguir, o código de exemplo chama o método timerTest personalizado, passando como argumentos o tamanho do fetch a ser usado e o conjunto de resultados. Em seguida, o método timerTest define o tamanho do fetch do conjunto de resultados usando o método setFetchSize, define a hora de início do teste e, depois, itera pelo conjunto de resultados com um loop `While`. Assim que o loop `While` é finalizado, o código define o tempo de parada do teste e, em seguida, exibe o resultado do teste, incluindo o tamanho do fetch, o número de linhas processadas e o tempo necessário para executar o teste.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class CacheResultSet {

    @SuppressWarnings("serial")
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, SQLServerResultSet.CONCUR_READ_ONLY);) {

            String SQL = "SELECT * FROM Sales.SalesOrderDetail;";

            for (int n : new ArrayList<Integer>() {
                {
                    add(1);
                    add(10);
                    add(100);
                    add(1000);
                    add(0);
                }
            }) {
                // Perform a fetch for every nth row in the result set.
                try (ResultSet rs = stmt.executeQuery(SQL)) {
                    timerTest(n, rs);
                }
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void timerTest(int fetchSize,
            ResultSet rs) throws SQLException {

        // Declare the variables for tracking the row count and elapsed time.
        int rowCount = 0;
        long startTime = 0;
        long stopTime = 0;
        long runTime = 0;

        // Set the fetch size then iterate through the result set to
        // cache the data locally.
        rs.setFetchSize(fetchSize);
        startTime = System.currentTimeMillis();
        while (rs.next()) {
            rowCount++;
        }
        stopTime = System.currentTimeMillis();
        runTime = stopTime - startTime;

        // Display the results of the timer test.
        System.out.println("FETCH SIZE: " + rs.getFetchSize());
        System.out.println("ROWS PROCESSED: " + rowCount);
        System.out.println("TIME TO EXECUTE: " + runTime);
        System.out.println();
    }
}
```

## <a name="see-also"></a>Consulte Também  

[Trabalhando com conjuntos de resultados](../../../connect/jdbc/code-samples/working-with-result-sets.md)  
