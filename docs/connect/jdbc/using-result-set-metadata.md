---
title: Usando metadados do conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86e41f52ed8296c46cfd7b167407b10fc9f0b285
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005945"
---
# <a name="using-result-set-metadata"></a>Usando metadados de conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar um conjunto de resultados para obter informações sobre as colunas que ele contém, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa a classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Esta classe contém diversos métodos que retornam informações como um único valor.

Para criar um objeto SQLServerResultSetMetaData, você pode usar o método [GetMetadata](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) .

No exemplo a seguir, uma conexão aberta com o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passada para a função, o método getMetaData da classe SQLServerResultSet é usado para retornar um objeto SQLServerResultSetMetaData e, em seguida, vários métodos do O objeto SQLServerResultSetMetaData é usado para exibir informações sobre o nome e o tipo de dados das colunas contidas no conjunto de resultados.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Consulte Também

[Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
