---
title: Usando conjunto de resultados metadados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03e6d7d247474c5c5c216ce744591e58f1c0eec8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-result-set-metadata"></a>Usando metadados de conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para consultar um conjunto de resultados para obter informações sobre as colunas que ele contém, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa o [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) classe. Esta classe contém diversos métodos que retornam informações como um único valor.  
  
 Para criar um objeto SQLServerResultSetMetaData, você pode usar o [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método getMetaData da classe SQLServerResultSet é usado para retornar um objeto SQLServerResultSetMetaData e, em seguida, vários métodos para o Objeto SQLServerResultSetMetaData são usados para exibir informações sobre o nome e tipo de dados das colunas contidas no conjunto de resultados.  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Tratando metadados com o JDBC Driver](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
