---
title: Noções básicas sobre transações | Microsoft Docs
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
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a0d737f8cbbcb09d67a73589c5e2a0a37c64d54
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-transactions"></a>Noções básicas sobre transações
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Transações são grupos de operações que são combinadas em unidades lógicas de trabalho. Elas são usadas para controlar e manter a consistência e a integridade de cada ação em uma transação, apesar de erros que poderiam ocorrer no sistema.  
  
 Com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], as transações podem ser locais ou distribuídas. As transações também podem usar níveis de isolamento. Para obter mais informações sobre os níveis de isolamento com suporte pelo driver JDBC, consulte [Noções básicas sobre níveis de isolamento](../../connect/jdbc/understanding-isolation-levels.md).  
  
 Os aplicativos devem controlar transações usando instruções de Transact-SQL ou os métodos fornecidos pelo driver JDBC, mas não ambos. Usar as instruções de Transact-SQL e também os métodos de API do JDBC na mesma transação pode causar problemas, como uma transação não poder ser confirmada quando esperada, uma transação ser confirmada ou revertida e uma nova iniciar inesperadamente ou exceções de "Falha ao retomar a transação".  
  
## <a name="using-local-transactions"></a>Usar transações locais  
 Uma transação é considerada local quando é uma transação de fase única e é tratada diretamente pelo banco de dados. O driver JDBC oferece suporte a transações locais usando vários métodos para o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe, incluindo [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [confirmação](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)e [reversão](../../connect/jdbc/reference/rollback-method.md). As transações locais normalmente são gerenciadas de forma explícita pelo aplicativo ou automaticamente pelo servidor de aplicativos da Plataforma Java, Enterprise Edition (Java EE).  
  
 O exemplo a seguir realiza uma transação local que consiste em duas instruções separadas no `try` bloco. As instruções são executadas em relação à tabela scrapreason no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo e elas são confirmadas se nenhuma exceção for lançada. O código de `catch` bloco reverte a transação se uma exceção for lançada.  
  
 [!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]  
  
## <a name="using-distributed-transactions"></a>Usando transações distribuídas  
 Uma transação distribuída atualiza dados em dois ou mais bancos de dados em rede, mantendo as propriedades atômicas, consistentes, isoladas e duráveis (ACID) importantes do processamento de transações. O suporte a transações distribuídas foi acrescentado à API do JDBC na especificação da API opcional do JDBC 2.0. O gerenciamento de transações distribuídas normalmente é executado de forma automática pelo gerenciador de transações Java Transaction Service (JTS) em um ambiente de servidor de aplicativos Java EE. No entanto, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte a transações distribuídas em qualquer Gerenciador de transações compatível com API de transação Java (JTA).  
  
 O driver JDBC integra-se perfeitamente com [!INCLUDE[msCoName](../../includes/msconame_md.md)] distribuídas de Distributed Transaction Coordinator (MS DTC) para proporcionar um verdadeiro suporte a transações com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. O MS DTC é um recurso de transação distribuída fornecido pela [!INCLUDE[msCoName](../../includes/msconame_md.md)] para [!INCLUDE[msCoName](../../includes/msconame_md.md)] sistemas Windows. O MS DTC usa a tecnologia de processamento de transações comprovada da [!INCLUDE[msCoName](../../includes/msconame_md.md)] para oferecer suporte a recursos XA como o protocolo completo de confirmação distribuída em duas fases e a recuperação de transações distribuídas.  
  
 Para obter mais informações sobre como usar transações distribuídas, consulte [Noções básicas sobre as transações XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
