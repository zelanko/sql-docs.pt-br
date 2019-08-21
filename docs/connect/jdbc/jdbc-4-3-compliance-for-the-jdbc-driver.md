---
title: Conformidade com JDBC 4,3 para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed9b10ad9e9a927789505c7d7327c6cf4d1ff3c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027939"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformidade do JDBC 4.3 com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> As versões anteriores ao Microsoft JDBC Driver 6.4 para SQL Server estão em conformidade apenas com as especificações da API do JDBC (Java Database Connectivity) 4.2. Esta seção não se aplica a versões incluindo a versão 6.4 e anteriores.

A partir da versão 6,4, o Microsoft JDBC Driver for SQL Server é compatível com Java `SQLFeatureNotSupportedException` 9 e gera para novas APIs JDBC 4,3 que têm métodos não implementados.

Com o Microsoft JDBC Driver 7,0 para versão SQL Server, o driver agora é compatível com JAVA 10 e dá suporte a APIs mencionadas abaixo. O driver gera `SQLFeatureNotSupportedException` outros métodos não implementados das especificações do JDBC 4,3.

|Nova API|Descrição|Implementação notável|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Dicas para o driver que uma solicitação, uma unidade de trabalho independente, está começando nessa conexão. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva os valores dos campos de conexão que podem ser modificados por meio de métodos `databaseAutoCommitMode`de API pública: `sendTimeAsDatetime` `networkTimeout`, `statementPoolingCacheSize` `enablePrepareOnFirstPreparedStatementCall` `transactionIsolationLevel` `holdability` `disableStatementPooling` `serverPreparedStatementDiscardThreshold`,,,,,,,, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Dicas para o driver que uma solicitação, uma unidade de trabalho independente, foi concluída. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Fecha as instruções criadas durante a unidade de trabalho e reverte as transações abertas. O método também reverte as alterações para os campos de conexão listados acima.|
