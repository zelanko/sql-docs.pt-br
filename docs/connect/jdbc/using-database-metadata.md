---
title: Usando metadados de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58e5e403bb33663654c3cd5f0f884c13957d04f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711264"
---
# <a name="using-database-metadata"></a>Usando metadados de banco de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar um banco de dados para obter informações sobre seu suporte, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa a classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Esta classe contém diversos métodos que retornam informações como um único valor ou um conjunto de resultados.

Para criar um objeto SQLServerDatabaseMetaData, você pode usar o método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) para obter informações sobre o banco de dados para o qual é conectado.

No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getMetaData da classe SQLServerConnection é usado para retornar um objeto SQLServerDatabaseMetadata e, em seguida, vários métodos das Objeto SQLServerDatabaseMetaData são usados para exibir informações sobre o driver, versão do driver, nome do banco de dados e versão do banco de dados.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>Consulte Também

[Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
