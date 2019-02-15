---
title: Usando a API de cópia em massa para a operação de inserção em lotes para o Driver JDBC MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3d3c7cc4d8dd7beeb620a211b2f41a1d1105a04
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737097"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Usando a API de cópia em massa para a operação de inserção em lote

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 para SQL Server pode suportar usando a API de cópia em massa para operações de inserção em lotes para o Data Warehouse do Azure. Esse recurso permite aos usuários permitir que o driver ao realizar a operação de cópia em massa abaixo quando operações de inserção em lotes em execução. Os objetivos de driver para atingir a melhoria no desempenho ao inserir os mesmos dados que o driver teria com o lote regular de operação de inserção. O driver analisa a consulta de SQL do usuário, aproveitando a API de cópia em massa em vez da operação de inserção em lotes usual. Veja abaixo as várias maneiras de habilitar a API de cópia em massa para o lote inserem recurso, bem como a lista de suas limitações. Esta página também contém um código de exemplo pequeno que demonstra um uso e o aumento de desempenho.

Esse recurso só é aplicável aos PreparedStatement e do CallableStatement `executeBatch()`  &  `executeLargeBatch()` APIs.

## <a name="pre-requisites"></a>Pré-requisitos

Existem dois pré-requisitos para habilitar a API de cópia em massa para inserção em lotes.

* O servidor deve ser o Data Warehouse do Azure.
* A consulta deve ser uma consulta insert (a consulta pode conter comentários, mas a consulta deve começar com a palavra-chave de inserção para esse recurso entrar em vigor).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Habilitando a API de cópia em massa para inserção em lotes

Há três maneiras de habilitar a API de cópia em massa para inserção em lotes.

### <a name="1-enabling-with-connection-property"></a>1. Habilitando com a propriedade de conexão

Adicionando **useBulkCopyForBatchInsert = true;** para a conexão a cadeia de caracteres habilita esse recurso.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Habilitando com o método setUseBulkCopyForBatchInsert() do objeto sqlserverconnection em questão

Chamando **SQLServerConnection.setUseBulkCopyForBatchInsert(true)** habilita esse recurso.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** recupera o valor atual para **useBulkCopyForBatchInsert** propriedade de conexão.

O valor para **useBulkCopyForBatchInsert** permanece constante para cada PreparedStatement no momento da inicialização. Qualquer chamada subsequente para **SQLServerConnection.setUseBulkCopyForBatchInsert()** não afetará o PreparedStatement já criada em relação ao seu valor.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Habilitando com o método setUseBulkCopyForBatchInsert() do objeto SQLServerDataSource

Semelhante ao acima, mas usando SQLServerDataSource para criar um objeto SQLServerConnection. Ambos os métodos geram o mesmo resultado.

## <a name="known-limitations"></a>Limitações conhecidas

Atualmente, há essas limitações que se aplicam a esse recurso.

* Inserir consultas que contêm valores sem parâmetros (por exemplo, `INSERT INTO TABLE VALUES (?, 2`)), não têm suporte. Caracteres curinga (?) é os únicos parâmetros com suporte para essa função.
* Inserir consultas que contêm expressões de INSERT-SELECT (por exemplo, `INSERT INTO TABLE SELECT * FROM TABLE2`), não têm suporte.
* Inserir consultas que contêm várias expressões de valor (por exemplo, `INSERT INTO TABLE VALUES (1, 2) (3, 4)`), não têm suporte.
* Consultas INSERT que são seguidas a cláusula OPTION, unidas com várias tabelas ou seguidas de outra consulta, não têm suporte.
* Devido a limitações de API de cópia em massa, `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY`, e `GEOGRAPHY` tipos de dados, no momento, não há suporte para isso recurso.

Se a consulta falhar devido a não erros relacionados ao "SQL server", o driver registrará em log a mensagem de erro e o fallback para a lógica original para inserção em lotes.

## <a name="example"></a>Exemplo

Abaixo está um código de exemplo que demonstra o caso de uso para uma operação de inserção do lote no DW do Azure de mil linhas, os dois cenários (API de cópia em massa de vs regular).

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

## <a name="see-also"></a>Consulte Também

[Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
