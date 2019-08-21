---
title: Como usar metadados de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce2bf9d72136b303ee3bc974f3aede313233a82
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026425"
---
# <a name="using-database-metadata"></a>Como usar metadados de banco de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar um banco de dados para obter informações sobre seu suporte, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa a classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Esta classe contém diversos métodos que retornam informações como um único valor ou um conjunto de resultados.

Para criar um objeto SQLServerDatabaseMetaData, você pode usar o método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) para obter informações sobre o banco de dados para o qual é conectado.

No exemplo a seguir, uma conexão aberta com o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passada para a função, o método getMetaData da classe SQLServerConnection é usado para retornar um objeto SQLServerDatabaseMetadata e, em seguida, vários métodos do O objeto SQLServerDatabaseMetaData é usado para exibir informações sobre o driver, a versão do driver, o nome do banco de dados e a versão do banco de dados.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>Confira também

[Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
