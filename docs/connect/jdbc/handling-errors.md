---
title: Tratamento de erros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eee315022a94795dd27ae8ae7fee6cc784912bec
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787321"
---
# <a name="handling-errors"></a>Tratando erros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], todas as condições de erro de banco de dados são retornadas para seu aplicativo Java como exceções, usando a classe [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). Os seguintes métodos da classe SQLServerException são herdados de java.sql.SQLException e java.lang.Throwable; e eles podem ser usados para retornar informações específicas sobre o erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ocorreu:  
  
-   O getSQLState retorna o X/Open padrão ou código de estado SQL99 da exceção.  
  
-   O getErrorCode retorna o número de erro de banco de dados específico.  
  
-   O getMessage retorna o texto completo da exceção. O texto de mensagem de erro descreve o problema e geralmente inclui espaços reservados para informações, como nomes de objeto, que são inseridos na mensagem de erro quando é exibido.  
  
-   getNextException retorna o próximo objeto SQLServerException ou nulo se não houver nenhum outro objeto de exceção para retornar.  
  
 No exemplo a seguir, uma conexão aberta para o banco de dados de amostra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função e uma instrução SQL malformada é construída, que não tem uma cláusula FROM. Em seguida, a instrução é executada e uma exceção SQL é processada.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Consulte Também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
