---
title: Tratando instruções complexas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b2b6dd6bb5fb3a0d7b2e9b78dee87f90f05147df
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781789"
---
# <a name="handling-complex-statements"></a>Tratando instruções complexas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], talvez você precise tratar instruções complexas, incluindo as geradas dinamicamente em tempo de execução. Instruções complexas geralmente realizam uma variedade de tarefas, incluindo atualizações, inserções e exclusões. Estes tipos de instruções também podem retornar vários conjuntos de resultados e parâmetros de saída. Nestas situações, o código Java que executa as instruções pode não saber com antecedência os tipos e o número de objetos e dados retornados.  
  
 Para processar instruções complexas com eficiência, o driver JDBC fornece vários métodos para consultar os objetos e os dados que são retornados, para que seu aplicativo possa processá-los corretamente. A chave para processar instruções complexas é o método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Esse método retorna um **boolean** valor. Quando o valor for true, o primeiro resultado retornado das instruções será um conjunto de resultados. Quando o valor for false, o primeiro resultado retornado será uma contagem de atualização.  
  
 Quando você souber o tipo de objeto ou dados retornados, pode usar o método [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) ou [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) para processar esses dados. Para prosseguir para o próximo objeto ou dados retornados da instrução complexa, chame o método [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md).  
  
 No exemplo a seguir, uma conexão aberta com o banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, uma instrução complexa é realizada, combinando uma chamada de procedimento armazenado com uma instrução SQL, as instruções são executadas e um loop `do` é usado para processar todos os conjuntos de resultados atualizado contagens são retornadas.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>Consulte Também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
