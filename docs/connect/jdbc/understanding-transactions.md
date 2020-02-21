---
title: Noções básicas sobre transações| Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d5a6caa9c9bf1766b59aa813719d1461b6ef1aa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027339"
---
# <a name="understanding-transactions"></a>Noções básicas sobre transações

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Transações são grupos de operações que são combinadas em unidades lógicas de trabalho. Elas são usadas para controlar e manter a consistência e a integridade de cada ação em uma transação, apesar de erros que poderiam ocorrer no sistema.

Com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], as transações podem ser locais ou distribuídas. As transações também podem usar níveis de isolamento. Confira mais informações sobre os níveis de isolamento compatíveis no JDBC Driver em [Noções básicas sobre níveis de isolamento](../../connect/jdbc/understanding-isolation-levels.md).

Os aplicativos devem controlar transações usando instruções de Transact-SQL ou os métodos fornecidos pelo driver JDBC, mas não ambos. Usar as instruções de Transact-SQL e também os métodos de API do JDBC na mesma transação pode causar problemas, como uma transação não poder ser confirmada quando esperada, uma transação ser confirmada ou revertida e uma nova iniciar inesperadamente ou exceções de "Falha ao retomar a transação".

## <a name="using-local-transactions"></a>Como usar transações locais

Uma transação é considerada local quando é uma transação de fase única e é tratada diretamente pelo banco de dados. O driver JDBC oferece suporte a transações locais usando vários métodos da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), incluindo [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) e [rollback](../../connect/jdbc/reference/rollback-method.md). As transações locais normalmente são gerenciadas de forma explícita pelo aplicativo ou automaticamente pelo servidor de aplicativos da Plataforma Java, Enterprise Edition (Java EE).

O exemplo a seguir realiza uma transação local que consiste em duas instruções separadas no bloco `try`. As instruções são executadas em relação à tabela Production.ScrapReason no banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e elas são confirmadas se nenhuma exceção for gerada. O código no bloco `catch` reverterá a transação se uma exceção for lançada.

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>Como usar transações distribuídas

Uma transação distribuída atualiza dados em dois ou mais bancos de dados em rede, mantendo as propriedades atômicas, consistentes, isoladas e duráveis (ACID) importantes do processamento de transações. O suporte a transações distribuídas foi acrescentado à API do JDBC na especificação da API opcional do JDBC 2.0. O gerenciamento de transações distribuídas normalmente é executado de forma automática pelo gerenciador de transações Java Transaction Service (JTS) em um ambiente de servidor de aplicativos Java EE. Entretanto, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte a transações distribuídas em qualquer gerenciador de transações compatível com a API de transação Java (JTA).

O driver JDBC integra-se perfeitamente com o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Coordenador de Transações Distribuídas (MS DTC) para proporcionar um verdadeiro suporte de transação distribuída com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O MS DTC é um recurso de transação distribuída fornecido pela [!INCLUDE[msCoName](../../includes/msconame_md.md)] para sistemas [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows. O MS DTC usa a tecnologia de processamento de transações comprovada da [!INCLUDE[msCoName](../../includes/msconame_md.md)] para oferecer suporte a recursos XA como, por exemplo, o protocolo completo de confirmação distribuída de duas fases e a recuperação de transações distribuídas.

Confira mais informações sobre como usar transações distribuídas em [Noções básicas sobre transações XA](../../connect/jdbc/understanding-xa-transactions.md).

## <a name="see-also"></a>Confira também

[Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
