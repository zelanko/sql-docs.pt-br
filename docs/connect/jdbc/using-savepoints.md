---
title: Como usar pontos de salvamento | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d860e368fe66ce926687fd343fe9f23704cfc7d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026136"
---
# <a name="using-savepoints"></a>Como usar pontos de salvamento

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os pontos de salvamento oferecem um mecanismo para reverter partes de transações. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode criar um ponto de salvamento usando a instrução savepoint_name SAVE TRANSACTION. Posteriormente, você executa uma instrução ROLLBACK TRANSACTION nome_do_ponto_de_salvamento para reverter ao ponto de salvamento em vez de reverter ao início da transação.

Os pontos de salvamento são úteis em situações onde erros são improváveis. O uso de um ponto de salvamento para reverter parte de uma transação na ocorrência de um erro não frequente pode ser mais eficiente do que testar cada transação para verificar se uma atualização é válida antes de fazer a atualização. As atualizações e reversões são operações caras, portanto, pontos de salvamento só serão eficientes se a probabilidade de encontrar o erro for baixa e o custo de verificar a validade de uma atualização com antecedência for relativamente alto.

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de pontos de salvamento por meio do método [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Usando o método setSavepoint, você pode criar um ponto de salvamento nomeado ou sem nome na transação atual, e o método retornará um objeto [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md). Podem ser criados vários pontos de salvamento em uma transação. Para reverter uma transação a um determinado ponto de salvamento, você pode passar o objeto SQLServerSavepoint para o método [rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md).

No exemplo a seguir, um ponto de salvamento é usado durante a execução de uma transação local que consiste em duas instruções separadas no bloco `try`. As instruções são executadas na tabela Production.ScrapReason do banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e um ponto de salvamento é usado para reverter a segunda instrução. Isso faz com que apenas a primeira instrução seja confirmada no banco de dados.

[!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]

## <a name="see-also"></a>Confira também

[Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
