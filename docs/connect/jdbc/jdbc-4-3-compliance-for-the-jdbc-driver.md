---
title: JDBC 4.3 conformidade para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f38b700f998babd9af54c3bf8a27409a4d2b6ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623934"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformidade do JDBC 4.3 com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> As versões anteriores ao Microsoft JDBC Driver 6.4 para SQL Server estão em conformidade apenas com as especificações da API do JDBC (Java Database Connectivity) 4.2. Esta seção não se aplica a versões incluindo a versão 6.4 e anteriores.

A partir da versão 6.4, Microsoft JDBC Driver para SQL Server é compatível com o JAVA 9 e gera `SQLFeatureNotSupportedException` para novas APIs do JDBC 4.3 que têm não implementados métodos.

Com o Microsoft JDBC Driver 7.0 para a versão do SQL Server, o driver agora é JAVA 10 compatível e dá suporte a abaixo mencionado APIs. O driver lançará `SQLFeatureNotSupportedException` para outros métodos não implementados das especificações do JDBC 4.3.

|Nova API|Descrição|Implementação notável|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Dicas para o driver que uma solicitação, uma unidade independente de trabalho, está começando nessa conexão. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva os valores dos campos de conexão que podem ser modificadas por meio de métodos de API públicos: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall `, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void java.sql.connection.endRequest()|Dicas para o driver que uma solicitação, uma unidade independente de trabalho, foi concluída. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Fecha as instruções que são criadas durante a unidade de trabalho e reverte qualquer transação aberta. O método também reverterá as alterações para os campos de conexão que estão listados acima.|
