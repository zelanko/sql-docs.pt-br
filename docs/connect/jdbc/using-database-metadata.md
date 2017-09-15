---
title: Usando metadados de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 421da278e1a4503a73fb4f4f8a8aba0b3cff672f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-database-metadata"></a>Usando metadados de banco de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar um banco de dados para obter informações sobre o que ele dá suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa o [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) classe. Esta classe contém diversos métodos que retornam informações como um único valor ou um conjunto de resultados.  
  
 Para criar um objeto SQLServerDatabaseMetaData, você pode usar o [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe para obter informações sobre o banco de dados que está conectado.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getMetaData da classe SQLServerConnection é usado para retornar um objeto SQLServerDatabaseMetadata e, em seguida, vários métodos para o Objeto SQLServerDatabaseMetaData são usados para exibir informações sobre o driver, versão do driver, nome do banco de dados e versão do banco de dados.  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
