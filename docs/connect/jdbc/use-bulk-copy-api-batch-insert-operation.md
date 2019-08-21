---
title: Como usar a API de cópia em massa para a operação de inserção em lote para o driver MSSQL JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027101"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Como usar a API de cópia em massa para a operação de inserção em lote

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver 7,0 para SQL Server dá suporte ao uso da API de cópia em massa para operações de inserção em lote para o Azure data warehouse. Esse recurso permite que os usuários habilitem o driver para executar a operação de cópia em massa abaixo da execução de operações de inserção em lote. O driver visa obter uma melhoria no desempenho ao inserir os mesmos dados que o driver teria com a operação de inserção em lote normal. O driver analisa a consulta SQL do usuário, aproveitando a API de cópia em massa no lugar da operação de inserção de lote usual. Abaixo estão várias maneiras de habilitar a API de cópia em massa para o recurso de inserção em lote, bem como a lista de suas limitações. Essa página também contém um pequeno código de exemplo que demonstra um uso e o aumento de desempenho também.

Esse recurso é aplicável somente às APIs do PreparedStatement e `executeBatch()` do  &  `executeLargeBatch()` CallableStatement.

## <a name="prerequisites"></a>Prerequisites

Há dois pré-requisitos para habilitar a API de cópia em massa para inserção em lote.

* O servidor deve ser o data warehouse do Azure.
* A consulta deve ser uma consulta de inserção (a consulta pode conter comentários, mas a consulta deve começar com a palavra-chave INSERT para que esse recurso entre em vigor).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Habilitando a API de cópia em massa para inserção em lote

Há três maneiras de habilitar a API de cópia em massa para inserção em lote.

### <a name="1-enabling-with-connection-property"></a>1. Habilitando com a propriedade Connection

Adicionar **useBulkCopyForBatchInsert = true;** à cadeia de conexão habilita esse recurso.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Habilitando com o método setUseBulkCopyForBatchInsert () do objeto SQLServerConnection

Chamar **SQLServerConnection. setUseBulkCopyForBatchInsert (true)** habilita esse recurso.

**SQLServerConnection. getUseBulkCopyForBatchInsert ()** recupera o valor atual para a propriedade de conexão **useBulkCopyForBatchInsert** .

O valor de **useBulkCopyForBatchInsert** permanece constante para cada PreparedStatement no momento da inicialização. Todas as chamadas subsequentes para **SQLServerConnection. setUseBulkCopyForBatchInsert ()** não afetarão o PreparedStatement já criado em relação ao seu valor.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Habilitando com o método setUseBulkCopyForBatchInsert () do objeto SQLServerDataSource

Semelhante a acima, mas usando SQLServerDataSource para criar um objeto SQLServerConnection. Ambos os métodos geram o mesmo resultado.

## <a name="known-limitations"></a>Limitações conhecidas

Atualmente, há essas limitações que se aplicam a esse recurso.

* Não há suporte para inserir consultas que contêm valores não parametrizados ( `INSERT INTO TABLE VALUES (?, 2`por exemplo,)). Curingas (?) são os únicos parâmetros com suporte para essa função.
* Não há suporte para inserir consultas que contêm expressões de inserção/ `INSERT INTO TABLE SELECT * FROM TABLE2`seleção (por exemplo,).
* Não há suporte para consultas Insert que contêm várias expressões de `INSERT INTO TABLE VALUES (1, 2) (3, 4)`valor (por exemplo,).
* Não há suporte para consultas Insert seguidas pela cláusula OPTION, Unidas com várias tabelas ou seguidas por outra consulta.
* Devido às limitações da API de cópia em massa `MONEY`, `SMALLMONEY` `DATETIMEOFFSET` `DATETIME` `DATE` `SMALLDATETIME`,,,,,,, e `GEOGRAPHY` tipos de dados, atualmente não são compatíveis com este `TIME` `GEOMETRY` recurso.

Se a consulta falhar devido a erros não "SQL Server" relacionados, o driver registrará em log a mensagem de erro e fará fallback para a lógica original para inserção em lote.

## <a name="example"></a>Exemplo

Abaixo está um exemplo de código que demonstra o caso de uso para uma operação de inserção em lote em relação ao DW do Azure de mil linhas, para cenários (normal versus a API de cópia em massa).

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

Resultado:

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>Confira também

[Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
