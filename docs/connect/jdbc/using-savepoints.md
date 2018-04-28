---
title: Usando pontos de salvamento | Microsoft Docs
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
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dccc8739a02fa478c153bbbe1702b925942f8efd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-savepoints"></a>Usando pontos de salvamento
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Os pontos de salvamento oferecem um mecanismo para reverter partes de transações. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode criar um ponto de salvamento usando a instrução SAVE TRANSACTION nome_do_ponto_de_salvamento. Posteriormente, você executa uma instrução ROLLBACK TRANSACTION nome_do_ponto_de_salvamento para reverter ao ponto de salvamento em vez de reverter ao início da transação.  
  
 Os pontos de salvamento são úteis em situações onde erros são improváveis. O uso de um ponto de salvamento para reverter parte de uma transação na ocorrência de um erro não frequente pode ser mais eficiente do que testar cada transação para verificar se uma atualização é válida antes de fazer a atualização. As atualizações e reversões são operações caras, portanto, pontos de salvamento só serão eficientes se a probabilidade de encontrar o erro for baixa e o custo de verificar a validade de uma atualização com antecedência for relativamente alto.  
  
 O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte ao uso de pontos de salvamento por meio de [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) método do [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Usando o método setSavepoint, você pode criar um ponto de salvamento nomeado ou sem nome dentro da transação atual, e o método retornará um [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto. Podem ser criados vários pontos de salvamento em uma transação. Para reverter uma transação para um determinado ponto de salvamento, você pode passar o objeto SQLServerSavepoint para o [rollback (Java.SQL. savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) método.  
  
 No exemplo a seguir, um ponto de salvamento é usado durante a execução de uma transação local que consiste em duas instruções separadas no `try` bloco. As instruções são executadas em relação à tabela scrapreason no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo e um ponto de salvamento é usado para reverter a segunda instrução. Isso faz com que apenas a primeira instrução seja confirmada no banco de dados.  
  
 [!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
