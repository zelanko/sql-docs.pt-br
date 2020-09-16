---
description: Conformidade do JDBC 4.3 com o JDBC Driver
title: Conformidade com JDBC 4.3 para o driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ce01ec71649549166aa6a3d2f33d9dbb157e08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438348"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Conformidade do JDBC 4.3 com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> As versões anteriores ao Microsoft JDBC Driver 6.4 para SQL Server estão em conformidade apenas com as especificações da API do JDBC (Java Database Connectivity) 4.2. Esta seção não se aplica a versões incluindo a versão 6.4 e anteriores.

A partir da versão 6.4, o Microsoft JDBC Driver para SQL Server passou a ser compatível com JAVA 9 e a gerar `SQLFeatureNotSupportedException` para novas APIs do JDBC 4.3 que possuem métodos não implementados.

Com o Microsoft JDBC Driver 7.0 para SQL Server, agora o driver é compatível com JAVA 10 e oferece suporte às APIs mencionadas abaixo. O driver gera `SQLFeatureNotSupportedException` para outros métodos não implementados das especificações do JDBC 4.3.

|Nova API|Descrição|Implementação notável|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Indica para o driver que uma solicitação, uma unidade de trabalho independente, está sendo inicializada nessa conexão. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Salva os valores dos campos de conexão modificáveis por meio de métodos públicos da API: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Indica para o driver que uma solicitação, uma unidade de trabalho independente, foi concluída. Para obter mais detalhes, confira [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Fecha as instruções criadas durante a unidade de trabalho e reverte todas as transações em aberto. O método também reverte as alterações nos campos de conexão listados acima.|
