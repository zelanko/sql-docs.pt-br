---
title: "Tratando instruções complexas | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0bde28417f084dc17c0cdecf8eabf2dd4def3ddc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="handling-complex-statements"></a>Tratando instruções complexas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você usa o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], talvez você precise tratar instruções complexas, incluindo instruções que são geradas dinamicamente em tempo de execução. Instruções complexas geralmente realizam uma variedade de tarefas, incluindo atualizações, inserções e exclusões. Estes tipos de instruções também podem retornar vários conjuntos de resultados e parâmetros de saída. Nestas situações, o código Java que executa as instruções pode não saber com antecedência os tipos e o número de objetos e dados retornados.  
  
 Para processar instruções complexas com eficiência, o driver JDBC fornece vários métodos para consultar os objetos e os dados que são retornados, para que seu aplicativo possa processá-los corretamente. A chave para processar instruções complexas é o [executar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe. Este método retorna um **booliano** valor. Quando o valor for true, o primeiro resultado retornado das instruções será um conjunto de resultados. Quando o valor for false, o primeiro resultado retornado será uma contagem de atualização.  
  
 Quando você souber o tipo de objeto ou dado que foi retornado, você pode usar o [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) ou [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) método para processar os dados. Para prosseguir para o próximo objeto ou dado retornado da instrução complexa, você pode chamar o [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) método.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, uma instrução complexa é construída, combinando uma chamada de procedimento armazenado com uma instrução SQL, as instruções são executadas e, em seguida, um `do` loop for usado para processar todos os conjuntos do resultados e contagens atualizadas que são retornadas.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
