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
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-database-metadata"></a>Usando metadados de banco de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar um banco de dados para obter informações sobre o que ele dá suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa o [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) classe. Esta classe contém diversos métodos que retornam informações como um único valor ou um conjunto de resultados.  
  
 Para criar um objeto SQLServerDatabaseMetaData, você pode usar o [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe para obter informações sobre o banco de dados que está conectado.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getMetaData da classe SQLServerConnection é usado para retornar um objeto SQLServerDatabaseMetadata e, em seguida, vários métodos para o Objeto SQLServerDatabaseMetaData são usados para exibir informações sobre o driver, versão do driver, nome do banco de dados e versão do banco de dados.  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
