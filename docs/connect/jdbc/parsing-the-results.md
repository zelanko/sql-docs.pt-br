---
title: Analisando os resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 127c97ec155ef1e19df4103b12a6e10b8b67fe74
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027858"
---
# <a name="parsing-the-results"></a>Análise dos resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo descreve como SQL Server espera que os usuários processem completamente os resultados retornados de qualquer consulta.

## <a name="update-counts-and-result-sets"></a>Contagens de atualizações e conjuntos de resultados

Esta seção abordará os dois resultados mais comuns retornados de SQL Server: contagem de atualização e ResultSet. Em geral, qualquer consulta executada por um usuário fará com que um desses resultados seja retornado; Espera-se que os usuários manipulem ambos ao processar os resultados.

O código a seguir é um exemplo de como um usuário pode iterar por todos os resultados do servidor:
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>Exceções
Quando você executa uma instrução que resulta em um erro ou em uma mensagem informativa, SQL Server responderá de forma diferente, dependendo se ela pode gerar um plano de execução. A mensagem de erro pode ser gerada imediatamente após a execução da instrução ou pode exigir um conjunto de resultados separado. No último caso, os aplicativos precisam analisar o conjunto de resultados para recuperar a exceção.

Quando SQL Server não puder gerar um plano de execução, a exceção será lançada imediatamente.

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

Quando SQL Server retorna uma mensagem de erro em um conjunto de resultados, o conjunto de resultados precisa ser processado para recuperar a exceção.

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

Se a execução da instrução gerar vários conjuntos de resultados, cada conjunto de resultados precisará ser processado até que aquele com a exceção seja atingido.

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

No caso do `String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`, a exceção é lançada `execute()` imediatamente e `SELECT 1` não é executada.

Se o erro de SQL Server tiver severidade de `0` para `9`, ele será considerado uma mensagem informativa e será retornado `SQLWarning`como.

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)
