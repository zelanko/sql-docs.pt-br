---
title: Usando uma instrução SQL sem parâmetros | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ffa560842124609b7c5117d86762326ff177f828
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-with-no-parameters"></a>Usando uma instrução SQL sem parâmetros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando uma instrução SQL que não contém parâmetros, você pode usar o [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe para retornar um [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) que conterá os dados solicitados. Para fazer isso, você deve primeiro criar um objeto SQLServerStatement usando o [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, uma instrução SQL é criada e executada e, em seguida, os resultados são lidos do conjunto de resultados.  
  
 [!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]  
  
 Para obter mais informações sobre como usar conjuntos de resultados, consulte [Gerenciando conjuntos de resultados com o Driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
