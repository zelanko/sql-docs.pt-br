---
title: Como usar metadados do conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed0b1eedcafa1fab59d17f756523fc0fc189200
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026120"
---
# <a name="using-result-set-metadata"></a>Como usar metadados do conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar um conjunto de resultados para obter informações sobre as colunas que ele contém, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa a classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Esta classe contém diversos métodos que retornam informações como um único valor.

Para criar um objeto SQLServerResultSetMetaData, você pode usar o método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).

No exemplo a seguir, uma conexão aberta com o banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passado para a função, o método getMetaData da classe SQLServerResultSet é usado para retornar um SQLServerResultSetMetaData e, em seguida, vários métodos do objeto SQLServerResultSetMetaData são usados para exibir informações sobre o nome e o tipo de dados das colunas contidas no conjunto de resultados.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Confira também

[Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
