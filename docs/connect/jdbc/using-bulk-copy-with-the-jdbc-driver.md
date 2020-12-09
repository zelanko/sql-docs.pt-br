---
title: Como usar cópia em massa com o JDBC Driver
description: A classe SQLServerBulkCopy permite que você grave soluções de carregamento de dados em Java que oferecem vantagens significativas de desempenho em relação às APIs JDBC padrão.
ms.custom: ''
ms.date: 08/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52f465b4cfdcb2ff771a71c1ef956af78b522358
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96442877"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>Como usar cópia em massa com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft SQL Server inclui um utilitário de linha de comando popular chamado `bcp` para copiar rapidamente em massa grandes arquivos para tabelas ou exibições em bancos de dados do SQL Server. A classe `SQLServerBulkCopy` permite escrever soluções de código no Java que fornecem funcionalidade semelhante. Há outras maneiras de carregar dados em uma tabela do SQL Server (instruções INSERT, por exemplo), mas `SQLServerBulkCopy` oferece uma vantagem de desempenho significativa sobre eles.  
  
A classe `SQLServerBulkCopy` pode ser usada para gravar dados somente em tabelas do SQL Server. Mas a fonte de dados não está limitada ao SQL Server; qualquer fonte de dados pode ser usada, desde que os dados possam ser lidos com uma implementação `ResultSet`, `RowSet` ou `ISQLServerBulkRecord`.  
  
Usando a classe `SQLServerBulkCopy`, você pode executar:  
  
- Uma única operação de cópia em massa  
  
- Várias operações de cópia em massa  
  
- Uma operação de cópia em massa com uma transação  
  
> [!NOTE]  
> Ao usar o Microsoft JDBC Driver 4.1 para SQL Server ou anterior (que não dá suporte à classe SQLServerBulkCopy), você pode executar a instrução BULK INSERT do Transact-SQL no SQL Server, em vez disso.  
  
## <a name="bulk-copy-example-setup"></a>Configuração de exemplo de cópia em massa  

A classe `SQLServerBulkCopy` pode ser usada para gravar dados somente em tabelas do SQL Server. Os exemplos de código mostrados neste artigo usam o banco de dados de exemplo do SQL Server, [AdventureWorks](../../samples/adventureworks-install-configure.md). Para evitar a alteração das tabelas existentes nos exemplos de código, primeiro grave os dados em tabelas criadas por você.  
  
Ambas as tabelas `BulkCopyDemoMatchingColumns` e `BulkCopyDemoDifferentColumns` são baseadas na tabela `Production.Products` do AdventureWorks. Nos exemplos de código que usam essas tabelas, os dados são adicionados da tabela `Production.Products` para uma dessas tabelas de exemplo. A tabela `BulkCopyDemoDifferentColumns` é usada quando o exemplo ilustra como mapear colunas de dados de origem para a tabela de destino; `BulkCopyDemoMatchingColumns` é usada na maioria dos outros exemplos.  
  
Alguns dos exemplos de código demonstram como usar uma classe `SQLServerBulkCopy` para gravar em várias tabelas. Para esses exemplos, as tabelas `BulkCopyDemoOrderHeader` e `BulkCopyDemoOrderDetail` são usadas como tabelas de destino. Essas tabelas se baseiam nas tabelas `Sales.SalesOrderHeader` e `Sales.SalesOrderDetail` do AdventureWorks.  
  
> [!NOTE]  
> Os exemplos de código `SQLServerBulkCopy` são fornecidos para demonstrar a sintaxe para usar somente `SQLServerBulkCopy`. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar um INSERT do Transact-SQL... Instrução SELECT para copiar os dados.  

### <a name="table-setup"></a>Configuração da tabela  

Para criar as tabelas necessárias para que os exemplos de código sejam executado corretamente, você deve executar as seguintes instruções Transact-SQL em um banco de dados do SQL Server.  

```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```

## <a name="single-bulk-copy-operations"></a>Operação únicas de cópia em massa

A abordagem mais simples para a execução de uma operação de cópia em massa do SQL Server é executar uma única operação em um banco de dados. Por padrão, uma operação de cópia em massa é executada como uma operação isolada: a operação de cópia ocorre de forma não transacionada, sem a oportunidade de disponibilizá-la de volta.  
  
> [!NOTE]  
> Se você precisar reverter toda ou parte da cópia em massa quando ocorrer um erro, poderá usar uma transação gerenciada `SQLServerBulkCopy` ou executar a operação de cópia em massa dentro de uma transação existente.  
> Para obter mais informações, veja [Operações de cópia em massa e transação](#transaction-and-bulk-copy-operations)  
  
 As etapas gerais para executar uma operação de cópia em massa são:  
  
1. Conectar-se ao servidor de origem e obter os dados a serem copiados. Os dados também podem vir de outras fontes, desde que possam ser recuperados de um objeto `ResultSet` ou de uma implementação `ISQLServerBulkRecord`.  
  
2. Conecte-se ao servidor de destino (a menos que deseje que `SQLServerBulkCopy` estabeleça uma conexão para você).  
  
3. Crie um objeto `SQLServerBulkCopy`, configurando as propriedades necessárias por meio de `setBulkCopyOptions`.  
  
4. Chame o método `setDestinationTableName` para indicar a tabela de destino para a operação Bulk Insert.  
  
5. Chame um dos métodos `writeToServer`.  
  
6. Opcionalmente, atualize as propriedades por meio de `setBulkCopyOptions` e chame `writeToServer` novamente, conforme necessário.  
  
7. Chame `close` ou encapsule as operações de cópia em massa em uma instrução para tentar com recursos.  
  
> [!CAUTION]  
> É recomendável que os tipos de dados da coluna de origem e destino correspondam. Se os tipos de dados não corresponderem, `SQLServerBulkCopy` tentará converter cada valor de origem para o tipo de dados de destino. As conversões podem afetar o desempenho e também podem resultar em erros inesperados. Por exemplo, um tipo de dados duplo pode ser convertido em um tipo de dados decimal na maior parte das vezes, mas não sempre.  
  
### <a name="example"></a>Exemplo

O aplicativo a seguir demonstra como carregar dados usando a classe `SQLServerBulkCopy`. Neste exemplo, um `ResultSet` é usado para copiar dados da tabela Production.Product no banco de dados AdventureWorks do SQL Server em uma tabela semelhante no mesmo banco de dados.  
  
> [!IMPORTANT]  
> Este exemplo não funcionará, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração da tabela](#table-setup). Esse código é fornecido para demonstrar a sintaxe para usar somente `SQLServerBulkCopy`. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar um INSERT do Transact-SQL... Instrução SELECT para copiar os dados.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopySingle {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // In real world applications you would
            // not use SQLServerBulkCopy to move data from one table to the other
            // in the same database. This is for demonstration purposes only.

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // table match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(rsSourceData);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Executando uma operação de cópia em massa usando Transact-SQL

O exemplo a seguir ilustra como usar o método `executeUpdate` para executar a instrução BULK INSERT.  
  
> [!NOTE]  
> O caminho do arquivo da fonte de dados é relativo ao servidor. O processo do servidor deve ter acesso a esse caminho para que a operação de cópia em massa seja bem-sucedida.  

```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  

## <a name="multiple-bulk-copy-operations"></a>Várias operações de cópia em massa  

Você pode executar várias operações de cópia em massa usando uma única instância de uma classe `SQLServerBulkCopy`. Se os parâmetros da operação forem alterados entre as cópias (por exemplo, o nome da tabela de destino), você deverá atualizá-los antes de qualquer chamada subsequentes a qualquer um dos métodos `writeToServer`, conforme demonstrado no exemplo a seguir. A menos que explicitamente alterados, todos os valores de propriedade permanecem como estavam na operação de cópia em massa anterior para determinada instância.  

> [!NOTE]  
> A execução de várias operações de cópia em massa usando a mesma instância de `SQLServerBulkCopy` é geralmente mais eficiente do que usar uma instância separada para cada operação.  
  
Se você executar várias operações de cópia em massa usando o mesmo objeto `SQLServerBulkCopy`, não haverá restrições se as informações de origem ou de destino forem iguais ou diferentes em cada operação. No entanto, você deve garantir que as informações de associação da coluna sejam definidas corretamente sempre que você gravar no servidor.  
  
> [!IMPORTANT]  
> Este exemplo não funcionará, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração da tabela](#table-setup). Esse código é fornecido para demonstrar a sintaxe para usar somente `SQLServerBulkCopy`. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar um INSERT do Transact-SQL... Instrução SELECT para copiar os dados.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyMultiple {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationHeaderTable = "dbo.BulkCopyDemoOrderHeader";
        String destinationDetailTable = "dbo.BulkCopyDemoOrderDetail";
        int countHeaderBefore, countDetailBefore, countHeaderAfter, countDetailAfter;
        ResultSet rsHeader, rsDetail;

        try (Connection sourceConnection1 = DriverManager.getConnection(connectionUrl);
                Connection sourceConnection2 = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection1.createStatement();
                PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(
                        "SELECT [SalesOrderID], [OrderDate], [AccountNumber] FROM [Sales].[SalesOrderHeader] WHERE [AccountNumber] = ?;");
                PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(
                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], [SalesOrderDetailID], [OrderQty], [ProductID], [UnitPrice] FROM "
                                + "[Sales].[SalesOrderDetail] INNER JOIN [Sales].[SalesOrderHeader] ON "
                                + "[Sales].[SalesOrderDetail].[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] WHERE [AccountNumber] = ?;");
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl);) {

            // Empty the destination tables.
            stmt.executeUpdate("DELETE FROM " + destinationHeaderTable);
            stmt.executeUpdate("DELETE FROM " + destinationDetailTable);

            // Perform an initial count on the destination
            // table with matching columns.
            countHeaderBefore = getRowCount(stmt, destinationHeaderTable);

            // Perform an initial count on the destination
            // table with different column positions.
            countDetailBefore = getRowCount(stmt, destinationDetailTable);

            // Get data from the source table as a ResultSet.
            // The Sales.SalesOrderHeader and Sales.SalesOrderDetail
            // tables are quite large and could easily cause a timeout
            // if all data from the tables is added to the destination.
            // To keep the example simple and quick, a parameter is
            // used to select only orders for a particular account
            // as the source for the bulk insert.
            preparedStmt1.setString(1, "10-4020-000034");
            rsHeader = preparedStmt1.executeQuery();

            // Get the Detail data in a separate connection.
            preparedStmt2.setString(1, "10-4020-000034");
            rsDetail = preparedStmt2.executeQuery();

            // Create the SQLServerBulkCopySQLServerBulkCopy object.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setBulkCopyTimeout(100);
            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationHeaderTable);

            // Guarantee that columns are mapped correctly by
            // defining the column mappings for the order.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("OrderDate", "OrderDate");
            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");

            // Write rsHeader to the destination.
            bulkCopy.writeToServer(rsHeader);

            // Set up the order details destination.
            bulkCopy.setDestinationTableName(destinationDetailTable);

            // Clear the existing column mappings
            bulkCopy.clearColumnMappings();

            // Add order detail column mappings.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("SalesOrderDetailID", "SalesOrderDetailID");
            bulkCopy.addColumnMapping("OrderQty", "OrderQty");
            bulkCopy.addColumnMapping("ProductID", "ProductID");
            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");

            // Write rsDetail to the destination.
            bulkCopy.writeToServer(rsDetail);

            // Perform a final count on the destination
            // tables to see how many rows were added.
            countHeaderAfter = getRowCount(stmt, destinationHeaderTable);
            countDetailAfter = getRowCount(stmt, destinationDetailTable);

            System.out.println((countHeaderAfter - countHeaderBefore) + " rows were added to the Header table.");
            System.out.println((countDetailAfter - countDetailBefore) + " rows were added to the Detail table.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

## <a name="transaction-and-bulk-copy-operations"></a>Transações e operações de cópia em massa

 Operações de cópia em massa podem ser executadas como operações isoladas ou como parte de uma transação de várias etapas. Essa última opção permite executar mais de uma operação de cópia em massa dentro da mesma transação, bem como executar outras operações de banco de dados (como inserções, atualizações e exclusões), podendo ainda confirmar ou reverter toda a transação.  
  
 Por padrão, uma operação de cópia em massa é executada como uma operação isolada. A operação de cópia em massa ocorre de forma não transacionada, sem a oportunidade de revertê-la novamente. Se você precisar reverter toda ou parte da cópia em massa quando ocorrer um erro, poderá usar uma transação gerenciada `SQLServerBulkCopy` ou executar a operação de cópia em massa dentro de uma transação existente.  

## <a name="extended-bulk-copy-for-azure-data-warehouse"></a>Cópia em massa estendida para o Azure Data Warehouse

A versão do Driver v8.4.1 adiciona uma nova propriedade de conexão, `sendTemporalDataTypesAsStringForBulkCopy`. Essa propriedade booliana é `true` por padrão.

Essa propriedade de conexão, quando definida como `false`, enviará os tipos de dados **DATE**, **DATETIME**, **DATIMETIME2**, **DATETIMEOFFSET**, **SMALLDATETIME** e **TIME** como os respectivos tipos, em vez de enviá-los com Cadeia de caracteres.

O envio dos tipos de dados temporais como seus respectivos tipos permite que o usuário envie dados nessas colunas para o Azure Synapse Analytics, o que não era possível antes devido ao driver converter os dados em uma cadeia de caracteres. O envio de dados de cadeia de caracteres em colunas temporais funciona para o SQL Server porque o SQL Server executaria a conversão implícita para nós, mas isso não acontece com o Azure Synapse Analytics.

Além disso, mesmo sem definir essa cadeia de conexão como "false", da **v8.4.1** em diante, os tipos de dados **MONEY** e **SMALLMONEY** serão enviados como os tipos de dados **MONEY** / **SMALLMONEY**, em vez de **DECIMAL**, o que também permite que esses tipos de dados sejam copiados em massa para o Azure Synapse Analytics.

### <a name="extended-bulk-copy-for-azure-data-warehouse-limitations"></a>Limitações da cópia em massa estendida para o Azure Data Warehouse

Atualmente, há duas limitações:

1. Com essa propriedade de conexão definida como `false`, o driver aceitará apenas o formato literal da cadeia de caracteres padrão de cada tipo de dados temporal, por exemplo:

    `DATE: YYYY-MM-DD`

    `DATETIME: YYYY-MM-DD hh:mm:ss[.nnn]`

    `DATETIME2: YYYY-MM-DD hh:mm:ss[.nnnnnnn]`

    `DATETIMEOFFSET: YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+/-}hh:mm]`

    `SMALLDATETIME:YYYY-MM-DD hh:mm:ss`

    `TIME: hh:mm:ss[.nnnnnnn]`

2. Com essa propriedade de conexão definida como `false`, o tipo de coluna especificado para cópia em massa deve respeitar o gráfico de mapeamento de tipo de dados de [aqui](../../connect/jdbc/using-basic-data-types.md). Por exemplo, os usuários anteriores podiam especificar `java.sql.Types.TIMESTAMP` para copiar dados em massa em uma coluna de `DATE`, porém, com esse recurso habilitado, eles devem especificar `java.sql.Types.DATE` para executar o mesmo.
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>Executando uma operação de cópia em massa não transacionada

O aplicativo a seguir mostra o que acontece quando uma operação de cópia em massa não transacionada encontra um erro na operação.  
  
No exemplo, tanto a tabela de origem quanto a tabela de destino incluem uma coluna de identidade chamada `ProductID`. O código prepara primeiro a tabela de destino excluindo todas as linhas e, em seguida, inserindo uma única linha cuja `ProductID` é conhecida por existir na tabela de origem. Por padrão, um novo valor para a coluna de identidade é gerado na tabela de destino para cada linha adicionada. Neste exemplo, uma opção é definida quando a conexão é aberta, o que força o processo de carregamento em massa a usar os valores de identidade da tabela de origem.  
  
A operação de cópia em massa é executada com a propriedade `BatchSize` definida como 10. Quando a operação encontra a linha inválida, uma exceção é lançada. Neste primeiro exemplo, a operação de cópia em massa é não transacionada. Todos os lotes copiados até o ponto do erro são confirmados; o lote que contém a chave duplicada é revertido e a operação de cópia em massa é interrompida antes de processar todos os outros lotes.  
  
> [!NOTE]  
> Este exemplo não funcionará, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração da tabela](#table-setup). Esse código é fornecido para demonstrar a sintaxe para usar somente `SQLServerBulkCopy`. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar um INSERT do Transact-SQL... Instrução SELECT para copiar os dados.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyNonTransacted {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error
            // after some of the batches have been copied.
            try {
                bulkCopy.writeToServer(rsSourceData);
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Como executar uma operação de cópia em massa dedicada em uma transação

Por padrão, uma operação de cópia em massa não cria transações em si. Quando você quiser executar uma operação de cópia em massa dedicada, crie uma instância de `SQLServerBulkCopy` com uma cadeia de conexão. Nesse cenário, cada lote da operação de cópia em massa é confirmado implicitamente pelo banco de dados. Você pode definir a opção `UseInternalTransaction` como `true` em `SQLServerBulkCopyOptions` para fazer com que a operação de cópia em massa crie transações, executando uma confirmação após cada lote da operação de cópia em massa.
  
```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```

### <a name="using-existing-transactions"></a>Usando transações existentes

Você poderá passar um objeto `Connection` que tem transações habilitadas como um parâmetro em um construtor `SQLServerBulkCopy`. Nessa situação, a operação de cópia em massa é executada em uma transação existente e nenhuma alteração é feita ao estado da transação (isto é, ela não é confirmada nem anulada). Isso permite que um aplicativo inclua a operação de cópia em massa em uma transação com outras operações de banco de dados. Se precisar reverter a operação de cópia em massa inteira por causa de um erro ou se a cópia em massa precisar ser executada como parte de um processo maior que pode ser revertido, você poderá executar a reversão no objeto `Connection` a qualquer momento após a operação de cópia em massa.  
  
O seguinte aplicativo é semelhante a `BulkCopyNonTransacted`, com uma exceção: neste exemplo, a operação de cópia em massa está incluída em uma transação maior, externa. Quando ocorre o erro de violação de chave primária, a transação inteira é revertida e nenhuma linha é adicionada à tabela de destino.

> [!NOTE]  
> Este exemplo não funcionará, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração da tabela](#table-setup). Esse código é fornecido para demonstrar a sintaxe para usar somente `SQLServerBulkCopy`. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar um INSERT do Transact-SQL... Instrução SELECT para copiar os dados.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyExistingTransactions {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;
        SQLServerBulkCopyOptions copyOptions;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object inside the transaction.
            destinationConnection.setAutoCommit(false);

            copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error.
            try {
                bulkCopy.writeToServer(rsSourceData);
                destinationConnection.commit();
            }
            catch (SQLException e) {
                e.printStackTrace();
                destinationConnection.rollback();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        catch (Exception e) {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="bulk-copy-from-a-csv-file"></a>Cópia em massa de um arquivo CSV  

 O aplicativo a seguir demonstra como carregar dados usando a classe `SQLServerBulkCopy`. Neste exemplo, um arquivo CSV é usado para copiar dados da tabela Production. Product no banco de dados AdventureWorks do SQL Server em uma tabela semelhante no banco de dados.  
  
> [!IMPORTANT]  
> Essa amostra não será executada, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração da tabela](#table-setup) para obtê-la.  
  
1. Abra o **SQL Server Management Studio** e conecte-se ao SQL Server com o banco de dados AdventureWorks.  
  
2. Expanda os bancos de dados, clique com o botão direito do mouse no banco de dados AdventureWorks, selecione **Tarefas** e **Exportar Dados**...  
  
3. Para a Fonte de Dados, selecione a **Fonte de Dados** que permite que você se conecte ao SQL Server (por exemplo, SQL Server Native Client 11.0), verifique a configuração e clique em **Avançar**  
  
4. Para o Destino, selecione o **Destino de Arquivo Simples** e insira um **Nome de Arquivo** com um destino, como `C:\Test\TestBulkCSVExample.csv`. Verifique se o **Formato** é Delimitado, se o **Qualificador de texto** é nenhum, habilite os **Nomes de coluna na primeira linha de dados** e, em seguida, selecione **Avançar**  
  
5. Selecione **Gravar uma consulta para especificar os dados a serem transferidos** e **Avançar**.  Insira sua **instrução SQL** `SELECT ProductID, Name, ProductNumber FROM Production.Product` e clique em **Avançar**  
  
6. Verifique a configuração: Você pode deixar o delimitador de linha como `{CR}{LF}` e o delimitador de coluna como a vírgula `{,}`.  Selecione **Editar Mapeamentos**… e verifique se o **Tipo** de dados está correto para cada coluna (por exemplo, inteiro para `ProductID` e cadeia de caracteres Unicode para os demais).  
  
7. Vá para **Concluir** e execute a exportação.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopyCSV {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;

        // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.
        // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.
        try (Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = destinationConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);
                SQLServerBulkCSVFileRecord fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);) {

            // Set the metadata for each column to be copied.
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // data reader match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(fileRecord);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```  

### <a name="bulk-copy-with-delimiters-as-data-in-csv-file"></a>Cópia em massa com delimitadores como dados no arquivo CSV

O Driver versão 8.4.1 adiciona uma API `SQLServerBulkCSVFileRecord.setEscapeColumnDelimitersCSV(boolean)`. Quando definido como true, as seguintes regras são aplicadas:

- Cada campo pode ou não ser colocado entre aspas duplas.
- Se os campos não estiverem entre aspas duplas, as aspas duplas poderão não aparecer dentro dos campos.
- Os campos que contêm aspas duplas e delimitadores devem ser colocados entre aspas duplas.
- Se as aspas duplas forem usadas para incluir campos, uma aspa dupla que aparece dentro de um campo deverá ser ignorada precedendo-a com outra aspa dupla.

### <a name="bulk-copy-with-always-encrypted-columns"></a>Cópia em massa com colunas Always Encrypted  

A partir do Microsoft JDBC Driver 6.0 para SQL Server, há suporte para cópia em massa com colunas Always Encrypted.  
  
Dependendo das opções de cópia em massa e do tipo de criptografia de tabelas de origem e destino, o driver JDBC pode descriptografar de forma transparente e, em seguida, criptografar os dados, ou pode enviar os dados criptografados como estão. Por exemplo, ao copiar em massa dados de uma coluna criptografada para uma coluna não criptografada, o driver descriptografa de modo transparente os dados antes de enviá-los para o SQL Server. Da mesma forma, ao copiar dados em massa de uma coluna não criptografada (ou de um arquivo CSV) para uma coluna criptografada, o driver criptografa de modo transparente os dados antes de enviá-los para o SQL Server. Se tanto a origem quanto o destino estiverem criptografados, então, dependendo da opção de cópia em massa `allowEncryptedValueModifications`, o driver enviará dados como estão ou descriptografará os dados e os criptografará novamente antes de enviá-los para o SQL Server.  
  
Para obter mais informações, confira a opção de cópia em massa `allowEncryptedValueModifications` abaixo e a seção [Uso do Always Encrypted com o Driver JDBC](using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
> Limitação do Microsoft JDBC Driver 6.0 para SQL Server ao copiar dados em massa de um arquivo CSV para colunas criptografadas:  
>
> Somente o formato literal de cadeia de caracteres padrão do Transact-SQL é compatível com os tipos de data e hora  
>
> Os tipos de dados DATETIME e SMALLDATETIME não são compatíveis  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>API de cópia em massa para o driver JDBC  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy

Permite o carregamento em massa eficiente de uma tabela do SQL Server que contém dados de outra fonte.  
  
O Microsoft SQL Server inclui um utilitário de prompt de comando popular chamado bcp para mover dados de uma tabela para outra, seja em um único servidor ou entre servidores. A classe `SQLServerBulkCopy` permite escrever soluções de código em Java que fornecem funcionalidade semelhante. Há outras maneiras de carregar dados em uma tabela do SQL Server (instruções INSERT, por exemplo), mas `SQLServerBulkCopy` oferece uma vantagem de desempenho significativa sobre elas.  
  
A classe `SQLServerBulkCopy` pode ser usada para gravar dados somente em tabelas do SQL Server. No entanto, a fonte de dados não está limitada ao SQL Server; qualquer fonte de dados pode ser usada, contanto que os dados possam ser lidos com uma instância `ResultSet` ou uma implementação `ISQLServerBulkRecord`.  
  
| Construtor | Descrição |
| ----------- | ----------- |
| `SQLServerBulkCopy(Connection connection)` | Inicializa uma nova instância da classe `SQLServerBulkCopy` usando a instância aberta especificada de `SQLServerConnection`. Se `Connection` tiver transações habilitadas, as operações de cópia serão executadas dentro da transação. |
| `SQLServerBulkCopy(String connectionURL)` | Inicializa e abre uma nova instância de `SQLServerConnection` com base na `connectionURL` fornecida. O construtor usa `SQLServerConnection` para inicializar uma nova instância da classe `SQLServerBulkCopy`. |
  
| Propriedade | DESCRIÇÃO |
| -------- | ----------- |
| `String DestinationTableName` | O nome da tabela de destino no servidor.<br /><br /> Se `DestinationTableName` não tiver sido definida quando `writeToServer` for chamada, uma `SQLServerException` será lançada.<br /><br /> `DestinationTableName` é um nome de três partes (`<database>.<owningschema>.<name>`). Você pode qualificar o nome da tabela com seu banco de dados e o esquema de propriedade, se quiser. No entanto, se o nome da tabela usar um sublinhado ("_") ou outros caracteres especiais, você deve ignorar o nome usando colchetes. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md). |
| `ColumnMappings` | Mapeamentos de coluna definem as relações entre colunas na fonte de dados e colunas no destino.<br /><br /> Se os mapeamentos não forem definidos, as colunas serão mapeadas implicitamente com base na posição ordinal. Para que isso funcione, os esquemas de origem e destino devem corresponder. Se não corresponderem, uma exceção será lançada.<br /><br /> Se os mapeamentos não estiverem vazios, nem todas as colunas presentes na fonte de dados deverão ser especificadas. Aquelas não mapeadas serão ignoradas.<br /><br /> Você pode se referir às colunas de origem e de destino por nome ou ordinal. |
  
| Método | Descrição |
| ------ | ----------- |
| `void addColumnMapping(int sourceColumn, int destinationColumn)` | Adiciona um novo mapeamento de coluna, usando números ordinais para especificar colunas de origem e destino. |
| `void addColumnMapping (int sourceColumn, String destinationColumn)` | Adiciona um novo mapeamento de coluna, usando um ordinal para a coluna de origem e um nome de coluna para a coluna de destino. |
| `void addColumnMapping (String sourceColumn, int destinationColumn)` | Adiciona um novo mapeamento de coluna, usando um nome de coluna para descrever a coluna de origem e um ordinal para especificar a coluna de destino. |
| `void addColumnMapping (String sourceColumn, String destinationColumn)` | Adiciona um novo mapeamento de coluna, usando nomes de coluna para especificar colunas de origem e destino. |
| `void clearColumnMappings()` | Exclui o conteúdo dos mapeamentos de coluna. |
| `void close()` | Fecha a instância de `SQLServerBulkCopy`. |
| `SQLServerBulkCopyOptions getBulkCopyOptions()` | Recupera o conjunto atual de `SQLServerBulkCopyOptions`. |
| `String getDestinationTableName()` | Recupera o nome da tabela de destino atual. |
| `void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)` | Atualiza o comportamento da instância de `SQLServerBulkCopy` de acordo com as opções fornecidas. |
| `void setDestinationTableName(String tableName)` | Define o nome da tabela de destino. |
| `void writeToServer(ResultSet sourceData)` | Copia todas as linhas da `ResultSet` fornecida para uma tabela de destino especificada pela propriedade `DestinationTableName` do objeto `SQLServerBulkCopy`. |
| `void writeToServer(RowSet sourceData)` | Copia todas as linhas da `RowSet` fornecida para uma tabela de destino especificada pela propriedade `DestinationTableName` do objeto `SQLServerBulkCopy`. |
| `void writeToServer(ISQLServerBulkRecord sourceData)` | Copia todas as linhas da implementação `ISQLServerBulkRecord` fornecida para uma tabela de destino especificada pela propriedade `DestinationTableName` do objeto `SQLServerBulkCopy`. |
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  

 Uma coleção de configurações que controla como os métodos `writeToServer` se comportam em uma instância de `SQLServerBulkCopy`.  
  
| Construtor | Descrição |
| ----------- | ----------- |
| `SQLServerBulkCopyOptions()` | Inicializa uma nova instância da classe `SQLServerBulkCopyOptions` usando os valores padrão para todas as configurações. |
  
 Existem getters e setters para as seguintes opções:  
  
| Opção | Descrição | Padrão |
| ------ | ----------- | ------- |
| `boolean CheckConstraints` | Verificar restrições enquanto os dados são inseridos. | False – as restrições não são verificadas |
| `boolean FireTriggers` | Faz com que o servidor dispare gatilhos de inserção para as linhas que estão sendo inseridas no banco de dados. | Falso - nenhum gatilho é disparado |
| `boolean KeepIdentity` | Preservar valores de identidade de origem. | Falso - valores de identidade são atribuídos pelo destino |
| `boolean KeepNulls` | Preservar valores nulos na tabela de destino, independentemente das configurações dos valores padrão. | Falso - valores nulos são substituídos por valores padrão, quando aplicável. |
| `boolean TableLock` | Obter um bloqueio de atualização em massa para a duração da operação de cópia em massa. | No caso de Falso, são usados bloqueios de linha. |
| `boolean UseInternalTransaction` | Quando definido como `true`, cada lote da operação de cópia de massa ocorre dentro de uma transação. Se `SQLServerBulkCopy` estiver usando uma conexão existente (conforme definido pelo construtor), uma `SQLServerException` ocorrerá.  Se `SQLServerBulkCopy` tiver criado uma conexão dedicada, uma transação será criada e confirmada para cada lote. | Falso - nenhuma transação |
| `int BatchSize` | Número de linhas em cada lote. No final de cada lote, as linhas no lote são enviados para o servidor.<br /><br /> Um lote estará concluído quando as linhas `BatchSize` forem processadas ou não houver mais linhas para enviar para a fonte de dados de destino.  Se a instância de `SQLServerBulkCopy` tiver sido declarada com a opção `UseInternalTransaction` definida como `false`, as linhas serão enviadas ao servidor, `BatchSize` linhas por vez, mas nenhuma ação relacionada à transação será executada. Se `UseInternalTransaction` for definido como `true`, cada lote de linhas será executado dentro de uma transação explícita. | 0 – indica que cada operação `writeToServer` é um lote único |
| `int BulkCopyTimeout` | Número de segundos para a conclusão da operação antes que ela atinja o tempo limite. Um valor 0 indica que não há limite; a cópia em massa vai esperar indefinidamente. | 60 segundos. |
| `boolean allowEncryptedValueModifications` | Essa opção está disponível com o Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server.<br /><br /> Quando definido como `true`, `allowEncryptedValueModifications` permite a cópia em massa de dados criptografados entre tabelas ou bancos de dados, sem precisar descriptografá-los. Normalmente, um aplicativo selecionaria dados de colunas criptografadas de uma tabela sem descriptografar os dados (o aplicativo se conectaria ao banco de dados com a palavra-chave de configuração de criptografia de coluna definida como desabilitada) e, em seguida, usaria essa opção para inserção em massa dos dados, que ainda estariam criptografado. Para obter mais informações, veja [Como usar Always Encrypted com o driver ODBC](using-always-encrypted-with-the-jdbc-driver.md).<br /><br /> Tenha cuidado ao configurar `allowEncryptedValueModifications` como `true`, pois isso pode levar à corrupção do banco de dados, já que o driver não verifica se os dados estão realmente criptografados ou se estão criptografados corretamente usando o mesmo tipo, algoritmo e chave de criptografia que a coluna de destino. |
  
 Getters e setters:  
  
| Métodos | Descrição |
| ------- | ----------- |
| `boolean isCheckConstraints()` | Indica se as restrições devem ser verificadas durante a inserção de dados ou não. |
| `void setCheckConstraints(boolean checkConstraints)` | Define se as restrições devem ser verificadas durante a inserção de dados ou não. |
| `boolean isFireTriggers()` | Indica se o servidor deve disparar os gatilhos de inserção para as linhas que estão sendo inseridas no banco de dados. |
| `void setFireTriggers(boolean fireTriggers)` | Define se o servidor deve ser definido como para disparar gatilhos para as linhas que estão sendo inseridas no banco de dados. |
| `boolean isKeepIdentity()` | Indica se é preciso ou não preservar quaisquer valores de identidade de origem. |
| `void setKeepIdentity(boolean keepIdentity)` | Define é preciso ou não preservar os valores de identidade. |
| `boolean isKeepNulls()` | Indica se é necessário preservar valores nulos na tabela de destino, independentemente das configurações de valores padrão ou se eles devem ser substituídos pelos valores padrão (quando aplicável). |
| `void setKeepNulls(boolean keepNulls)` | Define se é necessário preservar valores nulos na tabela de destino, independentemente das configurações de valores padrão ou se eles devem ser substituídos pelos valores padrão (quando aplicável). |
| `boolean isTableLock()` | Indica se `SQLServerBulkCopy` deve obter um bloqueio de atualização em massa durante toda a operação de cópia em massa. |
| `void setTableLock(boolean tableLock)` | Define se `SQLServerBulkCopy` deve obter um bloqueio de atualização em massa durante toda a operação de cópia em massa. |
| `boolean isUseInternalTransaction()` | Indica se cada lote da operação de cópia de massa ocorrerá dentro de uma transação. |
| `void setUseInternalTranscation(boolean useInternalTransaction)` | Define se cada lote da operação de cópia de massa ocorrerá dentro de uma transação. |
| `int getBatchSize()` | Obtém número de linhas de cada lote. No final de cada lote, as linhas no lote são enviados para o servidor. |
| `void setBatchSize(int batchSize)` | Define o número de linhas de cada lote. No final de cada lote, as linhas no lote são enviados para o servidor. |
| `int getBulkCopyTimeout()` | Obtém o número de segundos para a conclusão da operação antes que ela expire. |
| `void  setBulkCopyTimeout(int timeout)` | Define o número de segundos para a conclusão da operação antes que ela expire. |
| `boolean isAllowEncryptedValueModifications()` | Indica se a configuração `allowEncryptedValueModifications` está habilitada ou desabilitada. |
| `void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)` | Define a configuração `allowEncryptedValueModifications` que é usada para cópia em massa com colunas Always Encrypted. |
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  

 A interface `ISQLServerBulkRecord` pode ser usada para criar classes que leem dados de qualquer fonte (como arquivos, por exemplo) e permitir que uma instância do `SQLServerBulkCopy` carregue em massa uma tabela do SQL Server com esses dados.  
  
| Métodos de interface | Descrição |
| ----------------- | ----------- |
| `set<Integer> getColumnOrdinals()` | Obter os ordinais de cada uma das colunas representadas neste registro de dados. |
| `String getColumnName(int column)` | Obter o nome da coluna especificada. |
| `int getColumnType(int column)` | Obter o tipo de dados JDBC da coluna especificada. |
| `int getPrecision(int column)`  | Obter a precisão da coluna especificada. |
| `object[] getRowData()` | Obtém os dados para a linha atual como uma matriz de objetos.<br /><br /> Cada objeto deve corresponder ao tipo de linguagem Java que é usado para representar o tipo de dados JDBC indicado da coluna especificada.  Para obter mais informações, confira [Entendimento dos tipos de dados do JDBC Driver](understanding-the-jdbc-driver-data-types.md) para ver os mapeamentos apropriados". |
| `int getScale(int column)` | Obter a escala para a coluna especificada. |
| `boolean isAutoIncrement(int column)` | Indica se a coluna representa uma coluna de identidade. |
| `boolean next()` | Avança para a próxima linha de dados. |
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  

Uma simples implementação da interface `ISQLServerBulkRecord` que pode ser usada para ler os tipos de dados básicos do Java por meio de um arquivo delimitado, em que cada linha representa uma linha de dados.  
  
Notas e limitações de implementação:  
  
1. A quantidade máxima de dados permitida em qualquer linha é limitada pela memória disponível porque os dados são lidos uma linha de cada vez.  
  
2. O streaming de tipos de dados grandes, como `varchar(max)`, `varbinary(max)`, `nvarchar(max)`, `sqlxml` e `ntext` não é compatível.  
  
3. O delimitador especificado para o arquivo CSV não deve aparecer em nenhum lugar nos dados e deve ser ignorado corretamente se for um caractere restrito em expressões Java regulares.  
  
4. Na implementação do arquivo CSV, aspas duplas são tratadas como parte dos dados. Por exemplo, a linha `hello,"world","hello,world"` será tratada como tendo quatro colunas com os valores `hello`, `"world"`, `"hello` e `world"` caso o delimitador seja a vírgula.  
  
5. Caracteres de nova linha são usados como terminadores de linha e não são permitidos em nenhum lugar nos dados.  
  
| Construtor | Descrição |
| ----------- | ----------- |
| `SQLServerBulkCSVFileRecord(String fileToParse, String encoding, String delimiter, boolean firstLineIsColumnNames)` | Inicializa uma nova instância da classe `SQLServerBulkCSVFileRecord`, que analisa cada linha em `fileToParse` com a codificação e o delimitador fornecidos. Se `firstLineIsColumnNames` for definido como True, a primeira linha no arquivo será analisada como nomes de coluna.  Se a codificação for NULL, a codificação padrão será usada. |
| `SQLServerBulkCSVFileRecord(String fileToParse, String encoding, boolean firstLineIsColumnNames)` | Inicializa uma nova instância da classe `SQLServerBulkCSVFileRecord`, que analisa cada linha em `fileToParse` com a vírgula como delimitador e a codificação fornecida. Se `firstLineIsColumnNames` for definido como True, a primeira linha no arquivo será analisada como nomes de coluna.  Se a codificação for NULL, a codificação padrão será usada. |
| `SQLServerBulkCSVFileRecord(String fileToParse, boolean firstLineIsColumnNames` | Inicializa uma nova instância da classe `SQLServerBulkCSVFileRecord`, que analisa cada linha em `fileToParse` com a vírgula como delimitador e a codificação padrão. Se `firstLineIsColumnNames` for definido como True, a primeira linha no arquivo será analisada como nomes de coluna. |
  
| Método | Descrição |
| ------ | ----------- |
| `void addColumnMetadata(int positionInFile, String columnName, int jdbcType, int precision, int scale)` | Adiciona metadados da coluna especificada no arquivo. |
| `void close()` | Libera todos os recursos associados ao leitor de arquivos. |
| `void setTimestampWithTimezoneFormat(DateTimeFormatter dateTimeFormatter)` | Define o formato para analisar os dados de carimbo de data/hora do arquivo como `java.sql.Types.TIMESTAMP_WITH_TIMEZONE`. |
| `void setTimestampWithTimezoneFormat(String dateTimeFormat)` | Define o formato para analisar os dados de Hora do arquivo como `java.sql.Types.TIME_WITH_TIMEZONE`. |
| `void setTimeWithTimezoneFormat(DateTimeFormatter dateTimeFormatter)` | Define o formato para analisar os dados de Hora do arquivo como `java.sql.Types.TIME_WITH_TIMEZONE`. |
| `void setTimeWithTimezoneFormat(String timeFormat)` | Define o formato para analisar os dados de Hora do arquivo como `java.sql.Types.TIME_WITH_TIMEZONE`. |
  
## <a name="see-also"></a>Confira também  

[Visão geral do JDBC Driver](overview-of-the-jdbc-driver.md)  
