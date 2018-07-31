---
title: Usando metadados de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2f3e0a4e19b30eeb494f89281a01195cf98b7d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982108"
---
# <a name="using-database-metadata"></a>Usando metadados de banco de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar um banco de dados para obter informações sobre seu suporte, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa a classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Esta classe contém diversos métodos que retornam informações como um único valor ou um conjunto de resultados.  
  
 Para criar um objeto SQLServerDatabaseMetaData, você pode usar o método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) para obter informações sobre o banco de dados para o qual é conectado.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getMetaData da classe SQLServerConnection é usado para retornar um objeto SQLServerDatabaseMetadata e, em seguida, vários métodos das Objeto SQLServerDatabaseMetaData são usados para exibir informações sobre o driver, versão do driver, nome do banco de dados e versão do banco de dados.  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
