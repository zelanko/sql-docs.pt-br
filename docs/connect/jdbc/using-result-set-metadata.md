---
title: Usando conjunto de resultados metadados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d89e8130c897bbf7914b2d3d5d47cba8d38bd01
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39661668"
---
# <a name="using-result-set-metadata"></a>Usando metadados de conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar um conjunto de resultados para obter informações sobre as colunas que ele contém, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa a classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Esta classe contém diversos métodos que retornam informações como um único valor.

Para criar um objeto SQLServerResultSetMetaData, você pode usar o [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.

No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getMetaData da classe SQLServerResultSet é usado para retornar um objeto SQLServerResultSetMetaData e, em seguida, vários métodos para o Objeto SQLServerResultSetMetaData são usados para exibir informações sobre o tipo de dados e o nome das colunas contidas no conjunto de resultados.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Consulte Também

[Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
