---
title: API de cópia em massa para inserção em lote no JDBC
description: O Microsoft JDBC Driver para SQL Server dá suporte ao uso da Cópia em Massa em operações de inserção em lote no Data Warehouse do Azure para carregar os dados mais rapidamente no banco de dados.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14074b0136baf800b038e4b113325e81d65dc3e7
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96442594"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Como usar a API de cópia em massa para a operação de inserção em lote

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver 7.0 para SQL Server dá suporte ao uso da API de Cópia em Massa para operações de inserção em lote para o Data Warehouse do Azure. Esse recurso permite que os usuários habilitem o driver para executar a operação de Cópia em Massa abaixo ao executar operações de inserção em lote. O driver visa obter um aprimoramento no desempenho ao inserir os mesmos dados que o driver teria com a operação de inserção em lote normal. O driver analisa a Consulta SQL do usuário, utilizando a API de Cópia em Massa no lugar da operação de inserção em lote usual. Abaixo há várias maneiras de habilitar a API de Cópia em Massa para o recurso de inserção em lote, bem como a lista de limitações. Essa página também contém um pequeno código de exemplo que demonstra um uso e o aumento de desempenho também.

Esse recurso só é aplicável a APIs `executeBatch()` & `executeLargeBatch()` de PreparedStatement e CallableStatement.

## <a name="prerequisites"></a>Pré-requisitos

Há dois pré-requisito para habilitar a API de Cópia em Massa para inserção em lote.

* O servidor deve ser o Data Warehouse do Azure.
* A consulta deve ser de inserção (ela pode conter comentários, mas deve começar com a palavra-chave INSERT para que esse recurso entre em vigor).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Como habilitar a API de cópia em massa para inserção em lote

Há três maneiras de habilitar a API de Cópia em Massa para inserção em lote.

### <a name="1-enabling-with-connection-property"></a>1. Como habilitar com a propriedade de conexão

Adicionar **useBulkCopyForBatchInsert=true;** à cadeia de conexão habilita esse recurso.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Como habilitar com o método setUseBulkCopyForBatchInsert() do objeto SQLServerConnection

Chamar **SQLServerConnection.setUseBulkCopyForBatchInsert(true)** habilita esse recurso.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** recupera o valor atual da propriedade de conexão **useBulkCopyForBatchInsert**.

O valor de **useBulkCopyForBatchInsert** permanece constante para cada PreparedStatement no momento da inicialização. As chamadas subsequentes a **SQLServerConnection.setUseBulkCopyForBatchInsert()** não afetarão o PreparedStatement já criado com relação ao valor dele.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Como habilitar com o método setUseBulkCopyForBatchInsert() do objeto SQLServerDataSource

Semelhante ao exposto acima, mas usando SQLServerDataSource para criar um objeto SQLServerConnection. Ambos os métodos geram o mesmo resultado.

## <a name="known-limitations"></a>Limitações conhecidas

No momento, há essas limitações aplicáveis a esse recurso.

* Não há suporte para consultas de inserção que contenham valores não parametrizados (por exemplo, `INSERT INTO TABLE VALUES (?, 2`)). Curingas (?) são os únicos parâmetros com suporte para essa função.
* Não há suporte para consultas de inserção que contenham expressões INSERT-SELECT (por exemplo, `INSERT INTO TABLE SELECT * FROM TABLE2`).
* Não há suporte para consultas de inserção que contenham expressões VALUE múltiplas (por exemplo, `INSERT INTO TABLE VALUES (1, 2) (3, 4)`).
* Não há suporte para consultas de inserção que sejam seguidas pela cláusula OPTION, unidas com várias tabelas ou seguidas por outra consulta.
* Devido às limitações da API de Cópia em Massa, no momento, não há suporte para os tipos de dados `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY` e `GEOGRAPHY` para esse recurso.

Se a consulta falhar devido a erros não relacionados ao "SQL Server”, o driver registrará em log a mensagem de erro e fará fallback para a lógica original para inserção em lote.

## <a name="example"></a>Exemplo

Confira abaixo um código de exemplo que demonstra o caso de uso de uma operação de inserção em lote no Azure Synapse Analytics de mil linhas nos dois cenários (normal x API de Cópia em Massa).

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

[Melhorando o desempenho e a confiabilidade com o JDBC Driver](improving-performance-and-reliability-with-the-jdbc-driver.md)
