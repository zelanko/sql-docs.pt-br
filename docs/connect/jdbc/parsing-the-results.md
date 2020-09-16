---
description: Análise dos resultados
title: Como analisar os resultados | Microsoft Docs
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
ms.openlocfilehash: 93e494ceeac791368a0017f919a9676bbc193966
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438328"
---
# <a name="parsing-the-results"></a>Análise dos resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo descreve como o SQL Server espera que os usuários processem completamente os resultados retornados de consultas.

## <a name="update-counts-and-result-sets"></a>Conjuntos de resultados e contagens de atualizações

Esta seção abordará os dois resultados mais comuns retornados do SQL Server: Update Count e ResultSet. Em geral, uma consulta executada por um usuário fará com que um desses resultados seja retornado. Espera-se que os usuários manipulem ambos ao processar os resultados.

O seguinte código é um exemplo de como um usuário pode iterar por todos os resultados do servidor:
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
Quando você executar uma instrução que resulta em um erro ou em uma mensagem informativa, o SQL Server responderá de maneira diferente, dependendo de se ele pode ou não gerar um plano de execução. A mensagem de erro pode ser lançada imediatamente após a execução da instrução ou pode exigir um conjunto de resultados separado. No último caso, os aplicativos precisam analisar o conjunto de resultados para recuperar a exceção.

Quando o SQL Server não puder gerar um plano de execução, a exceção será lançada imediatamente.

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

Quando o SQL Server retorna uma mensagem de erro em um conjunto de resultados, o conjunto de resultados precisa ser processado para recuperar a exceção.

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

No caso de `String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`, a exceção é lançada imediatamente em `execute()` e `SELECT 1` não é executado.

Se o erro do SQL Server tiver gravidade de `0` a `9`, ele será considerado uma mensagem informativa e será retornado como `SQLWarning`.

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
