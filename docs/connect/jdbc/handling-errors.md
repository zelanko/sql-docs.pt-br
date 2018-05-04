---
title: Tratamento de erros | Microsoft Docs
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
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33f9c9daa495c26b1a1e35869016f0e7382d9d1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors"></a>Tratando erros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], todas as condições de erro de banco de dados são retornadas ao seu aplicativo Java como exceções usando o [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) classe. Os seguintes métodos da classe SQLServerException são herdados de Java.SQL. SqlException e Throwable; e eles podem ser usados para retornar informações específicas sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erro que ocorreu:  
  
-   getSQLState retorna o X / Open padrão ou o código de estado SQL99 da exceção.  
  
-   getErrorCode retorna o número de erro do banco de dados específico.  
  
-   getMessage retorna o texto completo da exceção. O texto de mensagem de erro descreve o problema e geralmente inclui espaços reservados para informações, como nomes de objeto, que são inseridos na mensagem de erro quando é exibido.  
  
-   getNextException retorna o próximo objeto SQLServerException ou nulo se não houver nenhum outro objeto de exceção para retornar.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função e uma instrução SQL malformada é construída que não tenha uma cláusula FROM. Em seguida, a instrução é executada e uma exceção SQL é processada.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
